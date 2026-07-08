---
name: "jsf-util-doc"
description: "Use when coding with jsf-util SDK, need API reference for URL paging, JSON mapping, date/time, tree structure, collection utils, IP lookup, Spring context, or exception base class."
---

# jsf-util SDK 参考

JSF 通用工具模块，提供 URL 分页、JSON 映射、日期时间、树结构、集合操作、IP 查询、Spring 上下文等工具类。

## 依赖引入

Maven 工程的依赖引入参考：'[jsf-bom-doc/SKILL.md](../jsf-bom-doc/SKILL.md)'

| ArtifactId | 说明 |
|-----------|------|
| `jsf-util` | 通用工具类 |

## 类索引

### io.soil.jsf.common.constant

| 类 | 说明 | 文档 |
|----|------|------|
| `EnumSample` | 枚举定义参考示例 | [EnumSample](references/io.soil.jsf.common.constant/EnumSample.md) |

### io.soil.jsf.common.exception

| 类 | 说明 | 文档 |
|----|------|------|
| `ExceptionType` | 异常类型枚举，对应 COLA 5 分层架构异常分类 | [ExceptionType](references/io.soil.jsf.common.exception/ExceptionType.md) |
| `BaseException` | 异常基类 | [BaseException](references/io.soil.jsf.common.exception/BaseException.md) |
| `BizException` | 业务异常，Domain/App 层业务规则违规时抛出（type = BIZ） | [BizException](references/io.soil.jsf.common.exception/BizException.md) |
| `SysException` | 系统异常，Infrastructure 层技术异常包装后抛出（type = SYS） | [SysException](references/io.soil.jsf.common.exception/SysException.md) |
| `ParamException` | 参数校验异常，Adapter 层入参校验失败时抛出（type = PARAM） | [ParamException](references/io.soil.jsf.common.exception/ParamException.md) |
| `UnknownEnumException` | 未知枚举类型异常 | [UnknownEnumException](references/io.soil.jsf.common.exception/UnknownEnumException.md) |

### io.soil.jsf.common.date

| 类 | 说明 | 文档 |
|----|------|------|
| `DateTimeConst` | 日期时间常量 | [DateTimeConst](references/io.soil.jsf.common.date/DateTimeConst.md) |
| `OffsetDateTimeUtil` | 日期时间格式化与转换 | [OffsetDateTimeUtil](references/io.soil.jsf.common.date/OffsetDateTimeUtil.md) |

### io.soil.jsf.common.tree

| 类 | 说明 | 文档 |
|----|------|------|
| `Node` | 通用树节点 | [Node](references/io.soil.jsf.common.tree/Node.md) |
| `TreeUtils` | 树结构转换工具 | [TreeUtils](references/io.soil.jsf.common.tree/TreeUtils.md) |

### io.soil.jsf.common.collection

| 类 | 说明 | 文档 |
|----|------|------|
| `CollectionUtil` | 集合转换与映射 | [CollectionUtil](references/io.soil.jsf.common.collection/CollectionUtil.md) |
| `FunctionWithParam` | 带一个额外参数的函数式接口 | [FunctionWithParam](references/io.soil.jsf.common.collection/FunctionWithParam.md) |
| `FunctionWith2Param` | 带两个额外参数的函数式接口 | [FunctionWith2Param](references/io.soil.jsf.common.collection/FunctionWith2Param.md) |
| `FunctionWith3Param` | 带三个额外参数的函数式接口 | [FunctionWith3Param](references/io.soil.jsf.common.collection/FunctionWith3Param.md) |

### io.soil.jsf.util.ip

| 类 | 说明 | 文档 |
|----|------|------|
| `IpUtil` | 本地 IP 工具 | [IpUtil](references/io.soil.jsf.util.ip/IpUtil.md) |

### io.soil.jsf.util.jdbc

| 类 | 说明 | 文档 |
|----|------|------|
| `JsfUrlParamConst` | URL 参数常量 | [JsfUrlParamConst](references/io.soil.jsf.util.jdbc/JsfUrlParamConst.md) |
| `JsfUrlParams` | URL 参数提取工具 | [JsfUrlParams](references/io.soil.jsf.util.jdbc/JsfUrlParams.md) |
| `JsfPagingUtil` | PageHelper 分页工具 | [JsfPagingUtil](references/io.soil.jsf.util.jdbc/JsfPagingUtil.md) |
| `JsfUrlParamsPage` | MyBatis-Flex 分页对象 | [JsfUrlParamsPage](references/io.soil.jsf.util.jdbc/JsfUrlParamsPage.md) |

### io.soil.jsf.util.json

| 类 | 说明 | 文档 |
|----|------|------|
| `JsonMapper` | JSON 序列化/反序列化工具 | [JsonMapper](references/io.soil.jsf.util.json/JsonMapper.md) |

### io.soil.jsf.util.spring

| 类 | 说明 | 文档 |
|----|------|------|
| `ApplicationContextUtil` | Spring 上下文工具 | [ApplicationContextUtil](references/io.soil.jsf.util.spring/ApplicationContextUtil.md) |

### io.soil.jsf.util.config

| 类 | 说明 | 文档 |
|----|------|------|
| `JsfCommonAutoConfig` | 自动配置类 | [JsfCommonAutoConfig](references/io.soil.jsf.util.config/JsfCommonAutoConfig.md) |
