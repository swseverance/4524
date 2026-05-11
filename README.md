# Reproduction — DataDog browser-sdk issue #4524

Minimal reproduction for [DataDog/browser-sdk#4524](https://github.com/DataDog/browser-sdk/issues/4524): Firestore WebChannel requests produce CORS errors in Safari when `@datadog/browser-rum` is active.

**Deployed at:** https://repro4524.web.app

## Reproducing

Open both URLs in **Safari** (macOS or iOS) and check the console. The bug does not affect Chrome or Firefox.

| URL | RUM |
|-----|-----|
| https://repro4524.web.app/with-rum.html | active |
| https://repro4524.web.app/without-rum.html | not loaded |

Both pages produce the same CORS errors, confirming the issue is not caused by DD RUM:

```
Fetch API cannot load https://firestore.googleapis.com/google.firestore.v1.Firestore/Listen/channel?...&TYPE=xmlhttp&... due to access control checks.
```
