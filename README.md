# minimal-csp

A minimal Content-Security-Policy to get started with.

```
Content-Security-Policy: default-src 'self'; form-action 'none'; frame-ancestors 'none'; upgrade-insecure-requests
```

# Explanation

Your website should be served via HTTPS anyway (or else what's the point of a CSP header that can be MITMed away or messed with by proxies?), so let's assume it is `https://www.example.com`.

| directive                 | result                                                                                                                                                                                                                                                                    |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| default-src 'self'        | JavaScript, CSS, images, videos, fonts, frames, objects (e.g. flash), Workers, AJAX, WebSockets are only allowed to be served from / communicate with `https://www.example.com`.                                                                                          |
| form-action 'none'        | No forms are allowed at all.                                                                                                                                                                                                                                              |
| frame-ancestors 'none'    | The page cannot be framed at all (like `X-Frame-Options: DENY`).                                                                                                                                                                                                          |
| upgrade-insecure-requests | If the page loads resources via HTTP (e.g. an image) it will be forced to HTTPS (the server will never receive an HTTP request and does not do a redirect). This only applies to resources that would be loaded from `http://www.example.com`, as all others are blocked. |

This is perfect for new projects. Add more policies as your site grows (e.g. allow images from a CDN).

# Report-only

For existing websites you can deploy it in report-only mode, so nothing breaks.

```
Content-Security-Policy-Report-Only: default-src 'self'; form-action 'none'; frame-ancestors 'none'; upgrade-insecure-requests
```

# Don't

Feel free to extend the CSP to match the needs of your website.

But:

* **do not** include `unsafe-inline` or `unsave-eval` (pls)
* **do not** allow [unsafe endpoints](https://research.google.com/pubs/pub45542.html) such as `*.googleapis.com`

if you do that you might as well not have a CSP.
