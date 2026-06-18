# jsf-bom Maven 使用指南

> 在配置 `pom.xml` 时优先应用以下规则，了解 JSF 框架的依赖版本管理与引入方式。
> jsf-bom 通过分层 BOM 统一管理整个 Java Service Framework 的依赖版本，避免版本冲突。

版本：0.0.1
GroupId：`io.soil`
Java 版本：21
Updated: 2026-06-18
---

## 核心坐标

| ArtifactId | packaging | 用途 |
|-----------|-----------|------|
| `jsf-dependencies` | pom | 总依赖聚合 BOM，管理所有第三方与内部依赖版本 |
| `jsf-parent` | pom | 父 POM，继承自 `jsf-dependencies`，额外提供多环境 Profile 与 Docker 构建 |

> **关键关系**：`jsf-parent` → 继承 → `jsf-dependencies`。继承 `jsf-parent` 即自动获得 `jsf-dependencies` 的全部版本管理。

---

## Agent 决策树：如何引入依赖

```

当前项目是否为「启动应用（可执行 Spring Boot 服务）」？
├─ 是 → 方式一
└─ 否 →（是否已有父 POM 的子模块）
   ├─ 是 → 方式二
   └─ 否 → 方式三 
```

| 场景 | 推荐方式 | 原因 |
|------|------|------|
| 新建微服务启动项目 | 方式一  | 自动获得 Profile、Docker、编译配置 |
| 已有公司父 POM 的项目 | 方式三  | 不破坏现有继承链 |
| JSF 内部公共库模块 | 方式三  | 与框架保持一致构建行为 |
| 仅需引用 JSF 工具类的轻量库 | 方式二  | 最小化引入 |

---

## 方式一：继承 jsf-parent（推荐用于启动项目）

```xml
<parent>
  <groupId>io.soil</groupId>
  <artifactId>jsf-parent</artifactId>
  <version>0.0.1</version>
</parent>
```

继承后**自动获得**：
- 全部依赖版本管理（无需写 `<version>`）
- Java 21 编译配置（source/target/release=21，UTF-8 编码）
- Lombok 注解处理器配置
- 源码包打包（maven-source-plugin）
- 多环境 Profile（local/backend/dev/uat/prod/live）
- Docker 镜像构建能力（激活 `pd-docker` Profile）

> 详见 [jsf-parent.md](./jsf-parent.md)

---

## 方式二：继续 jsf-dependencies BOM（用于非启动项目）

```xml
<parent>
  <groupId>io.soil</groupId>
  <artifactId>jsf-dependencies</artifactId>
  <version>0.0.1</version>
</parent>
```

导入后，在 `<dependencies>` 中声明所需依赖时**省略 `<version>`**，版本由 BOM 统一管理。

> 详见 [jsf-dependencies.md](./jsf-dependencies.md)



## 方式三：导入 jsf-dependencies BOM（用于非启动项目）

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>io.soil</groupId>
      <artifactId>jsf-dependencies</artifactId>
      <version>0.0.1</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>
```

导入后，在 `<dependencies>` 中声明所需依赖时**省略 `<version>`**，版本由 BOM 统一管理。

> 详见 [jsf-dependencies.md](./jsf-dependencies.md)
---

## 声明依赖的规则（Agent 必读）

引入 BOM/父 POM 后，声明具体依赖时**必须省略 `<version>` 标签**，否则会破坏版本统一管理。

✅ 正确写法：
```xml
<dependencies>
  <dependency>
    <groupId>io.soil</groupId>
    <artifactId>jsf-util</artifactId>
    <!-- 无 <version>，由 BOM 管理 -->
  </dependency>
</dependencies>
```

❌ 错误写法（不要硬编码版本）：
```xml
<dependency>
  <groupId>io.soil</groupId>
  <artifactId>jsf-util</artifactId>
  <version>0.0.1</version>  <!-- 不要写！ -->
