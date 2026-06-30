---
name: "jsf-bom-doc"
description: "Use when coding with jsf-bom, need reference for Maven BOM/parent POM configuration, dependency version management, multi-environment profiles, or Docker build setup."
---

# jsf-bom SDK 参考

JSF BOM（Bill of Materials）— 统一管理 JSF 框架及第三方依赖的版本，提供父 POM 多环境 Profile 和 Docker 构建配置。

## 引入方式

| 方式 | 适用场景 | GAV | 详见 |
|------|---------|-----|------|
| 继承 jsf-parent | 启动项目（推荐） | `io.soil:jsf-parent:0.0.1` | [jsf-parent.md](references/jsf-parent.md) |
| 继承 jsf-dependencies | 非启动项目 | `io.soil:jsf-dependencies:0.0.1` | [jsf-dependencies.md](references/jsf-dependencies.md) |
| 导入 jsf-dependencies BOM | 非启动项目（已有父 POM） | `io.soil:jsf-dependencies:0.0.1` | [jsf-dependencies.md](references/jsf-dependencies.md) |

引入 BOM/父 POM 后，使用 jsf-bom 中的依赖声明，无需重复声明版本号。声明具体依赖时**必须省略 `<version>` 标签**。

✅ 正确写法：
```xml
<dependency>
  <groupId>io.soil.jsf</groupId>
  <artifactId>jsf-util</artifactId>
  <!-- 无 <version>，由 BOM 管理 -->
</dependency>
```

## 声明依赖规则

> 📖 依赖速查表详见 [dependency-quick-reference.md](references/dependency-quick-reference.md)

## 文档索引

| 文档 | 说明 |
|------|------|
| [dependency-quick-reference.md](references/dependency-quick-reference.md) | 依赖速查表（按分类） |
| [jsf-dependencies.md](references/jsf-dependencies.md) | 完整依赖版本清单与插件管理 |
| [jsf-parent.md](references/jsf-parent.md) | 父 POM 的 Profile 与 Docker 构建配置 |

## Agent POM 生成检查清单

- [ ] 是否通过方式一或方式二引入了 BOM？
- [ ] 所有被 BOM 管理的依赖是否都**省略了 `<version>`**？
- [ ] Java 版本是否为 21（若继承 jsf-parent 则自动配置）？
- [ ] Lombok 依赖 scope 是否为 `provided`（BOM 已默认配置）？