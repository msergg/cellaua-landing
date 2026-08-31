# cellaua.com

Landing page for **Cella** — a shared family shopping list.

Hand-written HTML and CSS. No framework, no bundler, no dependencies, no build
step. The whole site is five files, and there is nothing between the commit and
what the browser receives.

## Files

| File | Purpose |
|---|---|
| `index.html` | The page |
| `style.css` | Tokens mirrored from the app's `lib/ui/core/tokens.dart` |
| `icon.svg` | The arch — the opening of a *cella*. Same geometry as the app icon |
| `_headers` | Security headers, applied by Cloudflare Pages |
| `robots.txt`, `sitemap.xml` | Indexing |

## Deploying

Cloudflare Pages watches this repository directly. Every push to `main`
publishes.

*Workers & Pages → Create → Pages → Connect to Git → `msergg/cellaua-landing`*

| Setting | Value |
|---|---|
| Framework preset | None |
| Build command | *(leave empty)* |
| Build output directory | `/` |
| Production branch | `main` |

There is deliberately no GitHub Actions workflow. It would need a
`CLOUDFLARE_API_TOKEN` and a `CLOUDFLARE_ACCOUNT_ID` as repository secrets, and
a token with the `workflow` scope to commit it — three credentials to publish
five static files that Cloudflare can already fetch by itself. If you ever do
want Actions instead, disconnect the Git integration first: two things
deploying one site is how they start disagreeing.

## Custom domain

Add `cellaua.com` in *Pages → your project → Custom domains*. Cloudflare issues
the certificate. If the domain is registered elsewhere, point its nameservers
at Cloudflare first.

## Editing the copy

Every claim on the page describes something the app actually does today. The
"Чесно про обмеження" section is deliberate: the app has real limits — a small
catalogue, no construction prices, no reminders on macOS — and a landing page
that hides them only moves the disappointment to after the download.
