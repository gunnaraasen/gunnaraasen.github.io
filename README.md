# gunnaraasen.com

Personal site — a [Hugo](https://gohugo.io) static site published to GitHub
Pages at <https://gunnaraasen.com>.

## Local development

```sh
hugo server -D      # http://localhost:1313, -D includes drafts
hugo --gc --minify  # production build into ./public
```

Requires Hugo extended ≥ 0.146 (the version pinned in CI is in
`.github/workflows/deploy.yml`).

## Layout

```
content/_index.md              home page copy
content/projects/_index.md     projects page intro
content/projects/<name>.md     one listing entry per project
static/projects/<name>/        self-contained static projects
static/CNAME                   custom domain for GitHub Pages
layouts/                       templates (no external theme)
assets/css/main.css            all styling
```

## Editing the home page

Everything above the links row is the body of `content/_index.md`. The links
themselves — LinkedIn and GitHub — come from `[[params.links]]` in `hugo.toml`,
and are also rendered in the footer.

## Adding a project

Project entries are listing-only: each markdown file supplies a title, year,
blurb, and a link, but does not render a page of its own. That is what the
`build.render = never` block does, and it is what keeps the URL
`/projects/<name>/` free for a static project of the same name.

1. Copy `content/projects/example-project.md` to
   `content/projects/<name>.md`.
2. Fill in `title`, `date` (entries sort newest first), `params.year`,
   `params.link`, and an optional `params.repo`. Write the blurb in the body.
3. Delete `draft: true`.

`params.link` can be either an external URL or a path within this site.

### Hosting a static project here

Drop the project's files in `static/projects/<name>/` with an `index.html` at
its root. Hugo copies that tree verbatim, so it is served at
`https://gunnaraasen.com/projects/<name>/` — point the entry's `params.link` at
that path. These files bypass Hugo's pipeline entirely: plain HTML, CSS, and JS
only, with relative asset paths.

## Deployment

Every push to `main` triggers `.github/workflows/deploy.yml`, which builds with
Hugo and publishes via GitHub Pages. No build output is committed — `public/` is
gitignored.

One-time repository setup: **Settings → Pages → Build and deployment → Source**
must be set to **GitHub Actions**, and **Settings → Pages → Custom domain** to
`gunnaraasen.com` with **Enforce HTTPS** enabled. DNS for `gunnaraasen.com`
needs the four GitHub Pages A records (plus AAAA records for IPv6), and a CNAME
on `www` pointing to `gunnaraasen.github.io`.
