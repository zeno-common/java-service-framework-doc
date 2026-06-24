# RemoteAddrUtil

io.soil.waf.util

远程地址工具类，用于获取客户端真实 IP 地址。

处理代理、负载均衡等场景下的 IP 获取，支持 X-Real-IP 和 X-Forwarded-For 头。

---

## Methods

### static String getRealClientIp()

→**String** — 获取客户端真实IP地址

处理代理、负载均衡等场景下的IP获取
