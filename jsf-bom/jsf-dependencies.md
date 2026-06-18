# jsf-dependencies

`io.soil:jsf-dependencies:0.0.1` (packaging=pom)

总依赖聚合 BOM，是项目依赖版本管理的统一入口。通过 `dependencyManagement` 以 `import` 方式聚合 6 个子 BOM，并额外直接管理一批第三方依赖与 Maven 插件版本。

---

## 聚合结构

```
jsf-dependencies (聚合入口)
├── jsf-spring-dependencies      (import)  Spring Boot / Spring Cloud
├── jsf-alibaba-dependencies     (import)  Spring Cloud Alibaba / Nacos / Sentinel / Seata / Dubbo
├── jsf-common-dependencies      (import)  jsf-pojo / jsf-util / jsf-waf
├── jsf-jdbc-dependencies        (import)  MyBatis-Flex / MyBatis / PageHelper
├── jsf-redis-dependencies       (import)  Redisson
└── jsf-tools-dependencies       (import)  Hutool / Jackson / Caffeine / MapStruct-Plus / Commons
```

> `jsf-components-dependencies`（ruoyi-common 组件 BOM）当前内容已被注释，暂未实际聚合。

---

## 编译属性（Properties）

| 属性 | 值 | 说明 |
|------|-----|------|
| `maven.compiler.source` | 21 | 源码兼容版本 |
| `maven.compiler.target` | 21 | 编译目标版本 |
| `maven.compiler.release` | 21 | release 模式版本 |
| `project.build.sourceEncoding` | UTF-8 | 源码编码 |
| `project.reporting.outputEncoding` | UTF-8 | 报告输出编码 |

---

## 直接管理的依赖版本

### Spring 生态（经 jsf-spring-dependencies）

| groupId | artifactId | 版本 |
|---------|-----------|------|
| `org.springframework.boot` | `spring-boot-dependencies` | 3.5.15 |
| `org.springframework.cloud` | `spring-cloud-dependencies` | 2025.0.3 |

### Alibaba 生态（经 jsf-alibaba-dependencies）

| groupId | artifactId | 版本 |
|---------|-----------|------|
| `com.alibaba.cloud` | `spring-cloud-alibaba-dependencies` | 2025.0.0.0 |
| `com.alibaba.nacos` | `nacos-client` | 2.5.1 |
| `com.alibaba.csp` | `sentinel-*`（全系列） | 由 spring-cloud-alibaba BOM 管理 |
| `org.apache.seata` | `seata-spring-boot-starter` / `seata-all` | 由 spring-cloud-alibaba BOM 管理 |
| `org.apache.dubbo` | `dubbo-spring-boot-starter` / `dubbo` / `dubbo-spring-boot-actuator` | 3.0.0 |
| `org.apache.dubbo.extensions` | `dubbo-metadata-report-redis` | 由 dubbo-extensions 管理 |
| `com.alibaba.spring` | `spring-context-support` | 由 spring-cloud-alibaba BOM 管理 |

### JSF 内部模块（经 jsf-common-dependencies）

| groupId | artifactId | 版本 |
|---------|-----------|------|
| `io.soil` | `jsf-pojo` | 0.0.1 |
| `io.soil` | `jsf-util` | 0.0.1 |
| `io.soil` | `jsf-waf` | 0.0.1 |

### 数据库 / ORM（经 jsf-jdbc-dependencies）

| groupId | artifactId | 版本 | 备注 |
|---------|-----------|------|------|
| `com.mybatis-flex` | `mybatis-flex-spring-boot3-starter` | 1.11.7 | 排除 HikariCP |
| `com.mybatis-flex` | `mybatis-flex-core` | 1.11.7 | |
| `org.mybatis.spring.boot` | `mybatis-spring-boot-starter` | 3.0.4 | |
| `org.mybatis` | `mybatis` | 3.5.19 | |
| `com.github.pagehelper` | `pagehelper` | 6.1.1 | |

### Redis（经 jsf-redis-dependencies）

| groupId | artifactId | 版本 |
|---------|-----------|------|
| `org.redisson` | `redisson-spring-boot-starter` | 3.49.0 |

### 工具库（经 jsf-tools-dependencies）

| groupId | artifactId | 版本 |
|---------|-----------|------|
| `cn.hutool` | `hutool-bom` | 5.8.35 |
| `org.lionsoul` | `ip2region` | 2.7.0 |
| `io.github.linpeilie` | `mapstruct-plus-spring-boot-starter` | 1.4.8 |
| `com.fasterxml.jackson.core` | `jackson-core` / `jackson-annotations` / `jackson-databind` | 2.18.4 |
| `org.apache.logging.log4j` | `log4j-slf4j-impl` | 2.24.3 |
| `com.lmax` | `disruptor` | 4.0.0 |
| `com.github.ben-manes.caffeine` | `caffeine` | 3.2.0 |
| `commons-io` | `commons-io` | 2.19.0 |
| `jakarta.validation` | `jakarta.validation-api` | 3.1.1 |
| `org.apache.commons` | `commons-lang3` | 3.17.0 |
| `org.apache.commons` | `commons-collections4` | 4.5.0 |

