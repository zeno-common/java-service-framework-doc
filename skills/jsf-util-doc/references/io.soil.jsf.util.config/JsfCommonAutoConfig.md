# JsfCommonAutoConfig

> JSF 通用模块自动配置类，扫描 io.soil.jsf.util 包下的组件

- **包**: io.soil.jsf.util.config
- **注解**: `@Configuration`, `@ComponentScan({"io.soil.jsf.util"})`

## 说明

引入 `jsf-util` 依赖后，Spring Boot 自动加载此配置类，扫描 `io.soil.jsf.util` 包下所有 `@Component`，包括：

- `ApplicationContextUtil` — Spring 上下文工具

无需手动配置。
