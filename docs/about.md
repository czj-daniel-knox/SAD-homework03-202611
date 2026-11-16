# 关于本项目

## 项目目标

实现从 Markdown 文档到公开网站的自动化发布：写作用 Markdown，构建交给 MkDocs，发布交给 GitHub Actions，托管交给 GitHub Pages。

## 技术组成

| 工具 | 作用 |
| --- | --- |
| Markdown | 编写文档内容 |
| MkDocs Material | 将文档构建成静态网站 |
| GitHub Actions | 自动执行安装、构建和部署 |
| GitHub Pages | 托管并提供网站访问地址 |

## 从源码到网站的四层关系

| 层次 | 存放位置 | 是否提交到仓库 | 说明 |
| --- | --- | --- | --- |
| 源码 | `docs/`、`mkdocs.yml`、`requirements.txt` | 提交 | 唯一的"真源"，改内容只改这里 |
| 构建产物 | `site/` | 不提交（已被 `.gitignore` 忽略） | 由 `mkdocs build` 生成，可随时删除重建 |
| 工作流 | `.github/workflows/deploy.yml` | 提交 | 定义"什么时候按什么步骤构建与部署" |
| 托管网站 | GitHub Pages 服务器 | 不适用 | 读取 Actions 上传的产物对外提供访问 |

**为什么不能手工修改 `site/`：** 它每次构建都会被整体覆盖，手工改动下一次推送就丢失；它也不进版本库，别人 clone 下来根本没有这个目录。版本库里保存的应该只有源码和配置。

## 部署链路

下面的片段是本项目工作流的关键部分，说明"触发器"和"任务依赖"是怎么写的：

```yaml
on:
  push:
    branches: [main]
    paths:
      - 'docs/**'
      - 'mkdocs.yml'
      - 'requirements.txt'
      - '.github/workflows/deploy.yml'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v7
      - run: python -m mkdocs build --strict

  deploy:
    needs: build
    environment:
      name: github-pages
```

`needs: build` 表示部署必须等构建成功；`paths` 过滤则意味着只修改报告或 README 不会触发整条流水线。

## 相关页面

- [返回首页](index.md)
- [使用指南](guide.md)
- [API 参考](api.md)
