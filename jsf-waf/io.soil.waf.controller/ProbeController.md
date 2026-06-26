# `ProbeController`

`package io.soil.waf.controller`

`@RestController` `@RequestMapping("/v1/probes")`

健康探针控制器，提供应用活跃状态检测接口

---

## Methods

### `String activeness()`

`@GetMapping("/v1/probes/activeness")`

→ **String** — 活跃探针