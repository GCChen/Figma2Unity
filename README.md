# Figma2Unity

> **语言 / Language:** [中文](README.md) · [English](README_en.md)

把 Figma 顶层 Frame（页面层）导入为 Unity **uGUI Prefab**：保留层级、填充、文字、向量出图，并可选生成绑定脚本。

- **作者：** GCChen · **发布名：** Fllyt Studio  
- **商店：** [Asset Store](https://assetstore.unity.com/packages/slug/405028) · [短链](https://u3d.as/49C6)  
- **Unity**：2021.3+  
- **依赖**：`com.unity.ugui`（Unity UI）  
- **许可**：见包内 [`LICENSE`](LICENSE)

空白 Connection 与 Demo 见 **`Samples/`**。选项与排障见包内 **`Documentation/`**（各文档顶部可切换中英文）。

导入选项说明见 [Documentation/connection-options.md](Documentation/connection-options.md)。  
屏幕适配 / 布局：[figma-screen-fit.md](Documentation/figma-screen-fit.md)、[figma-layout-adapt.md](Documentation/figma-layout-adapt.md)。

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
| [`Documentation/figma-screen-fit.md`](Documentation/figma-screen-fit.md) | 居中 vs 拉满 |
| [`Documentation/figma-layout-adapt.md`](Documentation/figma-layout-adapt.md) | Auto Layout 适配 |
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
