# JsonMapper

> JSON 映射工具类，封装 Jackson ObjectMapper 提供对象与 JSON 之间的序列化/反序列化操作

- **包**: io.soil.util.json
- **修饰**: `final`（不可继承）
- **Lombok**: `@Slf4j`

## 内置配置

| 配置项 | 值 | 说明 |
|--------|-----|------|
| 时间模块 | `JavaTimeModule` | Java 8 时间支持 |
| 日期格式 | `DATE_FORMAT_STR_ISO8601` | ISO 8601 格式 |
| WRITE_ENUMS_USING_TO_STRING | true | 枚举字符串序列化 |
| READ_ENUMS_USING_TO_STRING | true | 枚举字符串反序列化 |
| FAIL_ON_UNKNOWN_PROPERTIES | false | 忽略未知属性 |
| WRITE_DATES_AS_TIMESTAMPS | false | 日期不写为时间戳 |

## 方法

### toString

`static String toString(Object object)`

> Java 对象转换成 JSON 字符串

**参数**:
- `object` (`Object`) — 转换对象

**返回**: `String` — JSON 字符串，对象为 null 时返回 `"{}"`

### toJsonNode (Object)

`static JsonNode toJsonNode(Object object)`

> Java 对象转换成 JsonNode

**返回**: `JsonNode` — JsonNode 对象

### toJsonNode (String)

`static JsonNode toJsonNode(String jsonContent)`

> JSON 字符串转换成 JsonNode

**返回**: `JsonNode` — JsonNode 对象，解析失败返回 NullNode

### toObject (String, Class)

`static <T> T toObject(String jsonContent, Class<T> clazz)`

> JSON 字符串转 Java 对象

**返回**: `T` — Java 对象，解析失败返回 null

### toObject (InputStream, Class)

`static <T> T toObject(InputStream in, Class<T> clazz)`

> 输入流转 Java 对象

**返回**: `T` — Java 对象，解析失败返回 null

### toObject (String, TypeReference)

`static <T> T toObject(String jsonString, TypeReference<T> typeRef)`

> JSON 字符串转泛型 Java 对象

**返回**: `T` — Java 对象，解析失败返回 null

### toObject (JsonNode, Class)

`static <T> T toObject(JsonNode value, Class<T> clazz)`

> JsonNode 转 Java 对象

**返回**: `T` — Java 对象

### toObject (InputStream, TypeReference)

`static <T> T toObject(InputStream in, TypeReference<T> typeRef)`

> 输入流转泛型 Java 对象

**返回**: `T` — Java 对象，解析失败返回 null

## 示例

```java
// 序列化
String json = JsonMapper.toString(user);

// 反序列化
User user = JsonMapper.toObject(json, User.class);

// 泛型反序列化
List<User> users = JsonMapper.toObject(json, new TypeReference<List<User>>(){});

// JsonNode 操作
JsonNode node = JsonMapper.toJsonNode(json);
User user = JsonMapper.toObject(node, User.class);
```