# Lab 09 — Review the app beyond its happy path

**Week:** 11. **Target:** local app only. **Time:** three sessions.

## A. Observe headers and cookies

Run the local app, sign in as a fake user and inspect a notes response. Record content-type, x-content-type-options, x-frame-options and referrer-policy if present. Inspect cookie attributes without copying cookie values. Inspect the rendered form for a CSRF input but do not publish its token.

Your local HTTP exercise does not enable Secure cookies because it has no HTTPS setup. This is a documented development exception, not a deployment recommendation. HTTPS deployments must use appropriate secure-cookie settings and validated TLS configuration.

## B. Add narrow audit events

At the top of notes/views.py add:

~~~python
import logging
logger = logging.getLogger("notes.audit")
~~~

Add this function and use it in place of each repeated ownership lookup (including the API's lookup). Leave the guest API check before it:

~~~python
from django.http import Http404

def owned_note(request, pk):
    try:
        return Note.objects.get(pk=pk, owner=request.user)
    except Note.DoesNotExist:
        logger.warning("note_access_denied actor=%s object=%s", request.user.pk, pk)
        raise Http404
~~~

The replacement line is `note = owned_note(request, pk)`.

Immediately after `form.save()` in note_edit, add:

~~~python
logger.info("note_updated actor=%s object=%s", request.user.pk, note.pk)
~~~

At the end of config/settings.py add:

~~~python
LOGGING = {
    "version": 1,
    "disable_existing_loggers": False,
    "handlers": {"console": {"class": "logging.StreamHandler"}},
    "loggers": {
        "notes.audit": {
            "handlers": ["console"],
            "level": "INFO",
            "propagate": False,
        },
    },
}
~~~

Trigger one allowed update and one Bob-to-Alice denial. Expected: action, synthetic actor ID and object ID in the terminal; no note body, password or session value. The development server also has its own request logs. This small logger does not record every event, provide durable storage or prevent tampering.

Re-run Lab 08 tests after changing the lookups. Add an assertLogs test if you want to verify this behavior automatically. Treat log confidentiality and retention as separate design requirements.

## C. Review deployment gaps

Run:

~~~powershell
.\.venv\Scripts\python.exe manage.py check --deploy
.\.venv\Scripts\python.exe -m pip list --outdated
~~~

The first command is expected to warn about this development configuration. The second checks package-index metadata and needs internet access; record an unavailable result honestly. Do not disable warnings simply to make a check green.

For each finding record: what it means, why it is present locally, the production change, and how you would verify it. Use the [Django checklist](https://docs.djangoproject.com/en/5.2/howto/deployment/checklist/). A deployment would require DEBUG=False, explicit hosts, external stable secrets, HTTPS and secure cookies, suitable application hosting, abuse controls, protected logs, backup/restore tests and dependency maintenance.

Do not enable forced HTTPS against this plain HTTP server. Do not add permissive hosts or trusted origins as a workaround for unrelated errors.

**Save:** a truthful “tested locally / planned for deployment” checklist and three remaining risks. [OWASP logging guidance](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html) covers the broader logging lifecycle.

[Week 11](../curriculum/WEEK-11.md)

