# CLAUDE.md

## 项目概述

这是一个基于 **Material for MkDocs** 搭建的个人网站，部署在 GitHub Pages。

- **站点名称**：Yessi的个人网站
- **线上地址**：https://yessi-zzz.github.io/
- **GitHub 用户**：Yessi-zzz

## 本地开发

```bash
# 激活虚拟环境
source .venv/bin/activate

# 本地预览（热重载）
mkdocs serve
```

本地预览地址：http://127.0.0.1:8000/

> 注意：`docs/Yessi/` 目录下的内容在本地对应 `/Yessi/` 子路径，编辑该目录时注意相对路径引用。

## 部署

推送到 `main` 分支后，GitHub Actions 自动触发部署：

```bash
git add .
git commit -m "update"
git push
```

CI 流程见 `.github/workflows/PublishMySite.yml`，使用 `mkdocs gh-deploy --force` 部署到 `gh-pages` 分支。

## 项目结构

```
mkdocs-site/
├── mkdocs.yml          # 站点配置（主题、导航、插件）
├── requirements.txt    # Python 依赖
├── docs/
│   ├── index.md        # 首页
│   ├── Yessi/          # "我" 导航栏下的个人介绍页
│   │   ├── index.md
│   │   ├── Desktop/    # 数码设备、穿搭等分类页
│   │   └── recipe.md
│   ├── notes/          # 笔记板块
│   │   └── codes/      # 算法代码
│   ├── DP/             # 动态规划笔记
│   ├── blog/           # 博客（含 RSS）
│   ├── stylesheets/
│   │   └── extra.css   # 自定义样式
│   ├── javascripts/
│   │   └── mathjax.js  # MathJax 配置
│   └── LXGWBright/     # 霞鹜文楷字体文件
└── .venv/              # Python 虚拟环境（不提交）
```

## 主题配置

- **主题**：Material，深色模式（slate）
- **主色**：orange，强调色：pink
- **字体**：霞鹜文楷（LXGWBright）

## 已启用插件

| 插件 | 用途 |
|------|------|
| `social` | 自动生成社交分享卡片 |
| `meta` | 支持页面级 meta 配置 |
| `blog` | 博客功能 |
| `tags` | 标签系统 |
| `search` | 全站搜索 |
| `rss` | 博客 RSS 订阅 |

## Markdown 扩展

- **arithmatex**：数学公式（MathJax / LaTeX 语法）
- **attr_list**：图像对齐等属性
- **md_in_html**：HTML 块内嵌 Markdown
- **pymdownx.blocks.caption**：图片标题

## 依赖管理

```bash
# 安装依赖
pip install -r requirements.txt

# 新增依赖后更新
pip freeze > requirements.txt
```

当前依赖：`mkdocs-material`、`mkdocs-rss-plugin`、`mkdocs-git-revision-date-localized-plugin`
