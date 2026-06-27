# JsfUrlParamConst

> JSF URL 参数常量类，定义 REST API 规约中分页、排序、偏移等 URL 参数名称

- **包**: io.soil.util.jdbc

## 常量

| 常量 | 类型 | 值 | 说明 |
|------|------|-----|------|
| `OFFSET_ID` | `String` | `"$offsetId"` | 大于 ID 的查询参数名，用于轮询 |
| `OFFSET_TIME` | `String` | `"$offsetTime"` | 大于时间的查询参数名，用于轮询 |
| `ORDER` | `String` | `"$order"` | 排序参数名，多列排序逗号分隔，如 `name asc,update_time desc` |
| `PAGE_NO` | `String` | `"$pageNo"` | 分页页码参数名 |
| `PAGE_SIZE` | `String` | `"$pageSize"` | 分页条目数参数名 |
| `OFFSET` | `String` | `"$offset"` | 偏移量参数名 |
| `LIMIT` | `String` | `"$limit"` | 偏移限制量参数名 |