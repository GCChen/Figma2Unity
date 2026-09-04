# Figma2Unity

> **Language / 语言:** [English](README_en.md) · [中文](README.md)

Import top-level Figma frames into Unity **uGUI Prefabs**: hierarchy, fills, text, rendered vectors, optional binding scripts.

- **Author:** GCChen · **Publisher label:** Fllyt Studio  
- **Store:** [Asset Store](https://assetstore.unity.com/packages/slug/405028) · [short link](https://u3d.as/49C6)  
- **Unity**: 2021.3+  
- **Dependency**: `com.unity.ugui` (Unity UI)  
- **License**: see [`LICENSE`](LICENSE)

Samples: **`Samples/`**. Options and troubleshooting: **`Documentation/`** (language switch at the top of each doc).

Connection options: [Documentation/connection-options_en.md](Documentation/connection-options_en.md).  
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
| [`Documentation/figma-screen-fit_en.md`](Documentation/figma-screen-fit_en.md) | Center vs stretch |
| [`Documentation/figma-layout-adapt_en.md`](Documentation/figma-layout-adapt_en.md) | Auto Layout adapt |
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
