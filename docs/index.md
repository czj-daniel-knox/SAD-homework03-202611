# 我的技术文档

欢迎访问我的个人文档网站。本网站使用 MkDocs 构建，通过 GitHub Actions 自动部署到 GitHub Pages。

- 作者：czj-daniel-knox
- 实践主题：静态文档自动部署
- [关于本项目](about.md)
- [使用指南](guide.md)
- [API 参考](api.md)

## 这个网站是怎么来的

整个站点没有一行手写 HTML。`docs/` 目录里只有四个 Markdown 文件，Markdown 由 MkDocs Material 渲染成 `site/` 下的静态网页，再由 GitHub Pages 对外提供访问。每次我修改 Markdown 并推送到 `main` 分支，GitHub Actions 会自动完成"安装依赖 → 构建 → 上传产物 → 部署"这一串动作，几十秒后线上页面就更新了。

## 站点导航

| 页面 | 源文件 | 内容 |
| --- | --- | --- |
| 首页 | `docs/index.md` | 站点介绍与导航 |
| 关于 | `docs/about.md` | 项目目标、技术组成与原理 |
| 使用指南 | `docs/guide.md` | 写作流程与常用命令 |
| API 参考 | `docs/api.md` | 接口文档示例 |

## 实践体会

这次实践让我真正理解了"源码、构建产物、工作流、托管网站"这四层之间的关系：写文档的人只需要维护 `docs/`，`site/` 是可以随时丢弃再生的一次性产物，真正决定发布行为的是 `.github/workflows/deploy.yml` 里的那几十行 YAML。在没有自动化之前，改一个错别字都要重新构建、重新上传；现在只要 `git push`，剩下的交给 Actions。另外我也体会到"本地能跑通"和"CI 能跑通"不是一回事——本地漏掉的警告，到了 `--strict` 模式下会直接让构建失败，所以本地先跑一遍 `mkdocs build --strict` 是最省事的自检方式。
