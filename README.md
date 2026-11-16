# SAD-homework03-202611

实践项目 2：通过 GitHub Actions 自动部署 MkDocs 静态文档到 GitHub Pages。

## 网站与报告

- 网站地址：<https://czj-daniel-knox.github.io/SAD-homework03-202611/>
- [个人实验报告](report/README.md)

## 项目结构

```text
.
├── .github/workflows/deploy.yml   # 自动构建与部署工作流
├── docs/                          # 网站内容（唯一需要手写的部分）
│   ├── index.md
│   ├── about.md
│   ├── guide.md
│   └── api.md
├── report/                        # 个人实验报告与截图
├── mkdocs.yml                     # 站点配置（site_url、主题、导航）
├── requirements.txt               # 构建依赖
└── .gitignore
```

## 本地预览

```bash
python -m venv .venv
.\.venv\Scripts\Activate.ps1      # macOS / Linux 用 source .venv/bin/activate
python -m pip install -r requirements.txt
python -m mkdocs build --strict
python -m mkdocs serve
```

浏览器打开 <http://127.0.0.1:8000/SAD-homework03-202611/> 预览（`site_url` 带仓库路径，直接访问根路径会 302 跳到该地址）。

## 发布方式

推送到 `main` 分支且改动涉及 `docs/**`、`mkdocs.yml`、`requirements.txt` 或工作流文件时，GitHub Actions 会自动构建 `site/` 并发布到 GitHub Pages。仅修改 `report/` 或 `README.md` 不会触发部署。
