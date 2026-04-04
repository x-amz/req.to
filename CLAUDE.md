# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

req.to is a Universal Links domain for the Requiem iOS app (`HG8N27K4S4.dev.amz.req`). Its primary purpose is to deep-link into the app — or prompt installation if the app isn't installed. The site is intentionally minimal because it exists to serve the app, not to be a standalone product.

The web page decodes and displays content as a fallback for compatibility and graceful degradation, not as the primary experience.

## How the fallback works

`index.html` reads `window.location.hash`, splits on `.` to get base64url chunks, decodes each chunk, joins them with double newlines, and renders into a `<pre>`. Invalid input or missing hash shows a landing page or 404. The fragment format is: `#<base64url-chunk>.<base64url-chunk>...`

Base64url encoding: standard base64 with `+/` replaced by `-_`, padding stripped.

## Hosting & deployment

- Deployed via GitHub Pages — push to `main` to deploy
- Domain: `req.to` (set in `CNAME`)
- `.nojekyll` disables Jekyll processing
- `robots.txt` disallows all crawlers
- Apple Universal Links configured in `.well-known/apple-app-site-association` (app ID: `HG8N27K4S4.dev.amz.req`)

## Local development

```
python3 test-server.py
# http://localhost:8000
```

The test server (`test-server.py`, untracked) provides three experimental approaches for plain-text rendering: blob URL redirect, data URI redirect, and server-side decode. The production site only uses the fragment-based client-side approach.
