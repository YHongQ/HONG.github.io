# HONG.github.io

基于 **GitHub Pages + Jekyll Remote Theme（Minimal Mistakes）** 的个人博客运维方案。
主题以远程方式加载（`remote_theme`），仓库内不保存主题源码，升级主题只需改一行版本号。

## 目录结构

```
.
├── .github/workflows/pages-deploy.yml   # GitHub Actions 自动构建部署
├── Gemfile                              # github-pages gem（与 Pages 构建环境一致）
├── _config.yml                          # 站点配置（Firefly 迁移后的全部配置都在这里）
├── _data/navigation.yml                 # 顶部导航菜单
├── _includes/head/custom.html           # 自定义 <head>（favicon）
├── index.html                           # 首页（文章卡片列表 + 分页）
├── _pages/                              # 静态页面（关于 / 归档 / 分类 / 标签）
├── _posts/                              # 博客文章（当前为空，后续按需迁移）
└── assets/images/                       # 头像 avatar.jpg、favicon.png
```

## 本地开发

```bash
# 1. 安装依赖（需要 Ruby >= 3.1 与 Bundler）
bundle install

# 2. 本地预览（默认 http://127.0.0.1:4000）
bundle exec jekyll serve

# 3. 本地构建检查
bundle exec jekyll build
```

> 请始终使用 `bundle exec jekyll ...`，确保本地环境与 GitHub Pages 一致。

## 部署（GitHub Pages）

1. 首次推送后，进入仓库 **Settings → Pages → Build and deployment → Source**，选择 **GitHub Actions**。
2. 之后每次 `git push origin main` 都会自动触发 `.github/workflows/pages-deploy.yml` 完成构建与发布。
3. 在 **Settings → Pages** 中确认 Custom domain（如使用自定义域名）与 **Enforce HTTPS**。

## 运维管理

| 场景 | 操作 |
| --- | --- |
| 升级主题 | 修改 `_config.yml` 中 `remote_theme: "mmistakes/minimal-mistakes@<新版本>"`，提交推送即可（版本标签见主题仓库 Tags 页） |
| 换皮肤 | 修改 `_config.yml` 中 `minimal_mistakes_skin`（default/air/aqua/contrast/dark/dirt/neon/mint/plum/sunrise） |
| 改导航 | 编辑 `_data/navigation.yml` |
| 改个人信息/社交链接 | 编辑 `_config.yml` 的 `author` 与 `footer` 段 |
| 发布文章 | 在 `_posts/` 下新建 `YYYY-MM-DD-标题.md`，front matter 见主题文档 |
| 接入评论 | `_config.yml` 的 `comments.provider` 填 `giscus` / `utterances` / `disqus` 并补齐对应参数 |
| 接入统计 | `_config.yml` 的 `analytics` 段（google / goatcounter / umami / matomo / cloudflare / fathom） |

## Firefly → Minimal Mistakes 配置迁移对照

| Firefly 配置 | 本仓库配置 |
| --- | --- |
| `siteConfig.title = 溄` | `title: "溄"` |
| `siteConfig.subtitle = HONG` | `subtitle: "HONG"` |
| `siteConfig.description` | `description` |
| `siteConfig.lang = zh_CN` | `locale: "zh-CN"` |
| `siteConfig.timezone` | `timezone: "Asia/Shanghai"` |
| `siteConfig.themeColor.hue = 220` | `minimal_mistakes_skin: "default"`（蓝灰调，最接近） |
| `profileConfig.avatar` | `author.avatar` → `assets/images/avatar.jpg` |
| `profileConfig.name / bio` | `author.name` / `author.bio` |
| `profileConfig.links`（QQ/Email/GitHub） | `author.links` + `footer.links` |
| `navbar.links`（主页/归档/友链/留言板/我的/关于/链接） | `_data/navigation.yml`（首页/归档/分类/标签/关于；友链等后续补充） |
| `postListLayout` + `pagination.postsPerPage = 10` | `paginate: 10`（首页卡片列表） |
| `navBarSearchConfig`（PageFind） | `search: true` + `search_provider: "lunr"` |
| 分类 / 标签页 | `_pages/category-archive.md` / `_pages/tag-archive.md` |
| `about` 页内容 | `_pages/about.md`（含建站日期、联系方式） |
| favicon `/favicon/cat.png` | `assets/images/favicon.png` + `_includes/head/custom.html` |
| `commentConfig`（Twikoo） | `comments.provider`（暂留空，后续接入 giscus 等） |

暂未迁移的 Firefly 特性（待后续博客内容迁移时按需处理）：公告栏、音乐播放器、
看板娘、樱花特效、相册/番组计划页、Microsoft Clarity 统计、RSS 图标入口
（主题已内置 Atom Feed，地址 `/feed.xml`）。

## 注意事项

- `_config.yml` 中 `url` 默认为 `https://yhongq.github.io`，请确认与你的 GitHub 用户名一致，
  否则会导致样式/资源 404。
- 本方案不依赖 `github-pages` 之外的白名单外插件，可直接使用 GitHub Pages 原生构建能力。
- 文章图片统一放 `assets/images/`，正文用 `/assets/images/xxx.png` 引用。
