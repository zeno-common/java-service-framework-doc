# LeafAutoConfig

> Spring Boot 自动配置类，按 holder-type 注册协调器 Bean

- **包**: io.soil.jsf.leaf
- **注解**: `@Configuration`, `@EnableConfigurationProperties`, `@ComponentScan`

## 说明

`LeafAutoConfig` 根据 `jsf.leaf.holder-type` 配置项决定使用哪种工作节点协调器：
- `default`（默认）— 使用静态配置的 workerId
- `jdbc` — 使用数据库协调自动分配 workerId

注册的 `ILeafGenerator` Bean 会被 `LeafId` 构造函数注入，用于初始化 Snowflake ID 生成器的 dataCenterId 和 workerId。

## 注册的 Bean

### defaultHolder

`ILeafGenerator defaultHolder(Integer dataCenterId, Integer workerId)`

> 静态配置的工作节点协调器

**激活条件**: `jsf.leaf.holder-type=default` 或未配置（matchIfMissing=true）

**参数**:
- `dataCenterId` — 配置的 dataCenterId，默认 0
- `workerId` — 配置的 workerId，默认 0

### leafWorkerJdbcHolder

`ILeafGenerator leafWorkerJdbcHolder(Integer dataCenterId, LeafProperties properties, LeafHolderMapper workerMapper, Integer serverPort)`

> 基于 JDBC 的工作节点协调器

**激活条件**: `jsf.leaf.holder-type=jdbc`

**参数**:
- `dataCenterId` — 配置的 dataCenterId，默认 0
- `properties` — Leaf 配置属性
- `workerMapper` — 数据库 Mapper
- `serverPort` — 当前服务端口，用于构建 nodeKey