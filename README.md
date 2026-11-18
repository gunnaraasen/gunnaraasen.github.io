# gunnaraasen.com

Gunnar Aasen's personal site: a single page built with [Hugo](https://gohugo.io/)
and published to GitHub Pages at <https://gunnaraasen.com>. No theme; the
templates and stylesheet live in this repo.

## Edit

| To change              | Edit                                                     |
| ---------------------- | -------------------------------------------------------- |
| The bio                | `content/_index.md`                                      |
| Meta description       | `params.description` in `hugo.toml`                      |
| The "Writing" section  | `[params.blog]` in `hugo.toml` (delete it to hide)       |
| The "Elsewhere" links  | `[[params.links]]` in `hugo.toml`                        |
| Side projects          | `data/projects.yaml` (the section is hidden while empty) |
| Colors and type        | `assets/css/main.css`                                    |
| Page structure         | `layouts/home.html`, `layouts/baseof.html`               |
| `<head>` and metadata  | `layouts/_partials/head.html`                            |
| The 404 page           | `layouts/404.html`                                       |
| Favicon                | `static/favicon.svg`                                     |
| Crawler rules          | `layouts/robots.txt` (a template; adds the sitemap URL)  |

Each entry in `[[params.links]]` is also emitted as a `<link rel="me">` in the
page head, for profile verification.

### Adding a project

Replace the `[]` in `data/projects.yaml` with a list of entries. Only `name` is
required; entries render in file order.

```yaml
- name: Project name
  url: https://example.com/
  note: One sentence on what it is.
  year: 2026
```

## Preview

```sh
hugo server          # http://localhost:1313/
hugo --gc --minify   # production build into ./public
```

Built with Hugo 0.170.1; the standard edition is enough, since the site uses no
Sass or image processing. CI pins that version and its checksum in
`.github/workflows/deploy.yml`.

## Upgrading dependencies

Every build dependency is pinned in `.github/workflows/deploy.yml`:

- **Hugo**: bump `HUGO_VERSION` and replace `HUGO_SHA256` with the line for
  `hugo_<version>_linux-amd64.tar.gz` from that release's `checksums.txt`.
  Update the version above as well.
- **GitHub Actions**: each `uses:` names a full commit SHA, with its release
  tag in a comment. To upgrade, replace both:
  `gh api repos/actions/checkout/commits/<tag> -q .sha`.
- **Runner image**: `ubuntu-24.04`.

There are no other build dependencies (no theme, Hugo modules, npm, or
external scripts). The fonts are vendored in `static/fonts/`.

## Publish

Push to `main`. `.github/workflows/deploy.yml` builds the site and deploys it
to GitHub Pages in about a minute. Build output is not committed; `public/` is
gitignored.

One-time repository setup:

- **Settings → Pages → Build and deployment → Source**: GitHub Actions.
- **Settings → Pages → Custom domain**: `gunnaraasen.com`, with **Enforce
  HTTPS** on. `static/CNAME` holds the same domain.
- DNS for `gunnaraasen.com`: the four GitHub Pages A records (plus AAAA for
  IPv6), and a `www` CNAME pointing to `gunnaraasen.github.io`.

## Type

The typeface is [Newsreader](https://github.com/productiontype/Newsreader),
self-hosted as variable WOFF2 files in `static/fonts/` under the SIL Open Font
License (`static/fonts/OFL.txt`). Its palette and type are shared with
[turtlesdown.dev](https://turtlesdown.dev/).
