# Lab 07 — Build a local website with private notes

**Weeks:** 8–9. **Target:** 127.0.0.1 only. **Prerequisites:** Python functions, HTTP, forms and ownership rules. **Time:** spread across both weeks.

You will build a small Django application with login and create/read/update/delete operations. Django supplies password hashing, sessions, form validation and CSRF support; your code enforces note ownership. This is a learning app without MFA, recovery email, abuse throttling or production deployment.

Framework references: [project setup](https://docs.djangoproject.com/en/5.2/intro/tutorial01/) and [authentication views](https://docs.djangoproject.com/en/5.2/topics/auth/default/). The lesson uses Django 5.2 with Python 3.12/3.13.

## 1. Create the project

In PowerShell, start from your learning repository folder. Use a fresh exercise directory:

~~~powershell
New-Item -ItemType Directory -Force exercises/notes-app
Set-Location exercises/notes-app
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install "Django>=5.2,<5.3"
.\.venv\Scripts\python.exe -m django startproject config .
.\.venv\Scripts\python.exe manage.py startapp notes
.\.venv\Scripts\python.exe -m pip freeze > requirements.txt
~~~

The dot after config means “this folder.” The virtual environment keeps dependencies here. Commit requirements.txt after reviewing it. Installations later can use `-m pip install -r requirements.txt`; review patch updates periodically.

## 2. Configure local settings

Edit `config/settings.py`. Add `"notes"` to the existing INSTALLED_APPS list. Keep the default middleware, SQLite configuration, password validators and template configuration.

Replace the generated SECRET_KEY assignment with this local-development setup. Remove the old literal key before committing:

~~~python
import os
from django.core.management.utils import get_random_secret_key

# Local learning only: without an environment key, restarting logs users out.
SECRET_KEY = os.environ.get("DJANGO_SECRET_KEY") or get_random_secret_key()
~~~

At the end of the file add:

~~~python
ALLOWED_HOSTS = ["127.0.0.1", "localhost"]
LOGIN_URL = "/accounts/login/"
LOGIN_REDIRECT_URL = "/"
LOGOUT_REDIRECT_URL = "/accounts/login/"
SESSION_COOKIE_HTTPONLY = True
SESSION_COOKIE_SAMESITE = "Lax"
~~~

Keep DEBUG=True only for this loopback development app. Production requires a durable external secret, HTTPS and further controls; Week 11 records those gaps. Do not commit .venv, db.sqlite3, .env or generated secrets.

## 3. Define records and form input

Replace `notes/models.py`:

~~~python
from django.conf import settings
from django.db import models

class Note(models.Model):
    owner = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    body = models.CharField(max_length=500)
~~~

Create `notes/forms.py`:

~~~python
from django import forms
from .models import Note

class NoteForm(forms.ModelForm):
    class Meta:
        model = Note
        fields = ["body"]
~~~

The browser edits body only. The server chooses owner.

## 4. Add views and URLs

Replace `notes/views.py`:

~~~python
from django.contrib.auth.decorators import login_required
from django.shortcuts import get_object_or_404, redirect, render
from django.views.decorators.http import require_http_methods, require_POST
from .forms import NoteForm
from .models import Note

@login_required
@require_http_methods(["GET", "POST"])
def note_list(request):
    form = NoteForm(request.POST if request.method == "POST" else None)
    if request.method == "POST" and form.is_valid():
        note = form.save(commit=False)
        note.owner = request.user
        note.save()
        return redirect("note-list")
    return render(request, "notes/list.html", {
        "notes": Note.objects.filter(owner=request.user).order_by("id"),
        "form": form,
    })

@login_required
@require_http_methods(["GET"])
def note_detail(request, pk):
    note = get_object_or_404(Note, pk=pk, owner=request.user)
    return render(request, "notes/detail.html", {"note": note})

@login_required
@require_http_methods(["GET", "POST"])
def note_edit(request, pk):
    note = get_object_or_404(Note, pk=pk, owner=request.user)
    form = NoteForm(request.POST if request.method == "POST" else None, instance=note)
    if request.method == "POST" and form.is_valid():
        form.save()
        return redirect("note-detail", pk=note.pk)
    return render(request, "notes/edit.html", {"form": form})

@login_required
@require_POST
def note_delete(request, pk):
    note = get_object_or_404(Note, pk=pk, owner=request.user)
    note.delete()
    return redirect("note-list")
~~~

Create `notes/urls.py`:

~~~python
from django.urls import path
from . import views

urlpatterns = [
    path("", views.note_list, name="note-list"),
    path("notes/<int:pk>/", views.note_detail, name="note-detail"),
    path("notes/<int:pk>/edit/", views.note_edit, name="note-edit"),
    path("notes/<int:pk>/delete/", views.note_delete, name="note-delete"),
]
~~~

Replace `config/urls.py`:

~~~python
from django.contrib.auth import views as auth_views
from django.urls import include, path

urlpatterns = [
    path("accounts/login/", auth_views.LoginView.as_view(), name="login"),
    path("accounts/logout/", auth_views.LogoutView.as_view(), name="logout"),
    path("", include("notes.urls")),
]
~~~

The routes expose only the features in this exercise. Read each ownership query out loud: “this ID AND this verified user.”

## 5. Add templates

Create the folders `notes/templates/notes/` and `notes/templates/registration/`.

Save `notes/templates/registration/login.html`:

~~~html
<!doctype html>
<html lang="en"><meta charset="utf-8"><title>Lab login</title>
<h1>Sign in to the local lab</h1>
<form method="post">
  {% csrf_token %}
  {{ form.as_p }}
  <input type="hidden" name="next" value="{{ next }}">
  <button>Sign in</button>
</form>
</html>
~~~

Save `notes/templates/notes/list.html`:

~~~html
<!doctype html>
<html lang="en"><meta charset="utf-8"><title>My notes</title>
<h1>My notes</h1>
<ul>
{% for note in notes %}
  <li><a href="{% url 'note-detail' note.pk %}">{{ note.body }}</a></li>
{% empty %}
  <li>No notes yet.</li>
{% endfor %}
</ul>
<form method="post">{% csrf_token %}{{ form.as_p }}<button>Create</button></form>
<form method="post" action="{% url 'logout' %}">{% csrf_token %}<button>Sign out</button></form>
</html>
~~~

Save `notes/templates/notes/detail.html`:

~~~html
<!doctype html>
<html lang="en"><meta charset="utf-8"><title>Private note</title>
<h1>Private note</h1>
<p>{{ note.body }}</p>
<a href="{% url 'note-edit' note.pk %}">Edit</a>
<form method="post" action="{% url 'note-delete' note.pk %}">
  {% csrf_token %}<button>Delete</button>
</form>
<a href="{% url 'note-list' %}">My notes</a>
</html>
~~~

Save `notes/templates/notes/edit.html`:

~~~html
<!doctype html>
<html lang="en"><meta charset="utf-8"><title>Edit note</title>
<h1>Edit my note</h1>
<form method="post">{% csrf_token %}{{ form.as_p }}<button>Save</button></form>
<a href="{% url 'note-list' %}">My notes</a>
</html>
~~~

Do not add the `safe` filter to note.body. It would bypass the escaping this demonstration relies on.

## 6. Create fake users and run

Run:

~~~powershell
.\.venv\Scripts\python.exe manage.py makemigrations notes
.\.venv\Scripts\python.exe manage.py migrate
~~~

Save `seed_users.py` beside manage.py:

~~~python
import os
from getpass import getpass
os.environ.setdefault("DJANGO_SETTINGS_MODULE", "config.settings")
import django
django.setup()
from django.contrib.auth import get_user_model
from django.contrib.auth.password_validation import validate_password

User = get_user_model()
for username in ("alice", "bob"):
    user, _ = User.objects.get_or_create(username=username)
    password = getpass("Choose a NEW local-only password for " + username + ": ")
    validate_password(password, user)
    user.set_password(password)
    user.save()
    print("Ready:", username)
~~~

Then run:

~~~powershell
.\.venv\Scripts\python.exe seed_users.py
.\.venv\Scripts\python.exe manage.py runserver 127.0.0.1:8000
~~~

Use new disposable passwords, not ones from a real account. The prompt hides input. If validation rejects a password, rerun the script and choose stronger local-only passwords. Open `http://127.0.0.1:8000/`. Sign in as Alice; create a note. Use a private browser window for Bob so sessions stay separate.

## 7. Check the result

| Action | Expected |
|---|---|
| Guest opens / | Redirect to login |
| Alice creates and edits her note | Saved; owner remains Alice |
| Bob requests Alice's detail/edit URL | 404, no note text |
| Bob submits deletion of Alice's note with his valid CSRF token | 404; note remains |
| Signed-in user sends GET to delete URL | 405; note remains |
| A form omits the CSRF token | 403; no write |
| Body contains <b>Private</b> | Rendered as text, not bold markup |
| Body is empty or over 500 characters | Form rejects it |

For browser-only manual checks, inspect URLs and forms; Lab 08 supplies automated POST tests. Record observed results separately from the expected table. Stop the server with Ctrl+C.

**Explain:** what would fail if the ownership filter were removed? What still remains unprotected before public deployment?

[Week 8](../curriculum/WEEK-08.md) · [Week 9](../curriculum/WEEK-09.md)

