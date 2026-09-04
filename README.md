# Figma2Unity

> **语言 / Language:** [中文](README.md) · [English](README_en.md)

把 Figma 顶层 Frame（页面层）导入为 Unity **uGUI Prefab**：保留层级、填充、文字、向量出图，并可选生成绑定脚本。

- **Unity**：2021.3+  
- **依赖**：`com.unity.ugui`（Unity UI）  
- **许可**：见包内 [`LICENSE`](LICENSE)

空白 Connection 与 Demo 见 **`Samples/`**。选项与排障见包内 **`Documentation/`**（仅随付费包提供；各文档顶部可切换中英文）。

---

## 已实现能力

### 结构

| 能力 | 说明 |
|------|------|
| **Page / Layer** | Page 下列顶层 Frame，勾选导入；层级 → `RectTransform` 树 |
| **容器** | `FRAME` / `GROUP` / `SECTION` |
| **组件** | `COMPONENT` / `INSTANCE` 按节点树重建（不是 Unity Prefab 变体） |
| **显隐** | Visible Only / Invisible Only / All（Figma 隐藏层 → 未激活） |

### 视觉

| 能力 | 说明 |
|------|------|
| **填充** | 纯色、图片填充（`Images/`）、渐变烘焙（`Images/grad_*`） |
| **图层透明度** | Figma Appearance **Opacity** → `CanvasGroup`（含子节点一起变淡）。填充自己的透明度仍在颜色上 |
| **圆角 / 裁切** | 圆角 9-slice 近似；`clipsContent` → `RectMask2D` |
| **形状** | `RECTANGLE` / `ELLIPSE` / `LINE`（实时重建或出图） |
| **文字** | 默认可编辑 Text / TMP；渐变 Fill 不自动出图（TMP 顶点色近似） |
| **向量 / 布尔** | `VECTOR` / `BOOLEAN_OPERATION` 等渲到 `Renders/` |
| **投影** | 未出图节点用 uGUI `Shadow` 近似第一层 `DROP_SHADOW` |
| **1:1 出图** | 任意层有 Figma **Export** → PNG；或 Force Export + 可见 Effect（文字另需 Effect Text As Image） |

### 布局与滚动

| 能力 | 说明 |
|------|------|
| **Auto Layout** | 水平 / 垂直 / Grid → LayoutGroup（**Adaptive Figma**） |
| **Constraints** | 贴边 / 居中 / 拉伸 → Anchor |
| **Hug 显隐重排** | 子节点 `SetActive(false)` 后兄弟靠拢、父级收缩（改透明度不会重排） |
| **描边计入布局** | `strokesIncludedInLayout` 时 padding 内缩（描边本身不画） |
| **长页滚动** | `overflowDirection` 或超出 Reference Resolution → ScrollRect；`root` 为视口 |

### 脚本与控件

| 能力 | 说明 |
|------|------|
| **绑定脚本** | 生成 `UI_Xxx`，引用写入 Prefab；可按名前缀只导出 |
| **交互控件** | 按图层名挂 Button / InputField / Toggle 等，子节点按槽位接线 |
| **样式库** | 可选生成 `Styles` 资源（建 Prefab 不依赖） |

FigJam 白板节点（便签、连线等）**不导入**，Connection 上无开关。

### Connection 常用选项

| 选项 | 作用 |
|------|------|
| **Visibility Filter** | Visible Only / Invisible Only / **All (Figma-hidden → inactive)** |
| **Screen Fit** | 居中固定 Frame，或根节点拉满屏幕 |
| **Layout Adapt** | **Adaptive Figma**（默认）或 **Snapshot** |
| **Tall Frame Scroll** | 超出 Reference Resolution 时自动 ScrollRect；`root` 始终为根 |
| **Force Export Nodes With Effects** | 可拍平节点的 Effect → 图；有子集的容器不整棵拍平 |
| **Force Export Effect Text As Image** | 仅约束特效字；不拦截形状，也不拦截 Figma Export |
| **Use Text Mesh Pro** | 开则 TEXT 用 TMP（需自行安装） |
| **Generate Binding Scripts** | 生成 `UI_Xxx`；可开**按名前缀**只导出指定节点 |
| **Auto Interactive Controls** | 按名挂交互控件 + 槽位接线 |
| **Import Published Styles** | 可选样式库 |

选项全文：[Documentation/connection-options.md](Documentation/connection-options.md)。  
屏幕 / 布局：[figma-screen-fit.md](Documentation/figma-screen-fit.md)、[figma-layout-adapt.md](Documentation/figma-layout-adapt.md)。

---

## 快速开始

1. 将本文件夹放入工程的 `Assets/`（或通过 Package Manager 安装）。
2. 在 Figma 创建 [Personal Access Token](https://www.figma.com/developers/api#access-tokens)。
3. **Assets → Create → Figma2Unity → Connection Settings**，填入 Token 与文件 URL/Key。  
   （也可复制 `Samples/EmptyConnection/Connection_Empty.asset` 再填写。）
4. 在 Connection 上 **Refresh from Figma** → 勾选 Layer → 填英文 **Mapped Name** → **Import Selected**。

默认输出：`Assets/figma/prefabs/{MappedName}/`。

> 请妥善保管 Figma Token，不要提交到公开仓库。

逐步说明、绑定脚本用法与排障见 **[Documentation/usage.md](Documentation/usage.md)**。

---

## 包内目录

```
Figma2Unity/
├── Editor/          ← 导入窗口与流水线
├── Runtime/         ← Prefab 上的组件（进游戏包需保留）
├── Resources/       ← 内置 Sprite
├── Documentation/   ← 详细说明
└── Samples/         ← Demo + Connection 模板
```

---

## 更多文档

| 文档 | 内容 |
|------|------|
| [`Documentation/usage.md`](Documentation/usage.md) | **安装 → 导入 → 绑定脚本** |
| [`Documentation/connection-options.md`](Documentation/connection-options.md) | Connection 全部选项 |
| [`Documentation/style-library.md`](Documentation/style-library.md) | 样式库（一般不必管） |
| [`Documentation/architecture.md`](Documentation/architecture.md) | 架构与流程图 |
| [`Documentation/figma-api-mapping.md`](Documentation/figma-api-mapping.md) | 节点 / Paint → Unity |
| [`Documentation/figma-screen-fit.md`](Documentation/figma-screen-fit.md) | 居中 vs 拉满 |
| [`Documentation/figma-layout-adapt.md`](Documentation/figma-layout-adapt.md) | Auto Layout 适配 |
| [`Documentation/figma-official-docs.md`](Documentation/figma-official-docs.md) | Figma 官网索引 |
| [`README_en.md`](README_en.md) | English overview |

---

## 常见问题

| 现象 | 处理 |
|------|------|
| 401 / 403 | Token 或文件权限 |
| 映射表空 | Refresh from Figma |
| 没生成 Prefab | 勾选 Layer，并填写 Mapped Name |
| 脚本没挂上 | **Tools → Figma2Unity → Process Pending View Scripts** |
| 缺 `UnityEngine.UI` | 安装 `com.unity.ugui` |

更多排障见 [usage.md](Documentation/usage.md)。

---

## 权限与合规

- 需自备 Figma Token，并对目标文件有访问权限。
- 导入的设计内容版权仍属于你或原设计师。
- 第三方商标与 API 条款见 `Third Party Notices.md`。
