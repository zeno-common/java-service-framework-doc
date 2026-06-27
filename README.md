# JSF Skills

JSF（Java Service Framework）Agent Skills 集合，为 AI 编码助手提供框架 SDK 参考、依赖管理和编码规范。

## 可用 Skills

| Skill | 说明 | 安装命令 |
|-------|------|---------|
| `jsf-bom-doc` | Maven BOM/父 POM 配置、依赖版本管理、多环境 Profile、Docker 构建 | `pnpm dlx skills add https://gitee.com/zeno-common/java-service-framework --skill jsf-bom-doc` |
| `jsf-pojo-doc` | 通用 POJO/DTO 定义，分页结果响应体 | `pnpm dlx skills add https://gitee.com/zeno-common/java-service-framework --skill jsf-pojo-doc` |
| `jsf-util-doc` | 通用工具类：URL 分页、JSON 映射、日期时间、树结构、集合操作、IP 查询、Spring 上下文 | `pnpm dlx skills add https://gitee.com/zeno-common/java-service-framework --skill jsf-util-doc` |
| `jsf-waf-doc` | WAF 框架：全局异常处理、Jackson 配置、健康探针、客户端 IP 解析 | `pnpm dlx skills add https://gitee.com/zeno-common/java-service-framework --skill jsf-waf-doc` |

## 快速安装

安装全部 skills：

```bash
pnpm dlx skills add https://gitee.com/zeno-common/java-service-framework
```

安装指定 skill：

```bash
pnpm dlx skills add https://gitee.com/zeno-common/java-service-framework --skill jsf-bom-doc
```

指定目标 Agent：

```bash
# Claude Code
pnpm dlx skills add https://gitee.com/zeno-common/java-service-framework --agent claude-code

# Cursor
pnpm dlx skills add https://gitee.com/zeno-common/java-service-framework --agent cursor
```

## Skill 详情

### jsf-bom-doc

Maven BOM（Bill of Materials）统一管理 JSF 框架及第三方依赖版本，提供父 POM 多环境 Profile 和 Docker 构建配置。

- 引入方式：继承 jsf-parent / 继承 jsf-dependencies / 导入 jsf-dependencies BOM
- 依赖速查表、完整版本清单、Profile 与 Docker 构建配置

### jsf-pojo-doc

JSF 通用 POJO/DTO 模块，提供分页结果封装等基础数据结构。

- `PagedResult` — 分页结果响应体

### jsf-util-doc

JSF 通用工具模块，涵盖以下工具类：

| 包 | 类 | 说明 |
|----|-----|------|
| io.soil.common.constant | `EnumSample` | 枚举定义参考 |
| io.soil.common.exception | `BaseException`, `UnknownEnumException` | 异常基类 |
| io.soil.common.date | `DateTimeConst`, `OffsetDateTimeUtil` | 日期时间 |
| io.soil.common.tree | `Node`, `TreeUtils` | 树结构 |
| io.soil.common.collection | `CollectionUtil`, `FunctionWithParam` 等 | 集合操作 |
| io.soil.util.ip | `IpUtil` | IP 工具 |
| io.soil.util.jdbc | `JsfUrlParams`, `JsfPagingUtil`, `JsfUrlParamsPage` | URL 分页 |
| io.soil.util.json | `JsonMapper` | JSON 序列化 |
| io.soil.util.spring | `ApplicationContextUtil` | Spring 上下文 |
| io.soil.util.config | `JsfCommonAutoConfig` | 自动配置 |

### jsf-waf-doc

WAF（Web Application Framework）基于 Spring Boot 的 Web 应用框架：

| 包 | 类 | 说明 |
|----|-----|------|
| io.soil.waf.config | `WafConfig` | Jackson 配置与组件扫描 |
| io.soil.waf.controller | `ProbeController` | 健康探针 |
| io.soil.waf.exception | `WafException`, `WafHttpExceptionResolver`, `WafHttpExceptionResponse` | 异常处理 |
| io.soil.waf.util | `RemoteAddrUtil` | 客户端真实 IP |

## 目录结构

```
docs/jsf-skills/
├── index.json          # Skills 注册表（agent-skills 0.2.0 discovery spec）
├── README.md
└── skills/
    ├── jsf-bom-doc/
    │   ├── SKILL.md
    │   └── references/
    ├── jsf-pojo-doc/
    │   ├── SKILL.md
    │   └── references/
    ├── jsf-util-doc/
    │   ├── SKILL.md
    │   └── references/
    └── jsf-waf-doc/
        ├── SKILL.md
        └── references/
```
