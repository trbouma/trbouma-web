# Tim Bouma · personal website

A small personal homepage built with MkDocs, Markdown, and a lightweight local theme. No external fonts, JavaScript, or analytics. The published project URL will be **https://trbouma.github.io/trbouma-web/**.

## Preview locally

Use Python 3.12 (the same version as CI) and Poetry 1.8.2. This follows the non-package Poetry setup used in the nearby repositories. Poetry creates an ignored `.venv/` inside this repository.

Use your existing `poetry` command; no upgrade or alternate executable is needed. For a fresh machine without Poetry, install version 1.8.2 using `pipx install poetry==1.8.2`.

From the repository root:

```sh
poetry env use python3.12
poetry install
poetry run mkdocs serve
```

Open http://127.0.0.1:8000/trbouma-web/ (or the address printed by MkDocs). Changes refresh automatically. Stop with Ctrl+C.

To check a production build:

```sh
poetry check --lock
poetry run mkdocs build --strict
```

The generated site is in `site/`, which is ignored by Git.

## Make it yours

- Edit `docs/index.md` for the homepage copy and public links. HTML comments mark places to expand; the starter makes no professional biography claims.
- Edit `docs/stylesheets/site.css` for colors, spacing, and typography.
- Edit `theme/main.html` for the shared header, navigation, and footer.
- Add Markdown pages under `docs/`, list them in `mkdocs.yml` under `nav`, and add links in the template or homepage as needed.
- Update `site_url` if you rename the repository or later use a custom domain. Its `/trbouma-web/` prefix is required for this project site.

Every file under `docs/` is published, including unlinked pages. Keep private notes and unfinished drafts elsewhere. Markdown comments can remain in generated HTML; keep those public-safe too.

## Enable GitHub Pages

The workflow is ready, but Pages must be enabled once by a repository administrator. At setup on 2026-10-12, the GitHub API reported `has_pages: false`; the Pages endpoint returned 404.

1. Open [Settings → Pages](https://github.com/trbouma/trbouma-web/settings/pages).
2. Under **Build and deployment → Source**, select **GitHub Actions**.
3. Commit and push these files to `main` when ready to publish. If already pushed before enabling Pages, run **Build and deploy MkDocs** manually from the Actions tab, or rerun the failed workflow.
4. Wait for both jobs to succeed. The deployment links to https://trbouma.github.io/trbouma-web/.

Pushes to `main` build and deploy. Pull requests targeting `main` run the strict build only. Manual runs deploy only from `main`. Deployment uses the `github-pages` environment; any environment protection rules must allow `main`. No personal access token, `gh-pages` branch, or `mkdocs gh-deploy` command is needed.

Only the deployment job receives Pages and OIDC write permissions. If it reports that the Pages site cannot be found, check the Source setting above. This local setup does not push changes or enable Pages automatically.

## Dependencies and maintenance

`pyproject.toml` declares the dependency and `poetry.lock` pins the complete dependency graph. CI uses Poetry 1.8.2 and installs from that lockfile. To update, change the constraint if needed, run `poetry update`, and run the checks above before committing both files. There is no separate requirements-file workflow.

The workflow uses the current official Actions major releases. Review release notes when updating them.

References: [MkDocs configuration](https://www.mkdocs.org/user-guide/configuration/) · [GitHub Pages custom workflows](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages).
