# Setup

## 1. Create the profile repo
Create a public repo named exactly `nisarg-007`. GitHub renders its README on your profile.

## 2. Add files
```
nisarg-007/
├── README.md
├── .github/workflows/metrics.yml
└── .github/workflows/snake.yml
```

## 3. Token for the metrics cards
- GitHub → Settings → Developer settings → Personal access tokens → **Tokens (classic)**
- Scopes: `public_repo`, `read:user`
- Repo → Settings → Secrets and variables → Actions → New repository secret
- Name `METRICS_TOKEN`, value the token

## 4. Run both workflows once
Actions → "Generate Metrics" → Run workflow. Then "Generate Snake Animation" → Run workflow.

Metrics generates light and dark variants of all three cards. Both run on a schedule after this.

---

## Design notes

Every image is wrapped in `<picture>` with a `prefers-color-scheme` source, because
GitHub renders READMEs in both light and dark themes and a fixed-palette image
fails in one of them.

Measured contrast ratios (light canvas #ffffff / dark canvas #0d1117):

| Element | Light | Dark |
|---|---|---|
| Tagline `#6E6E73` (light) / `#8A8A8F` (dark) | 5.07:1 | 5.51:1 |
| Badge surface `#0071e3` | 4.70:1 | 4.03:1 |
| White label on `#0071e3` | 4.70:1 | 4.70:1 |

All clear the 4.5:1 body-text minimum. The previous `#1d1d1f` badges scored
**1.12:1** against the dark canvas — effectively invisible.

Every `<img>` carries an `alt` attribute. The typing header uses `repeat=false`
so the animation settles instead of looping forever.

If you skip step 3, delete the three `metrics/*` blocks from the Signals section.
