# Ricardo Carvalho — Business Central Blog

Static site (Hugo + PaperMod) fed by the LinkedIn content pipeline.

## Writing locally

```bash
hugo server -D        # preview at http://localhost:1313
hugo                  # build to public/
```

## Deploy

Automatic: every push to `main` builds and deploys via GitHub Actions to GitHub Pages.

**Before the first deploy:** set your GitHub username in `hugo.toml`:

```toml
baseURL = "https://mrricardocarvalho.github.io/ricardo-carvalho-blog/"
```

Then: create this repo on GitHub, push, and enable Pages → Settings → Pages → Source: **GitHub Actions**.

When the custom domain arrives: point DNS at GitHub Pages, set the domain in Settings → Pages, and update `baseURL`.

## Content

Articles are generated from approved LinkedIn drafts by the content pipeline
(`scripts/blog_converter.py` in the linkedin-posts repo) or written directly
in `content/posts/*.md` with standard Hugo frontmatter.

- Body: the LinkedIn post, expanded for long-form reading
- Code from the Visual Note becomes real, copyable code blocks
- `Resources:` links (GitHub issues, Microsoft Learn) are kept — every claim has a source
- The AI Visual Prompt section is dropped (image material, not article material)
