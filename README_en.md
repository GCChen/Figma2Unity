# Figma2Unity

> **Language / 语言:** [English](README_en.md) · [中文](README.md)

Import top-level Figma frames into Unity **uGUI Prefabs**: hierarchy, fills, text, rendered vectors, optional binding scripts.

- **Unity**: 2021.3+  
- **Dependency**: `com.unity.ugui` (Unity UI)  
- **License**: see [`LICENSE`](LICENSE)

Samples: **`Samples/`**. Options and troubleshooting: **`Documentation/`** (ships with the paid package; language switch at the top of each doc).

---

## What is implemented

### Structure

| Capability | Notes |
|------------|--------|
| **Page / Layer** | Top-level frames on a Page; tree → `RectTransform` |
| **Containers** | `FRAME` / `GROUP` / `SECTION` |
| **Components** | `COMPONENT` / `INSTANCE` rebuilt in-tree (not Unity Prefab variants) |
| **Visibility** | Visible Only / Invisible Only / All (Figma-hidden → inactive) |

### Visuals

| Capability | Notes |
|------------|--------|
| **Fills** | Solid, image fills (`Images/`), baked gradients (`Images/grad_*`) |
| **Layer opacity** | Figma Appearance **Opacity** → `CanvasGroup` (fades the subtree). Paint alpha stays on the color |
| **Corners / clip** | 9-slice approx; `clipsContent` → `RectMask2D` |
| **Shapes** | `RECTANGLE` / `ELLIPSE` / `LINE` (live or raster) |
| **Text** | Editable Text/TMP by default; gradient Fill does not auto-PNG (TMP vertex approx) |
| **Vectors / boolean** | `VECTOR` / `BOOLEAN_OPERATION` → `Renders/` |
| **Drop shadow** | First `DROP_SHADOW` ≈ uGUI `Shadow` when not rasterized |
| **1:1 raster** | Figma **Export** on any layer → PNG; or Force Export + visible Effect (TEXT also needs Effect Text As Image) |

### Layout & scroll

| Capability | Notes |
|------------|--------|
| **Auto Layout** | H / V / Grid → LayoutGroup (**Adaptive Figma**) |
| **Constraints** | Pin / center / stretch → anchors |
| **Hug reflow** | `SetActive(false)` on a child → siblings move, parent shrinks (opacity does not reflow) |
| **Stroke in layout** | `strokesIncludedInLayout` insets padding (stroke is not drawn) |
| **Tall-frame scroll** | `overflowDirection` or larger than Reference Resolution → ScrollRect; `root` = viewport |

### Scripts & controls

| Capability | Notes |
|------------|--------|
| **Binding scripts** | `UI_Xxx` with refs baked into the Prefab; optional name-prefix export |
| **Interactive controls** | Name-based Button / InputField / Toggle…; children wired by slots |
| **Style library** | Optional `Styles` asset (not required for Prefabs) |

FigJam whiteboard nodes (stickies, connectors, …) are **not imported**. There is no Connection toggle.

### Common Connection options

| Option | What it does |
|--------|----------------|
| **Visibility Filter** | Visible Only / Invisible Only / All (Figma-hidden → inactive) |
| **Screen Fit** | Center fixed Frame, or stretch root to fill the screen |
| **Layout Adapt** | **Adaptive Figma** (default) or **Snapshot** |
| **Tall Frame Scroll** | Auto ScrollRect when larger than Reference Resolution; `root` stays root |
| **Force Export Nodes With Effects** | Effect → PNG on flatten-safe nodes; containers with children not flattened |
| **Force Export Effect Text As Image** | Gates effect TEXT only; does not block shape PNG or Figma Export |
| **Use Text Mesh Pro** | TEXT → TMP when installed |
| **Generate Binding Scripts** | Emit `UI_Xxx`; optional **name-prefix** export |
| **Auto Interactive Controls** | Controls + slot wiring by layer name |
| **Import Published Styles** | Optional style-library asset |

Full options: [Documentation/connection-options_en.md](Documentation/connection-options_en.md).  
Screen & layout: [figma-screen-fit_en.md](Documentation/figma-screen-fit_en.md), [figma-layout-adapt_en.md](Documentation/figma-layout-adapt_en.md).

---

## Quick start

1. Put this folder under your project's `Assets/` (or install via Package Manager).
2. Create a Figma [Personal Access Token](https://www.figma.com/developers/api#access-tokens).
3. **Assets → Create → Figma2Unity → Connection Settings**, enter Token and file URL/key.  
   (Or copy `Samples/EmptyConnection/Connection_Empty.asset` and fill it in.)
4. **Refresh from Figma** → select layers → set ASCII **Mapped Name** → **Import Selected**.

Default output: `Assets/figma/prefabs/{MappedName}/`.

> Keep your Figma Token private.

Step-by-step import, binding scripts, and troubleshooting: **[Documentation/usage_en.md](Documentation/usage_en.md)**.

---

## Package layout

```
Figma2Unity/
├── Editor/          ← import window & pipeline
├── Runtime/         ← components on prefabs (keep in player builds if referenced)
├── Resources/       ← built-in sprites
├── Documentation/   ← guides
└── Samples/         ← Demo + Connection template
```

---

## More docs

| Doc | Content |
|-----|---------|
| [`Documentation/usage_en.md`](Documentation/usage_en.md) | **Install → import → binding scripts** |
| [`Documentation/connection-options_en.md`](Documentation/connection-options_en.md) | All Connection options |
| [`Documentation/style-library_en.md`](Documentation/style-library_en.md) | Style library (usually ignore) |
| [`Documentation/architecture_en.md`](Documentation/architecture_en.md) | Architecture |
| [`Documentation/figma-api-mapping_en.md`](Documentation/figma-api-mapping_en.md) | Nodes / paints → Unity |
| [`Documentation/figma-screen-fit_en.md`](Documentation/figma-screen-fit_en.md) | Center vs stretch |
| [`Documentation/figma-layout-adapt_en.md`](Documentation/figma-layout-adapt_en.md) | Auto Layout adapt |
| [`Documentation/figma-official-docs_en.md`](Documentation/figma-official-docs_en.md) | Figma link index |
| [`README.md`](README.md) | 中文总览 |

---

## Troubleshooting

| Symptom | Fix |
|---------|-----|
| 401 / 403 | Token or file access |
| Empty mapping table | Refresh from Figma |
| No Prefab | Tick layers and set Mapped Name |
| Script not attached | **Tools → Figma2Unity → Process Pending View Scripts** |
| Missing `UnityEngine.UI` | Install `com.unity.ugui` |

More: [usage_en.md](Documentation/usage_en.md).

---

## Rights & compliance

- You need a Figma Token and access to the target file.
- Imported design content remains yours or the original designer’s.
- Trademarks & API terms: `Third Party Notices.md`.
