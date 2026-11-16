# 使用指南

## 日常写作流程

1. 修改 docs 目录中的 Markdown 文件。
2. 在本地预览并检查页面及链接。
3. 提交修改并推送到 main 分支。
4. 在 Actions 页面查看构建与部署状态。
5. 打开网站检查内容是否更新。

## 常用命令

```bash
# 创建并激活虚拟环境（Windows PowerShell）
python -m venv .venv
.\.venv\Scripts\Activate.ps1

# 安装依赖
python -m pip install -r requirements.txt

# 提交前自检：把警告当错误处理
python -m mkdocs build --strict

# 本地预览
python -m mkdocs serve
```

| 命令 | 作用 | 使用时机 |
| --- | --- | --- |
| `python -m mkdocs serve` | 启动本地预览，地址为 <http://127.0.0.1:8000/SAD-homework03-202611/>，保存后自动刷新 | 写作过程中 |
| `python -m mkdocs build --strict` | 构建输出到 `site/`，并把 warning 视为 error | 每次提交前 |
| `git status` | 确认暂存区里没有 `site/`、`.venv/` | 每次提交前 |
| `git diff --staged` | 推送前复核实际改动内容 | 每次提交前 |

## 两个容易忽略的细节

**路径写法。** `mkdocs.yml` 中 `nav` 的路径**相对于 `docs/` 目录**，写 `index.md` 而不是 `docs/index.md`；`site_url` 则必须是完整网址并且**带上仓库名结尾的斜杠**，否则生成的站内绝对链接可能指向错误位置。

**YAML 缩进。** 只能用空格，不能出现 Tab。缩进错了 MkDocs 会直接报配置解析错误，而 Actions 日志里只会显示构建步骤失败。

**本地预览的地址会带仓库名。** 因为 `site_url` 含有 `/SAD-homework03-202611/` 这段路径，`mkdocs serve` 会把站点挂在该子路径下：访问 `http://127.0.0.1:8000/` 会先 302 跳转到 `http://127.0.0.1:8000/SAD-homework03-202611/`。看到这个跳转说明配置与线上路径一致，属于正常现象，不是错误。

## 出问题时看哪里

| 现象 | 首先检查 |
| --- | --- |
| Actions 里 build 步骤红叉 | 展开日志，定位是依赖安装还是 `mkdocs build` 报错 |
| 构建成功但网页 404 | `Settings → Pages` 的 Source 是否为 `GitHub Actions`，是否已产生部署记录 |
| 网页内容没更新 | 强制刷新 / 无痕窗口排除缓存，确认本次推送确实改动了 `docs/**` |

## 相关页面

- [返回首页](index.md)
- [关于本项目](about.md)
- [API 参考](api.md)
