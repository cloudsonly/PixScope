# PixScope

一个轻量、现代、纯前端的图片画廊浏览器。

输入一个可访问的 JSON URL，或直接粘贴 **GitHub 仓库目录链接**，即可把其中的图片以响应式画廊展示。无需后端、数据库或构建环境，打开网页即可使用。

[![Live Demo](https://img.shields.io/badge/Demo-GitHub%20Pages-4f46e5?style=flat-square)](https://cloudsonly.github.io/PixScope/)
[![License](https://img.shields.io/badge/license-MIT-22c55e?style=flat-square)](#许可证)

## ✨ 功能

- 🔗 **JSON URL 加载**：输入远程 JSON 地址即可读取数据。
- 📁 **GitHub 目录加载**：直接粘贴仓库目录链接，如 `https://github.com/owner/repo/tree/main/icons`，自动列出目录下所有图片（支持 png / jpg / gif / webp / avif / svg / bmp / ico）。
- 🧠 **智能识别图片**：递归识别 JSON 中的图片地址，支持常见对象、数组和嵌套结构。
- 🖼️ **响应式画廊**：自动适配桌面、平板和手机屏幕。
- 🖱️ **点击图片预览**：直接点击缩略图进入大图查看器，无需额外的预览按钮。
- 📐 **大图自动适应屏幕**：打开大图时按视口等比缩放，横图、竖图、超大图都不会溢出或被裁切。
- 🔍 **大图查看器**：支持上一张、下一张、放大、缩小、重置缩放、拖动平移和新窗口打开。
- 🔎 **实时搜索**：按图片名称、路径或图片 URL 快速过滤。
- 🗂️ **按目录筛选**：画廊右上角的目录下拉自动汇总数据里出现过的路径，可只看某个子目录；与搜索框叠加使用。
- 🚀 **分批渲染**：滚动到底部自动追加下一批卡片，上千甚至上万张图片也能秒开不卡顿。
- 📋 **复制图片地址**：一键复制图片 URL。
- 🕘 **访问历史**：自动保存最近访问过的地址。
- 🌙 **深浅主题**：右上角 `◐` 按钮在「跟随系统 / 浅色 / 深色」之间循环切换，首次点击即切换到相反的明暗主题，选择会保存在本机。
- ⬆️ **返回顶部**：页面右下角悬浮按钮，滚动超过一屏后出现，外圈进度环显示已浏览比例，点击平滑回到顶部。
- ⌨️ **键盘操作**：大图预览时可使用方向键和缩放快捷键。
- ⚡ **无需构建**：纯 HTML、CSS、JavaScript，无 npm、Node.js 或框架依赖。
- 🔒 **浏览器端处理**：项目没有后端服务，数据直接由浏览器请求目标地址。
- 📱 **移动端友好**：针对小屏幕进行了布局和交互适配。

## 🌐 在线使用

打开 PixScope：https://cloudsonly.github.io/PixScope/

支持三种输入，点击 **加载** 即可：

| 输入类型 | 示例 |
| --- | --- |
| JSON 文件 | `https://example.com/images.json` |
| GitHub 目录 | `https://github.com/owner/repo/tree/main/icons` |
| GitHub 单文件 | `https://github.com/owner/repo/blob/main/icons/a.svg` |

### GitHub 目录模式说明

- 目录链接会自动转成 GitHub API 请求，递归列出该目录（含子目录）下的图片文件。
- 图片地址使用 `raw.githubusercontent.com` 直链，因此需要目标仓库为 **公开仓库**。
- 未填写 Token 时，GitHub 接口限制 **60 次/小时（按 IP）**，公共网络下容易触发限流；展开输入框下方的「GitHub Token」填入只读 Token 后提升到 **5000 次/小时**。Token 仅保存在浏览器 `localStorage`，不会上传到任何服务器。
- 单个仓库最多展示 3000 张图片，超出部分会截断并提示。

### 按目录筛选

加载完成后，画廊右上角会出现目录下拉框：

- 选项来自当前数据里**实际包含图片**的目录（JSON 模式取图片 URL 的路径段，GitHub 模式取仓库内的相对路径），括号内是该目录的图片数量。
- 选中后只显示该目录（含子目录）下的图片，并可继续叠加搜索框缩小范围。
- 目录超过 200 个时只列前 200 个，其余可用搜索框输入路径片段过滤。

### 主题切换

右上角的 `◐` 按钮共有三种状态，依次点击循环：

| 图标 | 状态 | 行为 |
| --- | --- | --- |
| `◐` | 跟随系统 | 随系统明暗设置自动变化 |
| `☀` | 浅色 | 固定为浅色 |
| `☾` | 深色 | 固定为深色 |

首次点击会直接切到与当前画面相反的明暗主题，随后继续在浅色、深色、跟随系统之间循环。切换后按钮下方会短暂提示当前状态，设置保存在浏览器 `localStorage`，刷新页面后依然生效；浏览器地址栏 / 状态栏颜色也会随主题同步。

### 返回顶部

向下滚动超过约 320px 后，右下角会出现圆形返回顶部按钮：

- 外圈进度环表示当前页面已浏览的百分比，鼠标悬停时标题也会显示进度。
- 点击后平滑滚动回页面顶部，回到顶部自动隐藏。
- 小屏幕上按钮会自动缩小并靠右下方摆放，不遮挡内容。

## 🚀 部署

本项目是纯静态页面，不需要安装依赖或执行构建命令。

### GitHub Pages

1. 将仓库 Fork 到自己的 GitHub 账号，或直接使用本仓库。
2. 确认 `index.html` 位于仓库根目录。
3. 打开 `Settings → Pages`。
4. 在 **Build and deployment** 中选择 **Deploy from a branch**。
5. 选择 `main` 分支和 `/ (root)`。
6. 保存后等待 GitHub Pages 部署完成。

### 其他静态托管

直接将以下文件上传到网站根目录即可：

```text
PixScope/
├── index.html
└── README.md
```

支持：

- Cloudflare Pages
- Vercel
- Netlify
- Nginx / Apache
- GitHub Pages
- 任意静态文件服务器

## 📋 支持的 JSON 数据

项目不要求 JSON 使用固定结构，会递归查找常见的图片字段和容器字段。

### 字符串数组

```json
[
  "https://example.com/a.png",
  "https://example.com/b.jpg"
]
```

### 对象数组

```json
[
  {
    "name": "GitHub",
    "url": "https://example.com/github.png"
  },
  {
    "name": "Example",
    "url": "https://example.com/example.png"
  }
]
```

### 嵌套数据

```json
{
  "name": "My Images",
  "images": [
    { "name": "One", "url": "https://example.com/1.png" },
    { "name": "Two", "url": "https://example.com/2.png" }
  ]
}
```

也支持 `data`、`items`、`list`、`results`、`photos`、`icons`、`entries` 等常见容器字段，以及更深层的嵌套对象。

## 🖼️ 图片字段识别

对象中的以下字段会作为图片地址进行识别：

```text
url
imageUrl
src
image
icon
thumbnail
preview
cover
logo
```

图片名称会优先使用对象中的 `name` 或 `title`；如果没有名称，则根据图片 URL 自动生成名称。

重复的图片 URL 会自动去重。

## 🖱️ 图片预览

在图片画廊中：

- **直接点击图片**：打开大图预览。
- **打开即适应屏幕**：大图会按视口等比缩放，长边贴合屏幕，短边自动居中，不会出现只看到图片一角的情况。
- **双击图片**：在「适应屏幕」与「200%」之间切换。
- **放大后拖动**：按住鼠标或手指拖动可平移画面。
- **鼠标滚轮**：调整缩放比例。
- **上一张 / 下一张**：浏览其他图片。
- **复制地址**：复制当前图片 URL。
- **新窗口打开**：在浏览器新标签页打开原图。

缩略图采用等比例缩放方式显示，不会强制裁剪图片内容。

画廊采用分批渲染：首次加载 120 张，向下滚动时自动追加，搜索结果同样分批展示，因此上万条数据也不会一次性撑爆页面。

## ⌨️ 快捷键

大图预览状态下支持：

| 快捷键 | 功能 |
| --- | --- |
| `←` | 上一张 |
| `→` | 下一张 |
| `Esc` | 关闭预览 |
| `+` / `=` | 放大 |
| `-` | 缩小 |
| `0` | 恢复适应屏幕 |

鼠标滚轮也可以调整图片缩放比例，双击图片可在「适应屏幕 / 200%」之间切换。

## ⚠️ CORS 注意事项

由于项目完全运行在浏览器中，加载远程 JSON 时会受到浏览器的 **CORS（跨域资源共享）** 限制。

目标服务器需要允许当前网页发起跨域请求，例如返回：

```http
Access-Control-Allow-Origin: *
```

如果出现 `Failed to fetch`，即使将 JSON URL 直接粘贴到浏览器地址栏可以正常打开，也可能是目标服务器没有允许跨域请求。

### GitHub Raw

如果 JSON 文件存放在 GitHub 仓库中，可以使用 Raw 地址，例如：

```text
https://raw.githubusercontent.com/<user>/<repo>/main/images.json
```

## 🔐 隐私

PixScope 没有服务器端程序，也没有数据库或账号系统。

- JSON 请求由你的浏览器直接发送到输入的 URL。
- 本项目不会代替你上传 JSON 数据。
- 最近访问记录保存在浏览器的 `localStorage` 中。
- 主题设置保存在浏览器的 `localStorage` 中。
- 项目不要求登录。

需要注意的是，浏览器仍然会直接访问你输入的第三方 URL，因此具体的数据处理方式取决于目标服务器和浏览器环境。

## 🛠️ 技术栈

项目使用浏览器原生技术实现：

- HTML5
- CSS3
- Vanilla JavaScript
- Fetch API
- LocalStorage
- SVG

不依赖：

- React
- Vue
- Angular
- jQuery
- Bootstrap
- Tailwind CSS
- npm / pnpm / yarn
- Node.js
- 后端服务
- 数据库

## 📁 项目结构

```text
PixScope/
├── index.html   # 应用主体
└── README.md    # 项目说明
```

项目保持简单的单页面结构，适合个人使用、Fork 和静态部署。

## 📄 许可证

本项目采用 **MIT License**。
