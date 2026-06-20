# raghavchalapathy.ai

Personal profile website. Pure HTML + CSS, zero frameworks, hosted on GitHub Pages.

## Files
- `index.html` - all content/markup
- `style.css` - all styling (hand-rolled 12-col grid + timeline)
- `assets/` - profile photo and resources
- `CNAME` - custom domain (`raghavchalapathy.ai`)
- `.nojekyll` - disables Jekyll processing on GitHub Pages

## Local preview
```bash
python3 -m http.server 8000
# open http://localhost:8000
```

## Deploy
Push to the `main` branch of a GitHub repo, then enable
Settings -> Pages -> Deploy from branch -> `main` / root.
