---
name: "jsf-unit-test-doc"
description: "Use when coding with jsf-unit-test SDK, need API reference for YAML property loading in tests, or JUnit 5 / Mockito test dependencies."
---

# jsf-unit-test SDK 参考

JSF 单元测试工具模块，提供 YAML 配置加载、JUnit 5 和 Mockito 测试依赖传递。

## 依赖引入

Maven 工程的依赖引入参考：'[jsf-bom-doc/SKILL.md](../jsf-bom-doc/SKILL.md)'

| ArtifactId | 说明 |
|-----------|------|
| `jsf-unit-test` | 单元测试工具（test scope 引入） |

```xml
<dependency>
  <groupId>io.soil.jsf</groupId>
  <artifactId>jsf-unit-test</artifactId>
  <scope>test</scope>
</dependency>
```

引入 `jsf-unit-test` 后自动获得以下传递依赖（无需重复声明）：

| 依赖 | 说明 |
|------|------|
| `junit-jupiter` | JUnit 5 测试框架 |
| `mockito-core` | Mockito Mock 框架 |
| `spring-core` | Spring Core |
| `spring-beans` | Spring Beans |

## 类索引

### io.soil.jsf.test

| 类 | 说明 | 文档 |
|----|------|------|
| `YamlPropertySourceFactory` | YAML 配置文件加载工厂 | [YamlPropertySourceFactory](references/io.soil.jsf.test/YamlPropertySourceFactory.md) |