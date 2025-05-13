# Unity风格指南

### 关于文件结构、命名规范及其它事项

这些指南旨在帮助你的项目保持有序，使团队成员能快速找到所需资源。游戏开发周期长、项目体量大，有一套合理统一的规范，能避免后续大量麻烦。

请注意，每个团队或项目的需求、使用的软件可能不同。请将本指南作为基础，并根据团队实际需求做出适合自己的规范。每个项目都应该有自己的、易于查找的风格指南，确保团队成员都了解项目约定。

# 目录

- 资源命名
  - [文件夹](https://chat.q1.com/#folders)
  - [源码](https://chat.q1.com/#source-code)
  - [非代码资源](https://chat.q1.com/#non-code-assets)
- 目录/文件结构
  - [资源](https://chat.q1.com/#assets)
  - [脚本](https://chat.q1.com/#scripts)
  - [模型](https://chat.q1.com/#models)
- 工作流
  - [模型](https://chat.q1.com/#models)
  - [贴图](https://chat.q1.com/#textures)
  - [配置文件](https://chat.q1.com/#configuration-files)
  - [本地化](https://chat.q1.com/#localization)
  - [音频](https://chat.q1.com/#audio)
- [保持一致](https://chat.q1.com/#be-consistent)

# 资源命名

首先，文件或目录名**不允许有空格**。

## 文件夹

采用 `PascalCase`（大驼峰命名）。

优先使用更深的文件夹层级，而不是在资源名中堆砌过多信息。

目录名应尽量简短，推荐一到两个单词。若目录名过长，请合理拆分为子目录。

每个文件夹只放一种类型的文件。例如用 `Textures/Trees`、`Models/Trees`，而不是 `Trees/Textures`、`Trees/Models`。这样更易于设置美术等软件的根目录，比如Substance Painter可以固定保存到Textures目录。

如果项目里有多种环境或美术风格，使用资源类型作为父级目录：`Trees/Jungle`、`Trees/City`，不要用 `Jungle/Trees`、`City/Trees`，这样可以方便对比不同美术风格下的同类资源，方便风格统一。

### Debug文件夹

```
[PascalCase]
```

用方括号包裹，表示此文件夹仅用于非正式、非生产的调试资源。例如有 `[Assets]` 和 `Assets` 两个目录。

## 源代码

遵循所用编程语言的标准命名规范。C#和Shader文件都用 `PascalCase`。

## 非代码资源

命名时优先把大类放前面，例：用 `tree_small` 替代 `small_tree`。虽然后者更接近英语语序，但前者利于所有tree相关资源聚集在一起。

需要时可用 `camelCase`，例：`weapon_miniGun`（避免用 `weapon_gun_mini`）。如果计划同类型资源很多，命名字母顺序也要合理，比如 `vehicles_jet_fighter` 比 `vehicles_fighterJet` 更合适。

倾向用描述性后缀而非序号：`vehicle_truck_damaged` 比 `vehicle_truck_01` 好。如果一定要用数字后缀，保持2位数字；**不要**用序号做版本管理！请使用`git`等管理工具。

### 重要的/常驻的GameObject

用`_snake_case`，即前缀加下划线，让跨场景常驻对象更显眼。

### 调试对象

`[SNAKE_CASE]`
加方括号并大写，表示仅用于调试/测试，不会出现在正式包。

# 目录/文件结构

```
Root
+---Assets
+---Build
\---Tools    # 开发辅助工具：编译器、资源管理器等
```

## 资源

```
Assets
+---Art
|   +---Materials
|   +---Models     # FBX与BLEND文件
|   +---Textures   # PNG文件
+---Audio
|   +---Music
|   \---Sound      # 音效与采样
+---Code
|   +---Scripts    # C#脚本
|   \---Shaders    # Shader与节点
+---Docs           # Wiki、概念图、市场素材
+---Level          # Unity游戏设计相关内容
|   +---Prefabs
|   +---Scenes
|   \---UI
\---Resources      # 配置、本地化文本及其他用户文件
```

## 资源（可选结构）

```
Assets
+---Art
|   +---Materials
|   +---Models     # FBX与BLEND
|   +---Music
|   +---Prefabs
|   +---Sound      # 音效和采样
|   +---Textures
|   +---UI
+---Levels         # Unity场景文件
+---Src            # C#脚本和Shader
|   +---Framework
|   \---Shaders
```

## 脚本

命名空间建议和目录结构保持一致。

可以设立Framework文件夹专门放可复用代码。

Scripts内容可根据项目变化，但 `Environment`、`Framework`、`Tools`、`UI`结构应尽量保持一致。

```
Scripts
+---Environment
+---Framework
+---NPC
+---Player
+---Tools
\---UI
```

## 模型

建模源文件和导出可用模型分开存放。

```
Models
+---Blend
\---FBX
```

# 工作流

## 模型

文件格式：建议 `FBX`

虽然Unity原生支持Blender格式，但建议区分工作文件和已导出成品文件。使用Substance等贴图软件时也必须分区。

导出时保持 `Y轴向上`、`-Z为前`，尺度统一。

## 贴图

文件格式：`PNG`、`TIFF` 或 `HDR`

根据团队习惯和所用软件，选择 `高光/光泽` 或 `粗糙度/金属度` 流程。高光贴图如果使用RGB可额外支持彩色金属，除此之外两种流程效果差别不大。

### 贴图后缀

| 后缀名 |       贴图类型       |
| :----: | :------------------: |
| `_AL`  |   漫反射（Albedo）   |
| `_SP`  |   高光（Specular）   |
|  `_R`  | 粗糙度（Roughness）  |
| `_MT`  |  金属度（Metallic）  |
| `_GL`  |  光泽（Glossiness）  |
|  `_N`  |    法线（Normal）    |
|  `_H`  |    高度（Height）    |
| `_DP`  | 置换（Displacement） |
| `_EM`  |  自发光（Emission）  |
| `_AO`  |   环境光遮蔽（AO）   |
|  `_M`  |     遮罩（Mask）     |



### RGB遮罩贴图

尽量将黑白遮罩合成一张图，并用R/G/B分开不同通道。常用如下三张贴图：

```
texture_AL.png  # 漫反射
texture_N.png   # 法线
texture_M.png   # 遮罩
```

| 通道 |  高光/光泽  | 粗糙/金属 |
| :--: | :---------: | :-------: |
|  R   | Specularity | Roughness |
|  G   | Glossiness  | Metallic  |
|  B   |     AO      |    AO     |



> 特别说明：
>
> - 角色材质 blue(B)通道可用于*次表面散射参数*
> - 各向异性材质 blue(B)通道可放*各向异性方向贴图*

## 配置文件

推荐格式：`.INI`

解析简单，便于快速调优。

`XML`、`JSON`、`YAML`也都不错，选一种全项目保持一致。

涉及安全的内容、多人的参数，由服务器存放或使用二进制格式。

## 本地化

推荐格式：`.CSV`

主流本地化工具广泛支持，可以直接用表格编辑。

## 音频

混音时用`:WAV`，游戏中用`:OGG`。

小音效建议预加载到内存，大型音乐/不常用环境音则用异步加载。

# 保持一致

> 风格规范的意义，在于帮助团队统一代码与资源的表达方式，让大家关注“做什么”而不是“怎么写”。下面的规范是全局约束，但也要注意本地一致性。如果你新增的内容和周围代码风格差异很大，阅读时会很别扭，建议尽量避免。

—— [Google C++ 风格指南](https://google.github.io/styleguide/cppguide.html)