# cellaua.com

Landing page for **Cella** — a shared family shopping list.

Hand-written HTML and CSS. No framework, no bundler, no dependencies, no build
step. Nothing sits between the commit and what the browser receives.

## Layout

| Path | What |
|---|---|
| `wrangler.toml` | Deploy config. The only file at the root that is not the site |
| `public/` | Everything that gets served. The asset root |
| `public/index.html` | The live page — *Monolith*: dark, one statement per screen |
| `public/2/` … `public/5/` | Four alternate designs, kept for comparison |
| `public/404.html` | Served for unknown paths |
| `public/base.css` | Reset shared by all five. Each page owns the rest of its look |
| `public/icon.svg` | The arch — the opening of a *cella*. Same geometry as the app icon |
| `public/_headers` | Security headers. Applied by Cloudflare, never served itself |

The site lives in `public/` rather than at the repository root for one reason:
the asset directory is uploaded whole. Pointed at the root, Wrangler read 135
files instead of 17 — the extra ones were `.git`. `.assetsignore` did not
exclude them. A directory that contains only the site cannot leak anything that
is not the site.

The alternates carry `noindex` and are disallowed in `robots.txt`. They are
alternates, not content, and letting five near-identical pages into the index
would have them competing with each other.

To swap the live design, copy the chosen variant's `index.html` over
`public/index.html`, change its canonical to `https://cellaua.com/` and drop its
`noindex`.

## Deploying

Cloudflare Workers, static assets only — no server code. `wrangler.toml`
declares the asset directory and nothing else; there is no `main`, so no Worker
script ever runs.

```toml
[assets]
directory = "./public"
html_handling = "auto-trailing-slash"
not_found_handling = "404-page"
```

`auto-trailing-slash` makes `/2` redirect to `/2/`. `404-page` serves
`public/404.html` for unknown paths instead of an empty body.

### Continuous deployment

*Workers & Pages → Create → Workers → Import a repository →
`msergg/cellaua-landing`*

| Setting | Value |
|---|---|
| Build command | *(leave empty)* |
| Deploy command | `npx wrangler deploy` |
| Production branch | `main` |

Every push to `main` publishes.

### Deploying by hand

```
npx wrangler deploy
```

Check what would be uploaded before it is:

```
npx wrangler deploy --dry-run
```

It prints the file count. If that number is not the number of files in
`public/`, something is being picked up that should not be.

There is deliberately no GitHub Actions workflow. It would need a Cloudflare
API token stored as a repository secret and a GitHub token carrying the
`workflow` scope — two more credentials to publish a handful of static files
Cloudflare can fetch by itself. If you ever want Actions instead, disconnect
the Git integration first: two things deploying one site is how they start
disagreeing.

## Custom domain

*Workers & Pages → your Worker → Settings → Domains & Routes → Add custom
domain → `cellaua.com`*. Cloudflare issues the certificate. Add the domain to
your Cloudflare account first if it is registered elsewhere.

## Copy

English, and deliberately sparse. Every claim describes something the app does
today. There is no App Store badge because there is no listing yet.

A Ukrainian version is still missing, and matters: the app is Ukrainian and its
users shop at Сільпо and АТБ.
