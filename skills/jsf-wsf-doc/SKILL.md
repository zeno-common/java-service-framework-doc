---
name: "jsf-wsf-doc"
description: "Use when coding with jsf-wsf SDK, need API reference for WSF framework, exception handling, Jackson config, health probe, or client IP resolution."
---

# jsf-wsf SDK 参考

WSF（Web Service Framework）— 基于 Spring Boot 的 Web 应用框架，提供全局异常处理、Jackson 序列化配置、健康探针和工具类。

## 依赖引入
Maven 工程的依赖引入参考：'[jsf-bom-doc/SKILL.md](../jsf-bom-doc/SKILL.md)'

| ArtifactId | 说明 |
|-----------|------|
| `jsf-wsf` | Web 应用框架，含自动配置 |

## 类索引

| 类 | 包 | 说明 | 文档 |
|----|-----|------|------|
| `WsfConfig` | io.soil.jsf.wsf.config | Jackson 序列化/反序列化配置与组件扫描 | [WsfConfig](references/io.soil.jsf.wsf.config/WsfConfig.md) |
| `ProbeController` | io.soil.jsf.wsf.controller | 健康探针接口 | [ProbeController](references/io.soil.jsf.wsf.controller/ProbeController.md) |
| `WsfException` | io.soil.jsf.wsf.exception | WSF 异常，支持 HTTP 状态码和自定义错误码 | [WsfException](references/io.soil.jsf.wsf.exception/WsfException.md) |
| `WsfHttpExceptionResolver` | io.soil.jsf.wsf.exception | 全局异常处理器 | [WsfHttpExceptionResolver](references/io.soil.jsf.wsf.exception/WsfHttpExceptionResolver.md) |
| `WsfHttpExceptionResponse` | io.soil.jsf.wsf.exception | 异常响应 VO | [WsfHttpExceptionResponse](references/io.soil.jsf.wsf.exception/WsfHttpExceptionResponse.md) |
| `RemoteAddrUtil` | io.soil.jsf.wsf.util | 从代理头获取客户端真实 IP | [RemoteAddrUtil](references/io.soil.jsf.wsf.util/RemoteAddrUtil.md) |