### 直接管理（jsf-dependencies 本身）

| groupId | artifactId | 版本 | 用途 |
|---------|-----------|------|------|
| `org.projectlombok` | `lombok` | 1.18.46 | 代码简化（provided） |
| `cn.dev33` | `sa-token-core` | 1.44.0 | 权限认证核心 |
| `cn.dev33` | `sa-token-spring-boot3-starter` | 1.44.0 | Sa-Token Boot3 启动器 |
| `cn.dev33` | `sa-token-jwt` | 1.44.0 | Sa-Token JWT 扩展 |
| `cn.dev33` | `sa-token-dubbo3` | 1.44.0 | Sa-Token Dubbo3 集成 |
| `org.bouncycastle` | `bcprov-jdk15to18` | 1.80 | 加密库 |
| `me.zhyd.oauth` | `JustAuth` | 1.16.7 | 第三方登录 |
| `org.apache.skywalking` | `apm-toolkit-logback-1.x` | 9.3.0 | 链路追踪日志整合 |
| `org.apache.skywalking` | `apm-toolkit-trace` | 9.3.0 | 链路追踪 |
| `software.amazon.awssdk` | `s3` | 2.28.22 | AWS S3 对象存储 |
| `software.amazon.awssdk` | `s3-transfer-manager` | 2.28.22 | S3 传输管理 |
| `software.amazon.awssdk` | `netty-nio-client` | 2.28.22 | Netty HTTP 客户端 |
| `org.dromara.sms4j` | `sms4j-spring-boot-starter` | 3.3.4 | 短信服务 |
| `org.lionsoul` | `ip2region` | 2.7.0 | 离线 IP 定位 |
| `com.alibaba` | `fastjson` | 1.2.83 | JSON 解析（漏洞修复版） |
| `redis.clients` | `jedis` | 5.1.0 | Dubbo 专用 Redis 客户端 |
| `io.github.linpeilie` | `mapstruct-plus-spring-boot-starter` | 1.4.8 | 对象映射 |
| `org.apache.rocketmq` | `rocketmq-spring-boot-starter` | 2.3.0 | 消息队列 |
| `net.logstash.logback` | `logstash-logback-encoder` | 7.2 | 日志推送 |

---

## 默认依赖（dependencies 段）

引入 `jsf-dependencies`（或继承 `jsf-parent`）后，以下依赖会被**自动引入**，无需重复声明：

| groupId | artifactId | scope | 说明 |
|---------|-----------|-------|------|
| `org.projectlombok` | `lombok` | provided | 编译期代码生成 |
| `junit` | `junit` | test | 单元测试 |

---

## 插件版本管理（pluginManagement）

| groupId | artifactId | 版本 |
|---------|-----------|------|
| `org.apache.maven.plugins` | `maven-compiler-plugin` | 3.15.0 |
| `org.apache.maven.plugins` | `maven-resources-plugin` | 3.5.0 |
| `org.apache.maven.plugins` | `maven-jar-plugin` | 3.5.0 |
| `org.apache.maven.plugins` | `maven-source-plugin` | 3.4.0 |
| `org.apache.maven.plugins` | `maven-shade-plugin` | 3.3.0 |
| `org.apache.maven.plugins` | `maven-dependency-plugin` | 3.11.0 |
| `org.apache.maven.plugins` | `maven-checkstyle-plugin` | 3.2.0 |
| `org.apache.maven.plugins` | `maven-surefire-plugin` | 2.22.2 |
| `com.github.spotbugs` | `spotbugs-maven-plugin` | 4.8.6.2 |
| `org.sonarsource.scanner.maven` | `sonar-maven-plugin` | 3.9.1.2184 |
| `io.fabric8` | `docker-maven-plugin` | 0.48.1 |
| `org.jetbrains.dokka` | `dokka-maven-plugin` | 2.2.0 |
| `com.ly.smart-doc` | `smart-doc-maven-plugin` | 3.1.2 |

### 已激活的构建插件

以下插件在 `jsf-dependencies` 的 `<build><plugins>` 中已配置执行：

| 插件 | 配置说明 |
|------|----------|
| `maven-compiler-plugin` | 注解处理器路径含 Lombok |
| `maven-source-plugin` | package 阶段生成源码 jar |
| `dokka-maven-plugin` | Kotlin/Java 文档生成（gfm-plugin） |
| `smart-doc-maven-plugin` | API 文档生成（配置文件 `./doc/smart-doc.json`） |