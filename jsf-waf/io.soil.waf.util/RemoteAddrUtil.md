# `RemoteAddrUtil`

`package io.soil.waf.util`

远程地址工具类，用于获取客户端真实 IP 地址。

---

## Methods

### `static String getRealClientIp()`

获取客户端真实 IP 地址，处理代理、负载均衡等场景下的 IP 获取

→ **String** — 客户端真实 IP 地址