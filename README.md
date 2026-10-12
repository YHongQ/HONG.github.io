# yhongq.github.io

基于 **GitHub Pages + Jekyll Remote Theme（Minimal Mistakes）** 的个人博客。
主题以远程方式加载（`remote_theme`），仓库内不保存主题源码，升级主题只需改一行版本号。

## 目录结构

```
.
├── .github/workflows/pages-deploy.yml   # GitHub Actions 自动构建部署
├── Gemfile                              # github-pages gem（本地开发用）
├── _config.yml                          # 站点配置（全部配置都集中在这里）
├── _data/navigation.yml                 # 顶部导航菜单
├── index.html                           # 首页（文章卡片列表 + 分页）
├── _pages/                              # 静态页面（关于 / 归档 / 分类 / 标签 / 图片欣赏）
├── _posts/                              # 博客文章（YYYY-MM-DD-slug.md）
├── _gallery/                            # 图片欣赏集合（每张图一个文档）
└── assets/images/                       # 头像、文章配图（posts/）、画廊图（gallery/）
```

## 本地开发

```bash
bundle install
bundle exec jekyll serve   # http://127.0.0.1:4000
```

## 部署（GitHub Pages）

1. 每次 `git push origin main` 自动触发 `.github/workflows/pages-deploy.yml` 完成构建与发布（约 1 分钟）。
2. 仓库 **Settings → Pages → Build and deployment → Source** 应保持 **GitHub Actions**。

## 运维管理

| 场景 | 操作 |
| --- | --- |
| 升级主题 | 修改 `_config.yml` 中 `remote_theme: "mmistakes/minimal-mistakes@<新版本>"`，提交推送即可 |
| 换皮肤 | 修改 `_config.yml` 中 `minimal_mistakes_skin`（catppuccin_latte / dark / aqua / neon / plum 等 12 款） |
| 改导航 | 编辑 `_data/navigation.yml` |
| 改个人信息/社交链接 | 编辑 `_config.yml` 的 `author` 与 `footer` 段 |
| 发布文章 | 在 `_posts/` 下新建 `YYYY-MM-DD-slug.md`，front matter 含 `title / date / categories / tags / description` |
| 增加画廊图片 | 图片放入 `assets/images/gallery/`，在 `_gallery/` 新建文档并设置 `header.teaser` |
| 接入评论 | `_config.yml` 的 `comments.provider` 填 `giscus` / `utterances` / `disqus` 并补齐参数 |
| 接入统计 | `_config.yml` 的 `analytics` 段（google / goatcounter / umami / matomo / cloudflare / fathom） |

## 内容迁移说明（Firefly → 本站）

- **文章**：18 篇已迁移（CANN 系列 5 篇 + C++/Java 技术笔记 13 篇），统一了分类（`技术博客` / `学习笔记`），
  修正了标签错误（中文逗号粘连、C/C++ 错标、句子式标签），补全了缺失的摘要，修复了旧站外链。
  Firefly 自带的主题演示文章与一篇草稿（`huawei-tiling-design.md`，draft 标记）未发布。
- **图片**：文章配图 532 张已统一压缩为 WebP（最长边 1000px），**125.3 MB → 11.4 MB**；
  画廊精选 12 张（最长边 1600px，1.6 MB）。新增图片请沿用相同压缩规格，控制仓库体积。
- **图片欣赏**：`/gallery/` 栏目使用 Minimal Mistakes 的 collection + grid 布局，点击图片可查看大图。
- **未迁移的 Firefly 特性**（按需后续处理）：公告栏、音乐播放器、看板娘、樱花特效、番组计划页、
  Microsoft Clarity 统计、网页 favicon 图标（已按要求移除）。
