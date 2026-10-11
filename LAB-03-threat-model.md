# Lab 03 — Model the private-notes application

**Week:** 4. **Time:** two sessions plus review. **Tools:** Markdown or paper. **Target:** fictional notes app.

## Scenario

Alice and Bob each have private notes. Both can sign in and create, read, edit or delete their own notes. A support employee can help with account problems but has no routine reason to read note bodies. The public browser is not trusted to decide ownership.

## Steps

1. Copy [the threat-model template](../templates/THREAT-MODEL.md) into a new progress note.
2. Draw browser → application → database. Add session storage and label each flow: credentials, session ID, note body, query and result.
3. Mark what must remain confidential, what must remain unchanged without permission, and what must stay available.
4. Add five abuse cases. At least one must involve a legitimate signed-in user.
5. Assign controls to the browser, application or database. Explain why the assigned component can enforce them.
6. Give each control a test and an evidence location. Use “planned” until the test actually runs.

## Example to extend

| Threat | Effect | Control | Test |
|---|---|---|---|
| Bob supplies Alice's note ID | Private text is exposed | Query notes by both ID and verified owner | Bob gets no note body; Alice still receives her own note |
| A create request supplies a different owner | Records are misattributed | Owner comes from request.user, never form input | Supplied owner is ignored; saved owner is authenticated user |

Add your own rows for untrusted text, unwanted requests and session misuse. A threat is a plausible case; do not report it as a confirmed vulnerability without evidence.

## Expected result

A diagram plus at least five specific threat/control/test rows, each with priority and an owner. “Encrypt everything” is too broad to test. A useful statement identifies data, boundary and verification method.

**Check:** if you remove JavaScript from the page, which server controls should still work?

[Week 4](../curriculum/WEEK-04.md)

