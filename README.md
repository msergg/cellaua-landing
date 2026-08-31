# cellaua.com

Landing page for **Cella** — a shared family shopping list.

Hand-written HTML and CSS. No framework, no bundler, no dependencies, no build
step. Nothing sits between the commit and what the browser receives.

## Layout

| Path | What |
|---|---|
| `/` | The live page — *Monolith*: dark, one statement per screen |
| `/2/` … `/5/` | Four alternate designs, kept for comparison |
| `base.css` | Reset shared by all five. Each page owns the rest of its look |
| `icon.svg` | The arch — the opening of a *cella*. Same geometry as the app icon |
| `_headers` | Security headers, applied by Cloudflare Pages |

The alternates carry `noindex` and are disallowed in `robots.txt`. They are
alternates, not content, and letting five near-identical pages into the index
would have them competing with each other.

To swap the live design, copy the chosen variant's `index.html` to the root,
change its canonical to `https://cellaua.com/` and drop its `noindex`.

## Deploying

Cloudflare Pages watches this repository. Every push to `main` publishes.

*Workers & Pages → Create → Pages → Connect to Git → `msergg/cellaua-landing`*

| Setting | Value |
|---|---|
| Framework preset | None |
| Build command | *(leave empty)* |
| Build output directory | `/` |
| Production branch | `main` |

There is deliberately no GitHub Actions workflow. It would need two Cloudflare
secrets and a token with the `workflow` scope — three credentials to publish a
handful of static files Cloudflare can fetch by itself. If you ever want
Actions instead, disconnect the Git integration first: two things deploying one
site is how they start disagreeing.

## Custom domain

*Pages → your project → Custom domains → `cellaua.com`*. Cloudflare issues the
certificate. Add the domain to your Cloudflare account first if it is
registered elsewhere.

## Copy

English, and deliberately sparse. Every claim describes something the app does
today. There is no App Store badge because there is no listing yet.

A Ukrainian version is still missing, and matters: the app is Ukrainian and its
users shop at Сільпо and АТБ.
