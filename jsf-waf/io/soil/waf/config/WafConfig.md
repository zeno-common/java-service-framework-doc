# WafConfig

io.soil.waf.config

@Configuration @ComponentScan(basePackageClasses = {ProbeController.class})

WAF（Web Application Framework）配置类，配置 Jackson 序列化/反序列化规则和组件扫描。

主要配置：
- Java 8 时间格式的序列化/反序列化
- 枚举使用字符串序列化
- 忽略未知属性

---

## Methods

### Jackson2ObjectMapperBuilderCustomizer jackson2ObjectMapperBuilder()

@Bean

→**Jackson2ObjectMapperBuilderCustomizer** — 配置好的 Jackson2ObjectMapperBuilderCustomizer

配置 Jackson ObjectMapper 构建器，统一 JSON 序列化/反序列化规则
