# IpUtil

> 本地 IP 工具类，用于获取与指定远程 IP 端口连接的本地 IP 地址

- **包**: io.soil.util.ip

## 方法

### getLocalConnectedIp

`static String getLocalConnectedIp(String remoteIp, Integer remotePort)`

> 获取本地与指定远程 IP 端口连接时使用的 IP 地址

**参数**:
- `remoteIp` (`String`) — 远程 IP 地址（如 `"192.168.1.100"`）
- `remotePort` (`Integer`) — 远程端口（如 8080）

**返回**: `String` — 本地连接 IP 地址，连接失败时返回 `"localhost"`

**异常**: `IllegalArgumentException` — 远程 IP 格式无效或端口超出范围

**连接超时**: 3 秒

## 示例

```java
String localIp = IpUtil.getLocalConnectedIp("192.168.1.100", 8080);
// 返回如 "192.168.1.50"
```