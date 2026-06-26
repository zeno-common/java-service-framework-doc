# `WafConfig`

`package io.soil.waf.config`

`@Configuration` `@ComponentScan(basePackageClasses = {ProbeController.class})`

WAF（Web Application Framework）配置类，配置 Jackson 序列化/反序列化规则和组件扫描。

---

## Methods

### `Jackson2ObjectMapperBuilderCustomizer jackson2ObjectMapperBuilder()`

`@Bean`

→ **Jackson2ObjectMapperBuilderCustomizer** — 配置 Jackson ObjectMapper 构建器，统一 JSON 序列化/反序列化规则