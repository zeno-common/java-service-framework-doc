# OffsetDateTimeUtil

> 日期时间工具类，提供日期时间的格式化和转换操作

- **包**: io.soil.common.date

## 常量

| 常量 | 类型 | 值 |
|------|------|-----|
| `OFFSET_DATE_TIME_FORMATTER` | `DateTimeFormatter` | `DateTimeFormatter.ISO_OFFSET_DATE_TIME` |

## 方法

### toDayStartString

`static String toDayStartString(Temporal time)`

> 将指定日期时间格式化为当天开始时间（00:00:00）

**参数**:
- `time` (`Temporal`) — 日期时间对象

**返回**: `String` — ISO 8601 格式的当天 00:00:00 字符串

### toDayEndString

`static String toDayEndString(Temporal time)`

> 将指定日期时间格式化为当天结束时间（23:59:59）

**参数**:
- `time` (`Temporal`) — 日期时间对象

**返回**: `String` — ISO 8601 格式的当天 23:59:59 字符串

### toMillis

`static Long toMillis(Temporal time)`

> 将指定日期时间转换为毫秒时间戳

**参数**:
- `time` (`Temporal`) — 日期时间对象

**返回**: `Long` — 毫秒时间戳

### from

`static OffsetDateTime from(Temporal time)`

> 将各种 Temporal 类型统一转换为 OffsetDateTime

**支持的类型**:

| 输入类型 | 转换方式 |
|---------|---------|
| `OffsetDateTime` | 直接返回 |
| `ZonedDateTime` | `toOffsetDateTime()` |
| `Instant` | `atOffset(UTC)` |
| `LocalDateTime` | `atZone(systemDefault)` |
| `LocalDate` | `atStartOfDay(systemDefault)` |
| `LocalTime` | 当天 + `atZone(systemDefault)` |

**参数**:
- `time` (`Temporal`) — 日期时间对象

**返回**: `OffsetDateTime` — 统一转换后的 OffsetDateTime

**异常**: `UnsupportedOperationException` — 不支持的 Temporal 类型

### toString

`static String toString(Temporal time)`

> 将日期时间格式化为 ISO 8601 字符串

**参数**:
- `time` (`Temporal`) — 日期时间对象

**返回**: `String` — ISO 8601 带时区格式字符串

## 示例

```java
// 当天开始/结束
String start = OffsetDateTimeUtil.toDayStartString(LocalDateTime.now());
String end = OffsetDateTimeUtil.toDayEndString(LocalDateTime.now());

// 毫秒时间戳
Long millis = OffsetDateTimeUtil.toMillis(Instant.now());

// 统一转换
OffsetDateTime odt = OffsetDateTimeUtil.from(LocalDateTime.now());

// 格式化输出
String iso = OffsetDateTimeUtil.toString(Instant.now());
```