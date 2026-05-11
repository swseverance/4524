# Reproduction — DataDog browser-sdk issue #4524

Minimal reproduction for [DataDog/browser-sdk#4524](https://github.com/DataDog/browser-sdk/issues/4524): `@datadog/browser-rum` wrapping `fetch`/`XMLHttpRequest` causes Firestore WebChannel requests to fail on Safari with a CORS error.

**Deployed at:** https://repro4524.web.app

## Reproducing

Open both URLs in **Safari** (macOS or iOS). The bug does not affect Chrome or Firefox.

| URL | Expected |
|-----|----------|
| https://repro4524.web.app/without-rum.html | `{ "greeting": "hello world" }` — no console errors |
| https://repro4524.web.app/with-rum.html | `{ "greeting": "hello world" }` — but with CORS errors in the console |

On `with-rum.html` you should see one or more console errors along the lines of:

```
Fetch API cannot load https://firestore.googleapis.com/google.firestore.v1.Firestore/Listen/channel?...&TYPE=xmlhttp&... due to access control checks.
```

Firebase retries and eventually renders the document, but the CORS errors are real — in production these can cause degraded connectivity or hard failures depending on network conditions.

## Setup

```
firebase/12.13.0  (firebase-app-compat + firebase-firestore-compat)
@datadog/browser-rum  v6 (loaded from Datadog CDN)
```

Firestore security rules are read-only (`allow read: if true; allow write: if false`).
