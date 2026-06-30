# ApplicationContextUtil

> Spring ApplicationContext 工具类，提供在非 Spring 管理的类中获取 Bean 的能力

- **包**: io.soil.jsf.util.spring
- **注解**: `@Component`
- **实现**: `ApplicationContextAware`

## 方法

### getBean (name)

`static <T> T getBean(String name)`

> 根据名称获取 Bean 实例

**参数**:
- `name` (`String`) — Bean 的注册名称

**返回**: `T` — 以所给名字注册的 Bean 实例

**异常**: `BeansException` — 获取失败

### getBean (class)

`static <T> T getBean(Class<T> clazz)`

> 根据类型获取 Bean 实例

**参数**:
- `clazz` (`Class<T>`) — Bean 的类型

**返回**: `T` — 对应类型的 Bean 实例

**异常**: `BeansException` — 获取失败

## 示例

```java
// 在非 Spring 管理的类中获取 Bean
UserService userService = ApplicationContextUtil.getBean(UserService.class);

// 按名称获取
Object bean = ApplicationContextUtil.getBean("myBean");
```