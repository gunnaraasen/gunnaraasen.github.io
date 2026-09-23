---
# Template for a project entry. Copy this file, edit it, and remove `draft: true`.
title: "Example Project"
date: 2026-01-01
draft: true
params:
  year: 2026
  # Where the project lives. Either a path to a static project bundled in this
  # repo under static/projects/<name>/ ...
  link: "/projects/example-project/"
  # ... or an external URL, e.g. link: "https://example.com"
  #
  # Optional link to source code:
  repo: "https://github.com/gunnaraasen/example-project"
build:
  # This file supplies the listing entry only; it does not render its own page,
  # which leaves /projects/<name>/ free for the static project itself.
  list: always
  render: never
---

One or two sentences describing the project. This body is rendered inline on the
projects page, so keep it short.
