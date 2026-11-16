# API 参考

以下接口仅用于文档展示，不提供真实服务。

## 查询文档列表

- 请求方法：GET
- 请求路径：/api/docs
- 功能：返回文档条目列表。

### 请求参数

| 参数 | 位置 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- | --- |
| page | query | integer | 否 | 页码，默认 1 |
| size | query | integer | 否 | 每页条数，默认 20，最大 100 |
| keyword | query | string | 否 | 按标题模糊匹配 |

### 返回示例

```json
{
  "items": [
    {"id": 1, "title": "使用指南"}
  ]
}
```

## 查询单个文档

- 请求方法：GET
- 请求路径：/api/docs/{id}
- 功能：按主键返回一个文档条目。

### 返回字段

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| id | integer | 文档主键 |
| title | string | 文档标题 |
| path | string | 对应 `docs/` 下的文件路径 |
| updated_at | string | 最近一次更新的时间，ISO 8601 格式 |

### 调用示例

```bash
curl -s https://example.com/api/docs/1
```

```python
import requests

resp = requests.get("https://example.com/api/docs/1", timeout=5)
resp.raise_for_status()
print(resp.json()["title"])
```

> 说明：示例中的域名 `example.com` 并不存在，本页所有接口都只用来练习文档写作，不会真正发起请求。

## 相关页面

- [返回首页](index.md)
- [关于本项目](about.md)
- [使用指南](guide.md)
