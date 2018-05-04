# minimal-csp

A minimal Content-Security-Policy to get started with.

```
Content-Security-Policy: default-src 'self'; form-action 'none'; frame-ancestors 'none'; upgrade-insecure-requests
```

Your website should be served via HTTPS anyway (or else what's the point of a CSP header that can be MITMed away?), so let's assume it is `https://www.example.com`.

| directive                 | result                                                                                                                                                                         |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| default-src 'self'        | JavaScript, CSS, images, videos, fonts, frames, objects (e.g. flash), Workers, AJAX, WebSockets are only allowedto be served from / communicate with `https://www.example.com` |
| form-action 'none'        | No forms are allowed at all                                                                                                                                                    |
| frame-ancestors 'none'    | The page cannot be framed at all (like `X-Frame-Options: DENY`)                                                                                                                |
| upgrade-insecure-requests | If the page loads resources via HTTP (e.g. an image) it will be forced to HTTPS (the server will never receive an HTTP request and does not do a redirect)                     |

\*

* prevent any forms

This is perfect for new projects. Add more policies as your site grows (e.g. allow images from a CDN).

For existing websites you can deploy it in report-only mode, so nothing breaks.

```
Content-Security-Policy-Report-Only: default-src 'self'; form-action 'none'; frame-ancestors 'none'; upgrade-insecure-requests
```
