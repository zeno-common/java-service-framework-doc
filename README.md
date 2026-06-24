# Introduction
依赖引入参考： '[jsf-bom/README.md](jsf-bom/README.md)'

---

# SDK Documentation Index
## 模块概览

| Module | ArtifactId | Description |
|--------|-----------|-------------|
| jsf-waf | jsf-waf | 基于 Spring Boot 封装的 Web 应用框架，提供异常处理、序列化配置、健康探针等功能 |

---

## 类索引

> 按模块→包分组，每个类附一行功能描述和文档链接。

### jsf-waf — 基于 Spring Boot 封装的 Web 应用框架

#### io.soil.waf.config — 配置类

| Class | Package | Description | Doc |
|-------|---------|-------------|-----|
| WafConfig | io.soil.waf.config | WAF配置类，配置 Jackson 序列化/反序列化规则和组件扫描 | [WafConfig](jsf-waf/io/soil/waf/config/WafConfig.md) |

#### io.soil.waf.exception — 异常处理

| Class | Package | Description | Doc |
|-------|---------|-------------|-----|
| WafException | io.soil.waf.exception | WAF 异常类，用于 Web 应用框架层的异常处理 | [WafException](jsf-waf/io/soil/waf/exception/WafException.md) |
| WafHttpExceptionResponse | io.soil.waf.exception | WAF 异常响应内容，用于封装异常信息返回给客户端 | [WafHttpExceptionResponse](jsf-waf/io/soil/waf/exception/WafHttpExceptionResponse.md) |
| WafHttpExceptionResolver | io.soil.waf.exception | WAF 全局异常处理器，自动捕获并处理 Web 层异常 | [WafHttpExceptionResolver](jsf-waf/io/soil/waf/exception/WafHttpExceptionResolver.md) |

#### io.soil.waf.handler — 序列化处理器

| Class | Package | Description | Doc |
|-------|---------|-------------|-----|
| BigNumSerializer | io.soil.waf.handler | 超出 JS 最大最小值处理 | [BigNumSerializer](jsf-waf/io/soil/waf/handler/BigNumSerializer.md) |

#### io.soil.waf.controller — 控制器

| Class | Package | Description | Doc |
|-------|---------|-------------|-----|
| ProbeController | io.soil.waf.controller | 健康探针控制器，提供应用活跃状态检测接口 | [ProbeController](jsf-waf/io/soil/waf/controller/ProbeController.md) |

#### io.soil.waf.util — 工具类

| Class | Package | Description | Doc |
|-------|---------|-------------|-----|
| RemoteAddrUtil | io.soil.waf.util | 远程地址工具类，用于获取客户端真实 IP 地址 | [RemoteAddrUtil](jsf-waf/io/soil/waf/util/RemoteAddrUtil.md) |

---

## 使用指南

AI Agent 在代码生成时遵循以下流程：

1. **需求匹配** — 根据功能需求从上方「类索引」中查找对应类
2. **查阅详情** — 点击 Doc 链接进入类的完整 API 文档，了解方法签名、参数和返回值
3. **引入依赖** — 从「Maven 依赖引入」复制对应 rtifactId 的依赖坐标到 pom.xml
4. **编写代码** — 根据文档中的方法签名和参数说明生成正确的调用代码

---
