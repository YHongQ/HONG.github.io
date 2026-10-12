source "https://rubygems.org"

# 与 GitHub Pages 构建环境保持一致：
# github-pages gem 内置 jekyll-remote-theme 及全部受支持插件
# （jekyll-paginate / jekyll-sitemap / jekyll-gist / jekyll-feed / jekyll-include-cache 等）。
# 本地开发请使用 `bundle exec jekyll serve`，不要直接运行 `jekyll serve`。
gem "github-pages", group: :jekyll_plugins

# Windows 平台时区数据（Git Actions 云端构建不需要，可保留）
platforms :windows, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

gem "wdm", "~> 0.1.0", :platforms => [:windows]
