# 适用
适合理工科学术写作（数学、物理、计算机、生物等），双栏排版。

---

## 快速开始Quick Start

### 第一步：安装 Typst

打开终端，运行以下命令安装 Typst：

```bash
# macOS (推荐)
brew install typst

# 或手动下载（Apple Silicon M1/M2/M3）
# 从 https://github.com/typst/typst/releases 下载
# typst-aarch64-apple-darwin.tar.xz
# 解压后放入 /usr/local/bin/
```

验证安装成功：
```bash
typst --version
```

---

### 第二步：下载模版

将以下文件放到同一个文件夹（例如桌面的 `my-paper/`）：

```
my-paper/
├── main.typ           ← 你的论文（编辑这个）
├── oup-template.typ   ← 模版引擎（不要修改）
├── reference.bib      ← 你的参考文献
├── Fig/               ← 存放图片
│   ├── figure1.png
│   └── figure2.pdf
└── README.md
```

---

### 第三步：用 Cursor + Tinymist 实时预览

1. 用 **Cursor** 打开 `my-paper/` 文件夹：
   ```bash
   cd ~/Desktop/my-paper
   cursor .
   ```

2. 在 Cursor 中安装 **Tinymist** 插件：
   `Cmd + Shift + X` → 搜索 `Tinymist` → 安装

3. 打开 `main.typ`，点击顶部的 **Preview** 按钮，浏览器会弹出实时预览窗口。每次保存文件，预览页面自动更新。

4. 也可以用 AI 辅助写作：在 Cursor 中按 `Cmd + L`，用中文描述你要写的内容，AI 自动生成 Typst 代码。

---

### 编译为 PDF

```bash
cd ~/Desktop/my-paper
typst compile main.typ
open main.pdf
```

---

## 模版说明 / Template Info

### 关于本模版

本模版基于 OUP `oup-authoring-template.cls` v1.2 (2025) 转换而来，适用于：
- 理工科学术论文（数学、物理、CS、生物医学等）
- **不适合**：人文社科、无需双栏的轻量文档

---

### 文件结构

| 文件 | 说明 |
|------|------|
| `main.typ` | 你的论文主文件，写作内容在这里 |
| `oup-template.typ` | 模版引擎，控制排版格式，**不要修改** |
| `reference.bib` | BibTeX 格式参考文献库 |
| `Fig/` | 存放所有图片文件 |

---

### 关于 v1_modern 样式

在 `main.typ` 中设置 `style: "modern"` 启用 modern 样式。

**v1_modern 特别适合理科学习笔记**，例如：
- 数学公式推导笔记
- Python / 编程学习笔记
- 机器学习、信号处理等课程笔记

**右上角灰色占位符** 是预留的颜色标签区域，用来区分不同类型的笔记：

| 颜色 | 建议用途 |
|------|---------|
| 🔵 蓝色 | Python / 编程 |
| 🟢 绿色 | 数学 / 统计 |
| 🟠 橙色 | 物理 / 工程 |
| 🟣 紫色 | 机器学习 / AI |
| 🔴 红色 | 重要提醒 |

替换方法：在 `oup-template.typ` 中找到 `rect(width:45pt, height:55pt, fill:rgb("#cccccc"))` 改为你想要的颜色，例如蓝色：
```typst
rect(width:45pt, height:55pt, fill:rgb("#1a73e8"), stroke:none)
```

---

## 写作指南 Writing Guide

### 添加图片

将图片放入 `Fig/` 文件夹，然后替换占位符：

```typst
#figure(
  image("Fig/your-image.png", width: 100%),
  caption: [图片说明。],
) <fig-label>
```

跨全宽大图（出现在页面顶部）：
```typst
#figure(
  image("Fig/wide-image.png", width: 100%),
  caption: [跨全宽图片说明。],
  placement: top,
  scope: "parent",
) <fig-wide>
```

支持格式：`.png` `.jpg` `.svg` `.pdf`

---

### 引用文献

在 `reference.bib` 中添加条目，然后用 `@key` 引用：

```typst
如 @smith2023 所示，实验结果表明...
```

多篇引用：
```typst
参见 @lecun2015deep @krizhevsky2012imagenet @goodfellow2016deep。
```

---

### 数学公式

行内公式：
```typst
由此得 $E = m c^2$，其中 $m$ 为质量。
```

独立编号公式：
```typst
$ integral_0^infinity e^(-x^2) d x = sqrt(pi) / 2 $ <eq-label>
```

---

### 修改期刊样式

在 `main.typ` 顶部修改 `style` 参数：

```typst
style: "contemporary",   // OUP Contemporary（默认）
style: "modern",         // OUP Modern
style: "traditional",    // OUP Traditional（衬线字体）
```

---

### 修改参考文献格式

```typst
#bibliography("reference.bib", title: "References", style: "apa")
```

---

### 定理环境

```typst
#theorem(name: "定理名")[定理内容...]
#proposition[命题内容...]
#lemma[引理内容...]
#definition(name: "定义名")[定义内容...]
#proof[证明过程... □]
#example[例题内容...]
#remark[注记内容...]
```

---

### 算法块

```typst
#algorithm([Algorithm 1: 算法名称])[
  *Input:* 输入参数 \
  *Output:* 输出结果 \
  1. 步骤一 \
  2. 步骤二 \
  3. *return* 结果
]
```

---

## 常见问题 / FAQ

**Q: 编译报错 `unknown font family`？**
A: 安装 Liberation Sans 字体：`brew install --cask font-liberation`

**Q: 参考文献没有显示？**
A: 确认 `reference.bib` 在同一文件夹，且文件中有对应的 `@key`。

**Q: 图片不显示？**
A: 确认图片在 `Fig/` 文件夹内，路径大小写正确。

**Q: 如何让某个表格跨全宽？**
A: 在 `#figure(...)` 中添加 `placement: top, scope: "parent"`。

**Q: Tinymist 预览空白？**
A: 尝试无痕模式打开浏览器，或关闭广告拦截插件。

---

## 备注 Note

- 模版参考 [Oxford University Press](https://academic.oup.com) 官方 LaTeX 模版转换
- 排版引擎：[Typst](https://typst.app) v0.14+
- 编辑器推荐：[Cursor](https://cursor.sh) + [Tinymist](https://github.com/Myriad-Dreamin/tinymist)
