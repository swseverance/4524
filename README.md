# Reproduction — DataDog browser-sdk issue #4524

Minimal reproduction for [DataDog/browser-sdk#4524](https://github.com/DataDog/browser-sdk/issues/4524): Firestore WebChannel requests produce CORS errors in Safari when `@datadog/browser-rum` is active.

**Deployed at:** https://repro4524.web.app

## Reproducing

Open https://repro4524.web.app in **Safari** (macOS or iOS) and check the console. You may need to reload the page once or twice but eventually you should see one or more errors along the lines of:

```
Fetch API cannot load https://firestore.googleapis.com/google.firestore.v1.Firestore/Listen/channel?...&TYPE=xmlhttp&... due to access control checks.
```
