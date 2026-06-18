
---

# SDK Documentation Index
## 模块概览

| Module | ArtifactId | Description |
|--------|-----------|-------------|
| jsf-pojo | `jsf-pojo` | 通用 POJO/DTO 定义，含分页结果等基础数据结构 |
| jsf-util | `jsf-util` | 通用工具类集合，涵盖集合、日期、JSON、分页、树、Spring 上下文等 |

---

## 类索引

> 按模块 → 包分组，每个类附一行功能描述和文档链接。

### jsf-pojo — 通用 POJO/DTO

#### com.skylink.pojo.dto — 数据传输对象

| Class | Package | Description | Doc |
|-------|---------|-------------|-----|
| `PagedResult<T>` | `com.skylink.pojo.dto` | 分页结果响应体，含总数和列表 | [PagedResult](jsf-pojo/com.skylink.pojo.dto/PagedResult.md) |

### jsf-util — 通用工具类

#### io.soil.common.collection — 集合工具

| Class | Package | Description | Doc |
|-------|---------|-------------|-----|
| `CollectionUtil` | `io.soil.common.collection` | 集合转换、映射（toMap/mapList） | [CollectionUtil](jsf-util/io.soil.common.collection/CollectionUtil.md) |
| `FunctionWithParam<S,R,P>` | `io.soil.common.collection` | 带1个额外参数的函数式接口 | [FunctionWithParam](jsf-util/io.soil.common.collection/FunctionWithParam.md) |
| `FunctionWith2Param<S,R,P1,P2>` | `io.soil.common.collection` | 带2个额外参数的函数式接口 | [FunctionWith2Param](jsf-util/io.soil.common.collection/FunctionWith2Param.md) |
| `FunctionWith3Param<S,R,P1,P2,P3>` | `io.soil.common.collection` | 带3个额外参数的函数式接口 | [FunctionWith3Param](jsf-util/io.soil.common.collection/FunctionWith3Param.md) |

#### io.soil.common.constant — 常量/枚举

| Class | Package | Description | Doc |
|-------|---------|-------------|-----|
| `EnumSample` | `io.soil.common.constant` | 枚举定义参考事例 | [EnumSample](jsf-util/io.soil.common.constant/EnumSample.md) |

#### io.soil.common.date — 日期时间

| Class | Package | Description | Doc |
|-------|---------|-------------|-----|
| `DateTimeConst` | `io.soil.common.date` | 日期时间常量（系统时区偏移） | [DateTimeConst](jsf-util/io.soil.common.date/DateTimeConst.md) |
| `OffsetDateTimeUtil` | `io.soil.common.date` | 日期格式化/转换（ISO 8601） | [OffsetDateTimeUtil](jsf-util/io.soil.common.date/OffsetDateTimeUtil.md) |

#### io.soil.common.exception — 异常基类

| Class | Package | Description | Doc |
|-------|---------|-------------|-----|
| `BaseException` | `io.soil.common.exception` | 异常基类，含多种构造模板和异常栈获取 | [BaseException](jsf-util/io.soil.common.exception/BaseException.md) |
| `UnknownEnumException` | `io.soil.common.exception` | 未知枚举异常，状态值无匹配时抛出 | [UnknownEnumException](jsf-util/io.soil.common.exception/UnknownEnumException.md) |

#### io.soil.common.tree — 树结构

| Class | Package | Description | Doc |
|-------|---------|-------------|-----|
| `Node<ID,TYPE>` | `io.soil.common.tree` | 通用树节点，支持泛型ID和类型 | [Node](jsf-util/io.soil.common.tree/Node.md) |
| `TreeUtils` | `io.soil.common.tree` | 树/list/map 结构互转工具 | [TreeUtils](jsf-util/io.soil.common.tree/TreeUtils.md) |

#### io.soil.util.config — 自动配置

| Class | Package | Description | Doc |
|-------|---------|-------------|-----|
| `JsfCommonAutoConfig` | `io.soil.util.config` | Spring Boot 自动配置，扫描 `io.soil.util` 组件 | [JsfCommonAutoConfig](jsf-util/io.soil.util.config/JsfCommonAutoConfig.md) |

#### io.soil.util.ip — IP 工具

| Class | Package | Description | Doc |
|-------|---------|-------------|-----|
| `IpUtil` | `io.soil.util.ip` | 获取与指定远程IP端口连接的本地IP地址 | [IpUtil](jsf-util/io.soil.util.ip/IpUtil.md) |

#### io.soil.util.jdbc — JDBC 分页

| Class | Package | Description | Doc |
|-------|---------|-------------|-----|
| `JsfUrlParamConst` | `io.soil.util.jdbc` | REST API 分页/排序 URL 参数常量 | [JsfUrlParamConst](jsf-util/io.soil.util.jdbc/JsfUrlParamConst.md) |
| `JsfUrlParams` | `io.soil.util.jdbc` | 从 HTTP 请求提取分页、排序参数 | [JsfUrlParams](jsf-util/io.soil.util.jdbc/JsfUrlParams.md) |
| `JsfPagingUtil` | `io.soil.util.jdbc` | 基于 URL 参数的 PageHelper 分页工具 | [JsfPagingUtil](jsf-util/io.soil.util.jdbc/JsfPagingUtil.md) |
| `JsfUrlParamsPage<T>` | `io.soil.util.jdbc` | MyBatis-Flex 分页对象，继承 Page | [JsfUrlParamsPage](jsf-util/io.soil.util.jdbc/JsfUrlParamsPage.md) |

#### io.soil.util.json — JSON 工具

| Class | Package | Description | Doc |
|-------|---------|-------------|-----|
| `JsonMapper` | `io.soil.util.json` | Jackson 封装，对象/JSON 序列化反序列化 | [JsonMapper](jsf-util/io.soil.util.json/JsonMapper.md) |

#### io.soil.util.spring — Spring 工具

| Class | Package | Description | Doc |
|-------|---------|-------------|-----|
| `ApplicationContextUtil` | `io.soil.util.spring` | 非 Spring 管理类中获取 Bean | [ApplicationContextUtil](jsf-util/io.soil.util.spring/ApplicationContextUtil.md) |

---

## 使用指南

AI Agent 在代码生成时遵循以下流程：

1. **需求匹配** — 根据功能需求从上方「类索引」中查找对应类
2. **查阅详情** — 点击 Doc 链接进入类的完整 API 文档，了解方法签名、参数和返回值
3. **引入依赖** — 从「Maven 依赖引入」复制对应 `artifactId` 的依赖坐标到 `pom.xml`
4. **编写代码** — 根据文档中的方法签名和参数说明生成正确的调用代码

---