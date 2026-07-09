# jagankumar-content

Structured JSON source of truth for Jagankumar's personal site. The site repo
([jagankumar-site](https://github.com/ejagankumar/jagankumar-site)) fetches these files at build time and
renders static HTML from them — this repo never gets touched by the rendering
logic, so you can edit your bio, projects, or experience by just editing JSON.

## Files

| File | Purpose |
|---|---|
| `data/profile.json` | Name, title, bio, contact links |
| `data/experience.json` | Work history, ordered most recent first |
| `data/projects.json` | Project case studies — each becomes its own indexable page |
| `data/skills.json` | Grouped skill tags shown on the homepage |
| `data/seo.json` | Site-wide title/description/keywords used for meta tags |

## Editing

1. Edit the relevant JSON file. Keep keys the same — the site expects this shape.
2. Commit and push to `main`.

Pushing to `main` automatically tells the site repo to rebuild and redeploy
(see `.github/workflows/notify-site.yml`) — no manual trigger needed once set up.

## One-time setup for auto-rebuild

1. In **jagankumar-site**, create a GitHub Personal Access Token with `repo` scope
   (Settings → Developer settings → Personal access tokens → Tokens (classic) → Generate new token).
2. In **this repo**, add it as a secret named `SITE_REPO_DISPATCH_TOKEN`
   (Settings → Secrets and variables → Actions → New repository secret).

After that, every push to this repo triggers a fresh build + deploy of the site.

## Schema notes

- `projects.json[].slug` must be URL-safe (lowercase, hyphenated) — it becomes
  the page path: `/projects/<slug>`.
- `experience.json` is rendered in array order — put current role first.
- Leave `links.repo` as `""` if a project has no public repo to link to.
