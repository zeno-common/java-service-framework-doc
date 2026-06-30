# YamlPropertySourceFactory

> YAML 配置文件加载工厂，使 `@PropertySource` 注解支持加载 `.yml` / `.yaml` 文件

- **包**: io.soil.jsf.test
- **实现**: `PropertySourceFactory`

## 使用场景

Spring 的 `@PropertySource` 注解默认只支持 `.properties` 文件。当需要在轻量级测试上下文中加载 YAML 配置时，通过 `factory` 属性指定此类即可。

> 注意：`@SpringBootTest` 原生支持 YAML，无需使用此类。仅在 `@ContextConfiguration` 等轻量级上下文中加载 YAML 时才需要。

## 方法

### createPropertySource

`PropertySource<?> createPropertySource(String name, EncodedResource encodedResource)`

> 将 YAML 资源解析为 `PropertiesPropertySource`

**参数**:
- `name` (`String`) — 属性源名称（可为 null）
- `encodedResource` (`EncodedResource`) — 编码资源

**返回**: `PropertySource<?>` — 解析后的属性源

**异常**: `IOException` — 读取资源失败

## 示例

```java
@ContextConfiguration(classes = {MyConfig.class})
@PropertySource(value = "classpath:test-config.yml", factory = YamlPropertySourceFactory.class)
class MyTest {

    @Value("${my.property}")
    private String myProperty;

    // ...
}
```

## 与其他加载方式的对比

| 方式 | YAML 支持 | 上下文重量 | 适用场景 |
|------|----------|-----------|---------|
| `@SpringBootTest` | 原生支持 | 重 | 集成测试 |
| `@TestPropertySource` + `.properties` | 不支持 | 重 | 简单属性覆盖 |
| `@ContextConfiguration` + `YamlPropertySourceFactory` | 支持 | 轻 | 不需要 Boot 特性的单元测试 |
| `@DynamicPropertySource` | N/A | 重 | 动态属性值 |