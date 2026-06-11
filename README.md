# quest-2d-web

A **v0.app / Vercel 2D-web starter for the Meta Quest browser**. A modern
Next.js + shadcn/ui app that is dark, legible, comfortable, **installable as a
PWA**, and **multi-panel responsive** — no WebXR/3D dependencies.

> For immersive VR/AR, use the sibling [`quest-webxr-iwsdk`](https://github.com/axe-fb/quest-webxr-iwsdk)
> template (Vite + Meta's Immersive Web SDK).

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/axe-fb/quest-2d-web)

> Built on Next.js (App Router) · React 19 · TypeScript · Tailwind CSS v4 ·
> shadcn/ui (new-york).

---

## What you get

| Area | Included |
|---|---|
| **Design tokens** | Dark-first theme tuned to the Quest LCD (no pure black/white), generous radii, a `touch` spacing scale (48 / 56px), larger root font for VR legibility |
| **Multi-panel** | `PanelGroup` + `usePanelSize` reflow the layout live via `ResizeObserver`; `QuestPanel` fills the Horizon OS window edge-to-edge |
| **PWA** | `app/manifest.ts` (landscape, standalone, maskable icons), `public/sw.js` offline service worker, `/offline` fallback, generated icons |
| **Components** | shadcn/ui primitives (Button w/ Quest `xl`/`icon-touch` sizes, Card, Badge, Switch, Separator, ScrollArea) + theme toggle |
| **Registry** | `registry.json` so the Quest components install via the shadcn CLI and **Open in v0** |
| **Docs** | [`docs/QUEST_GUIDELINES.md`](docs/QUEST_GUIDELINES.md) — the full Quest web checklist with sources |

Routes: `/` landing · `/panels` multi-panel demo.

---

## Quick start

```bash
npm install
npm run icons      # generate PWA icons (zero deps; already committed)
npm run dev        # http://localhost:3000

# PWA install requires a secure context:
npm run dev:https  # https://localhost:3000
```

Then open the URL in the **Meta Quest browser**. For on-device debugging, use
`chrome://inspect#devices`.

---

## Project structure

```
app/
  layout.tsx        # metadata, viewport, theme provider, SW registration
  page.tsx          # landing (feature grid via PanelGroup)
  panels/page.tsx   # multi-panel responsive demo
  manifest.ts       # PWA manifest → /manifest.webmanifest
  offline/page.tsx  # offline fallback
  globals.css       # Tailwind v4 + Quest-tuned design tokens
components/
  ui/               # shadcn/ui primitives
  quest/            # QuestPanel, PanelGroup
  theme-provider.tsx, theme-toggle.tsx, register-sw.tsx, open-in-v0-button.tsx
hooks/              # usePanelSize
lib/                # utils (cn), quest (platform constants)
public/             # sw.js, icons/
scripts/            # generate-icons.mjs
registry.json       # shadcn / v0 registry
```

---

## Using the registry / Open in v0

```bash
npx shadcn@latest build      # outputs public/r/*.json
```

Once deployed, install a component into any shadcn project:

```bash
npx shadcn@latest add https://your-deploy.vercel.app/r/panel-group.json
```

…or wire up an **Open in v0** button (included as
`components/open-in-v0-button.tsx`):

```tsx
<OpenInV0Button url="https://your-deploy.vercel.app/r/quest-panel.json" />
```

> Note: the v0 "open" endpoint doesn't apply per-item `cssVars`/`css`/`envVars`,
> so this template keeps theme tokens in `app/globals.css`.

---

## Quest-specific notes

- **Hit targets:** use `size="xl"` / `size="icon-touch"` on Button, or the
  `min-h-touch` / `size-touch` utilities, to meet the 48px minimum.
- **Dark by default:** the theme is tuned for the Quest LCD — see the comments in
  `app/globals.css`.
- **Fluid layout:** assume your page is one resizable panel among several; the
  layout reflows from ~500px to 2000px wide.
- **Going further:** read [`docs/QUEST_GUIDELINES.md`](docs/QUEST_GUIDELINES.md)
  for layout, input, and PWA packaging (Bubblewrap → Meta Horizon Store) guidance.

---

## License

MIT — use it as a starting point for anything.
