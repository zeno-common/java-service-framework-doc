# JSF Skills

JSF（Java Service Framework）Agent Skills 集合，为 AI 编码助手提供框架 SDK 参考、依赖管理和编码规范。

## 可用 Skills

| Skill | 说明 | 安装命令 |
|-------|------|---------|
| `jsf-bom-doc` | Maven BOM/父 POM 配置、依赖版本管理、多环境 Profile、Docker 构建 | `pnpm dlx skills add https://github.com/zeno-common/java-service-framework-doc --skill jsf-bom-doc` |
| `jsf-pojo-doc` | 通用 POJO/DTO 定义，分页结果响应体 | `pnpm dlx skills add https://github.com/zeno-common/java-service-framework-doc --skill jsf-pojo-doc` |
| `jsf-util-doc` | 通用工具类：URL 分页、JSON 映射、日期时间、树结构、集合操作、IP 查询、Spring 上下文 | `pnpm dlx skills add https://github.com/zeno-common/java-service-framework-doc --skill jsf-util-doc` |
| `jsf-wsf-doc` | WSF 框架：全局异常处理、Jackson 配置、健康探针、客户端 IP 解析 | `pnpm dlx skills add https://github.com/zeno-common/java-service-framework-doc --skill jsf-wsf-doc` |
| `jsf-unit-test-doc` | 单元测试工具：YAML 配置加载、JUnit 5 / Mockito 依赖传递 | `pnpm dlx skills add https://github.com/zeno-common/java-service-framework-doc --skill jsf-unit-test-doc` |

## 快速安装

安装全部 skills：

```bash
pnpm dlx skills add https://github.com/zeno-common/java-service-framework-doc
```

安装指定 skill：

```bash
pnpm dlx skills add https://github.com/zeno-common/java-service-framework-doc --skill jsf-bom-doc
```

指定目标 Agent：

```bash
# Claude Code
pnpm dlx skills add https://github.com/zeno-common/java-service-framework-doc --agent claude-code

# Cursor
pnpm dlx skills add https://github.com/zeno-common/java-service-framework-doc --agent cursor
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
| io.soil.jsf.common.constant | `EnumSample` | 枚举定义参考 |
| io.soil.jsf.common.exception | `BaseException`, `UnknownEnumException` | 异常基类 |
| io.soil.jsf.common.date | `DateTimeConst`, `OffsetDateTimeUtil` | 日期时间 |
| io.soil.jsf.common.tree | `Node`, `TreeUtils` | 树结构 |
| io.soil.jsf.common.collection | `CollectionUtil`, `FunctionWithParam` 等 | 集合操作 |
| io.soil.jsf.util.ip | `IpUtil` | IP 工具 |
| io.soil.jsf.util.jdbc | `JsfUrlParams`, `JsfPagingUtil`, `JsfUrlParamsPage` | URL 分页 |
| io.soil.jsf.util.json | `JsonMapper` | JSON 序列化 |
| io.soil.jsf.util.spring | `ApplicationContextUtil` | Spring 上下文 |
| io.soil.jsf.util.config | `JsfCommonAutoConfig` | 自动配置 |

### jsf-wsf-doc

WSF（Web Service Framework）基于 Spring Boot 的 Web 应用框架：

| 包 | 类 | 说明 |
|----|-----|------|
| io.soil.jsf.wsf.config | `WsfConfig` | Jackson 配置与组件扫描 |
| io.soil.jsf.wsf.controller | `ProbeController` | 健康探针 |
| io.soil.jsf.wsf.exception | `WsfException`, `WsfHttpExceptionResolver`, `WsfHttpExceptionResponse` | 异常处理 |
| io.soil.jsf.wsf.util | `RemoteAddrUtil` | 客户端真实 IP |

### jsf-unit-test-doc

JSF 单元测试工具模块，提供 YAML 配置加载和测试依赖传递：

- 引入 `jsf-unit-test`（test scope）自动获得 JUnit 5 + Mockito
- `YamlPropertySourceFactory` — 在轻量级测试上下文中加载 YAML 配置

## 目录结构

```
index.json          # Skills 注册表（agent-skills 0.2.0 discovery spec）
README.md
skills/
├── jsf-bom-doc/
│   ├── SKILL.md
│   └── references/
├── jsf-pojo-doc/
│   ├── SKILL.md
│   └── references/
├── jsf-util-doc/
│   ├── SKILL.md
│   └── references/
├── jsf-wsf-doc/
│   ├── SKILL.md
│   └── references/
└── jsf-unit-test-doc/
    ├── SKILL.md
    └── references/
```