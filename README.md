[中文](README.zh.md) | English

# Hugo NexT theme starter

A bilingual example site and starting point for
[Hugo NexT](https://github.com/hugo-next/hugo-theme-next). It contains sample
content, menus, data, and configuration; the theme itself is pinned as a Git
submodule.

## Requirements

- Git
- Hugo **Extended 0.146.0 or newer**, as required by the pinned theme

The checked-in theme pointer currently corresponds to Hugo NexT v4.8.3.

## Clone with the theme

The submodule URL in `.gitmodules` uses SSH, so the shortest setup requires a
GitHub SSH key:

```bash
git clone --recurse-submodules https://github.com/iankingh/hugo-theme-next-starter.git
cd hugo-theme-next-starter
```

If the repository was cloned without submodules:

```bash
git submodule update --init --recursive
```

For an HTTPS-only checkout, override the submodule URL locally before
initializing it:

```bash
git config submodule.themes/hugo-theme-next.url https://github.com/hugo-next/hugo-theme-next.git
git submodule update --init --recursive
```

Do not run the preview script until `themes/hugo-theme-next/` is populated:
`startup.sh` reads the theme's `VERSION` file.

## Preview and build

```bash
# Preview at http://localhost:1414/
sh startup.sh

# Equivalent command without the banner
hugo server --port 1414

# Production build; output is written to public/
hugo --minify
```

`public/`, generated resources, and Hugo lock files are ignored by Git.

### Known configuration blocker

In the current checkout, `config/_default/menus.en-us.yaml` defines `parent`
twice for the `math` menu item. Hugo 0.164.0 rejects that duplicate YAML key,
so both preview and production builds stop while loading configuration. Remove
one of the identical `parent: example` lines in a site-maintenance change
before using the commands above.

## Customize the starter

- `config/_default/hugo.yaml`: base URL, title, language, output formats, and
  Markdown settings.
- `config/_default/languages.yaml`: Chinese and English language definitions.
- `config/_default/menus*.yaml`: language-specific navigation.
- `config/_default/params*.yaml`: NexT appearance and integration settings.
- `content/`: bilingual about, archives, links, and example posts.
- `data/flinks/`: language-specific friend-link data.
- `static/`: demo images, audio, and other files copied as-is.
- `themes/hugo-theme-next/`: the pinned upstream theme; do not copy site
  content into this directory.

At minimum, replace the sample `baseURL`, title, author metadata, menus,
content, and any enabled third-party integration settings before publishing.

## Deployment and automation

This repository has **no site build or GitHub Pages deployment workflow**.
Running `hugo --minify` produces a static `public/` directory that can be
published by the hosting service of your choice.

The only checked-in workflow, `.github/workflows/sync-2-gitee.yml`, runs when
this repository's `main` branch receives a push, then mirrors the hard-coded
upstream `hugo-next/hugo-theme-next-starter` source to its configured Gitee
repository. It requires the `GITEE_RSA_PRIVATE_KEY` secret and does not build
or deploy the example site. Forks should review or disable that workflow if
they do not own the configured mirror.

## Updating the theme

The submodule tracks the upstream theme's `main` branch:

```bash
git submodule update --remote themes/hugo-theme-next
hugo --minify
git add themes/hugo-theme-next
```

Review the theme release notes and generated site before committing the new
pointer.

## Related repositories

- `hugo-next/hugo-theme-next`: upstream theme used by this starter.
- `iankingh/blog`: a separate, customized site built with the same theme.
- `iankingh/iankingh.github.io`: a redirect to that blog.
- `iankingh/iankingh`: the GitHub profile README, not part of this build.

## License

See [LICENSE](LICENSE).
