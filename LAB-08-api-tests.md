# Lab 08 — Add an API and meaningful tests

**Week:** 10. **Prerequisite:** finished Lab 07. **Target:** local notes app and disposable test database.

## A. Add a read-only API

Append to `notes/views.py`:

~~~python
from django.http import JsonResponse

@require_http_methods(["GET"])
def note_api(request, pk):
    if not request.user.is_authenticated:
        return JsonResponse({"error": "authentication_required"}, status=401)
    note = get_object_or_404(Note, pk=pk, owner=request.user)
    return JsonResponse({"id": note.pk, "body": note.body})
~~~

Add this entry inside the existing urlpatterns list in `notes/urls.py`:

~~~python
path("api/notes/<int:pk>/", views.note_api, name="note-api"),
~~~

Contract: GET only, existing session cookie, id and body only. A guest receives JSON 401; an inaccessible object receives the framework's 404 response, which is not guaranteed to be JSON. A production API would standardize its error format. CORS is not an authorization control.

## B. Create the tests

Replace `notes/tests.py`:

~~~python
from django.contrib.auth import get_user_model
from django.test import Client, TestCase
from .models import Note

class ProtectionTests(TestCase):
    def setUp(self):
        User = get_user_model()
        self.alice = User.objects.create_user("alice")
        self.bob = User.objects.create_user("bob")
        self.note = Note.objects.create(owner=self.alice, body="Private text")
        self.detail = f"/notes/{self.note.pk}/"
        self.edit = self.detail + "edit/"
        self.delete = self.detail + "delete/"
        self.api = f"/api/notes/{self.note.pk}/"

    def test_guest_cannot_read(self):
        self.assertEqual(self.client.get(self.detail).status_code, 302)

    def test_owner_can_read(self):
        self.client.force_login(self.alice)
        self.assertContains(self.client.get(self.detail), "Private text")

    def test_other_user_cannot_read(self):
        self.client.force_login(self.bob)
        response = self.client.get(self.detail)
        self.assertEqual(response.status_code, 404)
        self.assertNotContains(response, "Private text", status_code=404)

    def test_create_uses_verified_owner(self):
        self.client.force_login(self.bob)
        response = self.client.post("/", {"body": "Bob note", "owner": self.alice.pk})
        self.assertEqual(response.status_code, 302)
        self.assertEqual(Note.objects.get(body="Bob note").owner, self.bob)

    def test_owner_can_edit(self):
        self.client.force_login(self.alice)
        self.assertEqual(self.client.post(self.edit, {"body": "Revised"}).status_code, 302)
        self.note.refresh_from_db()
        self.assertEqual(self.note.body, "Revised")
        self.assertEqual(self.note.owner, self.alice)

    def test_other_user_cannot_edit(self):
        self.client.force_login(self.bob)
        self.assertEqual(self.client.post(self.edit, {"body": "Changed"}).status_code, 404)
        self.note.refresh_from_db()
        self.assertEqual(self.note.body, "Private text")

    def test_other_user_cannot_delete(self):
        self.client.force_login(self.bob)
        self.assertEqual(self.client.post(self.delete).status_code, 404)
        self.assertTrue(Note.objects.filter(pk=self.note.pk).exists())

    def test_get_cannot_delete(self):
        self.client.force_login(self.alice)
        self.assertEqual(self.client.get(self.delete).status_code, 405)
        self.assertTrue(Note.objects.filter(pk=self.note.pk).exists())

    def test_owner_can_delete(self):
        self.client.force_login(self.alice)
        self.assertEqual(self.client.post(self.delete).status_code, 302)
        self.assertFalse(Note.objects.filter(pk=self.note.pk).exists())

    def test_template_escapes_markup(self):
        self.note.body = "<b>Private</b>"
        self.note.save()
        self.client.force_login(self.alice)
        self.assertContains(self.client.get(self.detail), "&lt;b&gt;Private&lt;/b&gt;")

    def test_api_checks_actor_and_owner(self):
        self.assertEqual(self.client.get(self.api).status_code, 401)
        self.client.force_login(self.alice)
        self.assertEqual(self.client.get(self.api).json(), {
            "id": self.note.pk, "body": "Private text"
        })
        self.client.force_login(self.bob)
        self.assertEqual(self.client.get(self.api).status_code, 404)

    def test_api_is_read_only(self):
        self.client.force_login(self.alice)
        self.assertEqual(self.client.post(self.api).status_code, 405)

    def test_csrf_missing_invalid_and_valid(self):
        client = Client(enforce_csrf_checks=True)
        client.force_login(self.alice)
        client.get("/")
        token = client.cookies["csrftoken"].value
        count = Note.objects.count()
        self.assertEqual(client.post("/", {"body": "No token"}).status_code, 403)
        self.assertEqual(client.post("/", {
            "body": "Bad token", "csrfmiddlewaretoken": "invalid"
        }).status_code, 403)
        self.assertEqual(Note.objects.count(), count)
        self.assertEqual(client.post("/", {
            "body": "Valid token", "csrfmiddlewaretoken": token
        }).status_code, 302)
        self.assertEqual(Note.objects.count(), count + 1)

    def test_validation_rejects_empty_and_long_body(self):
        self.client.force_login(self.alice)
        count = Note.objects.count()
        self.client.post("/", {"body": ""})
        self.client.post("/", {"body": "x" * 501})
        self.assertEqual(Note.objects.count(), count)

    def test_real_password_login_and_logout(self):
        # Fixed password exists only in a disposable test database.
        password = "Only-for-isolated-tests-472!"
        self.alice.set_password(password)
        self.alice.save()
        self.assertFalse(self.client.login(username="alice", password="wrong"))
        self.assertTrue(self.client.login(username="alice", password=password))
        self.assertEqual(self.client.get(self.detail).status_code, 200)
        self.client.post("/accounts/logout/")
        self.assertEqual(self.client.get(self.detail).status_code, 302)
~~~

## C. Execute and explain

From exercises/notes-app:

~~~powershell
.\.venv\Scripts\python.exe manage.py test notes
~~~

Expected baseline: 15 tests and OK. These tests do not contact a remote system. They demonstrate selected properties, not the security of every feature.

Most tests use the test client's default CSRF bypass to isolate authorization. The explicit CSRF test turns checks on and includes both successful and rejected writes. force_login sets up a known actor without testing the password path; the final test covers password login separately. The tests do not implement MFA or rate limiting.

Add one new negative test and explain its purpose. Save your actual output, date, Django version and any failures. Never paste an expected result as if you ran it.

[Week 10](../curriculum/WEEK-10.md)

