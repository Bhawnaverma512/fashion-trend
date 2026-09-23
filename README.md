# The Bridal Atelier

A static site for an Indian bridal couture house — collection, ceremony and
personality edits, a bridal style quiz, and a consultation request form.

## Running locally

```sh
npm start
```

Then open <http://localhost:5173>.

There is no build step and there are no dependencies to install. `npm start`
runs a small static file server ([`preview/serve.mjs`](preview/serve.mjs)) over
the `preview/` directory.

## Layout

| Path | Contents |
| --- | --- |
| `preview/index.html` | The entire site — markup, styles and rendering script, inline |
| `preview/img/` | Images the site renders |
| `preview/serve.mjs` | Static file server; honours `PORT`, defaults to 5173 |
| `public images/` | Source imagery, not referenced by the site |
| `vercel.json` | Deployment routing |

`preview/index.html` is self-contained: its only external requests are to
Google Fonts. Product cards are rendered client-side from an inline data table,
and image filenames are resolved through the `IMG` map near the top of the
script — a key with no entry falls back to `img/<key>.jpg`.

## Deploying

`vercel.json` routes all requests to `preview/serve.mjs`.

> **Note:** `serve.mjs` starts a long-running listener with
> `createServer(...).listen()`. Vercel's `@vercel/node` builder expects a module
> that exports a default `(req, res)` handler instead, so this needs adjusting
> before the deployment will serve correctly.

## Environment

The site itself needs no environment variables. `env` is git-ignored; keep any
Supabase credentials there or in your host's environment settings, never in a
committed file.