</dependency>
```

---

## 依赖速查表（按功能域）

> 完整版本清单见 [jsf-dependencies.md](./jsf-dependencies.md)

### JSF 内部模块

| 功能 | groupId | artifactId | 版本 |
|------|---------|-----------|------|
| 通用 POJO/DTO | `io.soil` | `jsf-pojo` | 0.0.1 |
| 通用工具类 | `io.soil` | `jsf-util` | 0.0.1 |
| Web 应用防火墙 | `io.soil` | `jsf-waf` | 0.0.1 |

### Spring 生态

| 功能 | groupId | artifactId | 版本 |
|------|---------|-----------|------|
| Spring Boot | `org.springframework.boot` | `spring-boot-dependencies` | 3.5.15 |
| Spring Cloud | `org.springframework.cloud` | `spring-cloud-dependencies` | 2025.0.3 |
| Spring Cloud Alibaba | `com.alibaba.cloud` | `spring-cloud-alibaba-dependencies` | 2025.0.0.0 |

### 数据库 / ORM

| 功能 | groupId | artifactId | 版本 |
|------|---------|-----------|------|
| MyBatis-Flex (Boot3) | `com.mybatis-flex` | `mybatis-flex-spring-boot3-starter` | 1.11.7 |
| MyBatis-Flex 核心 | `com.mybatis-flex` | `mybatis-flex-core` | 1.11.7 |
| MyBatis (Spring Boot) | `org.mybatis.spring.boot` | `mybatis-spring-boot-starter` | 3.0.4 |
| PageHelper 分页 | `com.github.pagehelper` | `pagehelper` | 6.1.1 |

### 缓存 / Redis

| 功能 | groupId | artifactId | 版本 |
|------|---------|-----------|------|
| Redisson | `org.redisson` | `redisson-spring-boot-starter` | 3.49.0 |

### 工具库

| 功能 | groupId | artifactId | 版本 |
|------|---------|-----------|------|
| Hutool (BOM) | `cn.hutool` | `hutool-bom` | 5.8.35 |
| Jackson | `com.fasterxml.jackson.core` | `jackson-databind` | 2.18.4 |
| Caffeine 缓存 | `com.github.ben-manes.caffeine` | `caffeine` | 3.2.0 |
| MapStruct-Plus | `io.github.linpeilie` | `mapstruct-plus-spring-boot-starter` | 1.4.8 |
| Commons Lang3 | `org.apache.commons` | `commons-lang3` | 3.17.0 |
| Commons IO | `commons-io` | `commons-io` | 2.19.0 |
| Lombok | `org.projectlombok` | `lombok` | 1.18.46 |

### 认证 / 加密 / 第三方

| 功能 | groupId | artifactId | 版本 |
|------|---------|-----------|------|
| Sa-Token | `cn.dev33` | `sa-token-spring-boot3-starter` | 1.44.0 |
| Sa-Token JWT | `cn.dev33` | `sa-token-jwt` | 1.44.0 |
| Bouncy Castle | `org.bouncycastle` | `bcprov-jdk15to18` | 1.80 |
| JustAuth 第三方登录 | `me.zhyd.oauth` | `JustAuth` | 1.16.7 |
| AWS S3 SDK | `software.amazon.awssdk` | `s3` | 2.28.22 |
| SMS4J 短信 | `org.dromara.sms4j` | `sms4j-spring-boot-starter` | 3.3.4 |
| RocketMQ | `org.apache.rocketmq` | `rocketmq-spring-boot-starter` | 2.3.0 |
| SkyWalking 链路 | `org.apache.skywalking` | `apm-toolkit-trace` | 9.3.0 |
| IP2Region | `org.lionsoul` | `ip2region` | 2.7.0 |

---

## Agent POM 生成检查清单

生成 `pom.xml` 时逐项确认：

- [ ] 是否通过方式一或方式二引入了 BOM？
- [ ] 所有被 BOM 管理的依赖是否都**省略了 `<version>`**？
- [ ] Java 版本是否为 21（若继承 jsf-parent 则自动配置）？
- [ ] 是否需要激活环境 Profile（如 `-P d-dev`）？
- [ ] 是否需要 Docker 构建（加 `-P pd-docker`）？
- [ ] Lombok 依赖 scope 是否为 `provided`（BOM 已默认配置）？

---

## 相关文档

- [jsf-dependencies.md](./jsf-dependencies.md) — 完整依赖版本清单与插件管理
- [jsf-parent.md](./jsf-parent.md) — 父 POM 的 Profile 与 Docker 构建配置