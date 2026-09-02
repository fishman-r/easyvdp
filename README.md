# Vehicle Data Platform（VDP）

Vehicle Data Platform 是面向车联网、车队运营、新能源车辆和车辆售后场景的统一大数据平台。平台负责连接车辆与外部业务系统，对车辆运行数据进行接入、解析、计算、治理、分析和开放，并为车辆监控、风险预警、能源管理、维修保养、车队调度和经营决策提供数据能力。

> 当前状态：已完成项目模块目录规划，模块代码和技术栈尚未初始化。

## 平台目标

- 统一接入 GPS、CAN、OBD、T-Box、电池、充电、维修、订单、道路和天气等数据。
- 建立车辆、设备、驾驶员、车队和组织之间统一、可信的基础关系。
- 同时支持高并发实时数据处理、历史数据分析和车辆轨迹查询。
- 建立统一的数据标准、指标口径、标签体系和数据质量规则。
- 为监控、预警、调度、运营、能源、维修和 AI 场景提供可复用的数据服务。
- 通过权限、审计、加密、脱敏和租户隔离保障车辆及位置数据安全。
- 通过标准 API、事件订阅和 Webhook 向合作伙伴安全开放平台能力。

## 总体数据链路

车辆与外部系统 → 数据接入 → 协议解析与标准化 → 实时计算 → 数据湖仓 → 指标与标签 → 业务应用、数据分析及开放平台。

身份权限、安全隐私、文件、通知、任务调度和可观测性作为公共能力贯穿整条数据链路。

## 一、平台入口与公共基础

| 模块 | 英文名称 | 核心能力 |
|---|---|---|
| [vdp-api-gateway](./vdp-api-gateway/)（Todo） | API Gateway | 平台统一访问入口；负责请求路由、协议转换、认证接入、限流、熔断、灰度发布、租户上下文传递和访问日志记录。 |
| [vdp-auth-service](./vdp-auth-service/)（Todo） | Authentication Service | 负责用户和应用登录认证、令牌签发与刷新、单点登录、设备或应用凭证校验以及会话安全；具体角色和数据权限由身份租户模块管理。 |
| [vdp-config-center](./vdp-config-center/)（Todo） | Configuration Center | 集中管理各服务的环境配置、动态参数、功能开关、规则参数和配置版本；支持配置发布、变更审计、回滚及环境隔离。 |
| [vdp-common](./vdp-common/)（Todo） | Common Components | 提供错误码、统一响应、日志规范、异常处理、基础工具、通用校验和公共常量；不承载具体业务逻辑。 |
| [vdp-data-model](./vdp-data-model/)（Todo） | Shared Data Models | 定义车辆、设备、位置、轨迹、报警等统一领域模型，以及 API、消息事件和数据交换契约；负责模型版本和兼容性管理。 |
| [vdp-infrastructure](./vdp-infrastructure/)（Todo） | Infrastructure Adapters | 封装数据库、缓存、消息队列、对象存储、搜索引擎、时序数据库和第三方平台的基础设施适配能力，降低业务模块与具体技术产品的耦合。 |

## 二、车辆与数据接入

| 模块 | 英文名称 | 核心能力 |
|---|---|---|
| [vdp-vehicle-device](./vdp-vehicle-device/)（Todo） | Vehicle & Device Management | 管理车辆 VIN、车型、车牌、所属组织、车队、驾驶员、T-Box、SIM 卡和传感器；维护车辆与设备的绑定、解绑、激活、停用及生命周期记录。 |
| [vdp-data-ingestion](./vdp-data-ingestion/)（Todo） | Data Ingestion Center | 接收车辆终端和外部系统数据；提供 TCP、HTTP、MQTT 等接入能力，以及设备鉴权、连接管理、流量控制、断点补传、数据校验和接入监控。 |
| [vdp-protocol-messaging](./vdp-protocol-messaging/)（Todo） | Protocol & Messaging Center | 负责不同厂商、车型和终端协议的解码、编码与版本适配；将原始报文转换为统一事件，并负责消息发布、重试、死信处理和车辆指令下发。 |
| [vdp-stream-processing](./vdp-stream-processing/)（Todo） | Real-Time Processing Center | 对实时车辆数据进行清洗、去重、补全、关联、窗口计算和状态聚合；生成实时位置、在线状态、行程、里程、能耗和异常事件等结果。 |

## 三、数据资产与治理

| 模块 | 英文名称 | 核心能力 |
|---|---|---|
| [vdp-data-lakehouse](./vdp-data-lakehouse/)（Todo） | Vehicle Data Lakehouse | 统一保存原始、明细、主题、汇总、时序、轨迹和空间数据；支持冷热分层、历史归档、批流一体计算及面向分析的高性能查询。 |
| [vdp-data-governance](./vdp-data-governance/)（Todo） | Data Governance Center | 管理数据标准、元数据、数据目录、数据血缘、质量规则、主数据、敏感等级、责任人和数据生命周期，持续提升数据的完整性、一致性与可追溯性。 |
| [vdp-metrics-tagging](./vdp-metrics-tagging/)（Todo） | Metrics & Tagging Center | 建立统一指标口径和标签体系；管理指标定义、计算规则、统计周期、版本、发布流程，以及车辆、驾驶员、车队、区域和客户标签。 |

## 四、位置、监控与风险

| 模块 | 英文名称 | 核心能力 |
|---|---|---|
| [vdp-gis-trajectory](./vdp-gis-trajectory/)（Todo） | GIS & Trajectory Center | 提供实时位置、历史轨迹、轨迹纠偏、停留点、道路匹配、电子围栏、地理编码、区域统计、里程计算和地图服务商适配能力。 |
| [vdp-vehicle-monitoring](./vdp-vehicle-monitoring/)（Todo） | Vehicle Monitoring Center | 汇总车辆在线状态、位置、速度、方向、里程、油量、电量、故障和任务状态，为车辆列表、监控地图、车辆详情和实时状态查询提供服务。 |
| [vdp-alert-risk](./vdp-alert-risk/)（Todo） | Alert & Risk Control Center | 管理超速、疲劳驾驶、碰撞、越界、异常停车、设备离线、异常能耗和故障等规则；提供事件识别、去重、抑制、升级、处置闭环和风险评分。 |

## 五、车辆业务与智能分析

| 模块 | 英文名称 | 核心能力 |
|---|---|---|
| [vdp-operations-analytics](./vdp-operations-analytics/)（Todo） | Operations Analytics Center | 分析车辆利用率、在线率、出勤率、空驶率、行驶里程、运行时长、区域分布、成本、收入和车队绩效，支持多维度经营分析。 |
| [vdp-energy-management](./vdp-energy-management/)（Todo） | Energy Management Center | 管理燃油、电耗、充电、续航、SOC、SOH、电池温度和能源成本；识别异常能耗、充电异常和电池健康风险。 |
| [vdp-maintenance-service](./vdp-maintenance-service/)（Todo） | Maintenance & After-Sales Center | 管理故障码、远程诊断、保养计划、维修工单、配件更换、服务记录、车辆健康档案和预测性维护。 |
| [vdp-fleet-dispatch](./vdp-fleet-dispatch/)（Todo） | Dispatch & Fleet Management | 管理车队、驾驶员、车辆可用性、运输任务、排班、路线和车辆分配；跟踪调度执行过程，并分析任务完成率和运力使用情况。 |
| [vdp-ai-modeling](./vdp-ai-modeling/)（Todo） | AI & Modeling Center | 管理特征、训练数据集、模型训练、评估、注册、发布、在线推理和效果监控；支持故障预测、驾驶风险、续航、残值和运力需求预测。 |
| [vdp-reporting-dashboard](./vdp-reporting-dashboard/)（Todo） | Reporting & Dashboard Center | 管理报表、数据集、查询条件、统计口径、驾驶舱和专题看板；支持定时报表、权限控制、文件导出和大屏数据服务。 |

## 六、开放、安全与平台支撑

| 模块 | 英文名称 | 核心能力 |
|---|---|---|
| [vdp-open-platform](./vdp-open-platform/)（Todo） | Open API & Integration Platform | 面向内部系统和合作伙伴开放车辆数据与业务能力；管理开发者、应用凭证、API 产品、版本、授权、配额、调用统计、事件订阅和 Webhook。 |
| [vdp-identity-tenant](./vdp-identity-tenant/)（Todo） | Identity & Tenant Management | 管理租户、组织、部门、用户、角色、岗位、菜单、资源权限和车辆数据范围；确保不同客户和组织之间的数据隔离。 |
| [vdp-security-privacy](./vdp-security-privacy/)（Todo） | Data Security & Privacy Center | 负责数据分类分级、加密、脱敏、密钥管理、访问审计、授权留痕、位置隐私、数据保留及删除策略和安全合规检查。 |
| [vdp-operations-observability](./vdp-operations-observability/)（Todo） | Platform Operations & Observability | 汇总服务指标、日志、调用链、任务状态、消息积压和数据延迟；提供告警、SLA/SLO、容量、成本、故障定位、备份和容灾监控。 |
| [vdp-file-service](./vdp-file-service/)（Todo） | File Storage Service | 统一管理图片、附件、维修凭证、报表和导出文件；提供上传、下载、元数据、访问权限、有效期、完整性校验和对象存储适配。 |
| [vdp-notification](./vdp-notification/)（Todo） | Notification Center | 管理通知模板、接收人、渠道和发送策略；支持站内信、短信、邮件、语音及第三方消息渠道，并记录发送、重试和回执状态。 |
| [vdp-job-scheduler](./vdp-job-scheduler/)（Todo） | Job Scheduling Center | 负责定时统计、数据同步、报表生成、数据归档和模型训练等任务的编排、分片、重试、补偿、依赖和执行历史管理。 |

## 七、前端应用

| 模块 | 英文名称 | 核心能力 |
|---|---|---|
| [vdp-admin-web](./vdp-admin-web/)（Todo） | Administration Web Portal | 面向平台管理员和业务管理员，提供车辆、设备、组织、租户、权限、规则、配置、开放接口和运维管理页面。 |
| [vdp-dashboard-web](./vdp-dashboard-web/)（Todo） | Data Visualization Portal | 面向运营、调度和管理人员，提供车辆地图、实时监控、报警处置、运营分析、能源分析、专题驾驶舱和数据大屏。 |

## 模块协作原则

1. 统一模型：跨模块传递的数据应使用 vdp-data-model 定义的标准模型和事件契约。
2. 数据归属清晰：每个业务模块只维护自身拥有的数据，不直接读写其他模块的内部数据库。
3. 接口与事件并用：即时查询或命令使用 API，状态变化和批量数据流转优先使用事件。
4. 原始数据可追溯：原始车辆报文进入标准化处理前应保留，解析结果能够追溯到来源、设备、协议版本和接收时间。
5. 租户全链路隔离：租户、组织和数据权限上下文应贯穿网关、服务、消息、任务和存储。
6. 安全默认开启：认证、授权、加密、脱敏、审计和数据保留策略作为平台基础要求，而不是业务模块的可选功能。
7. 全链路可观测：服务调用、车辆连接、消息队列、实时计算、离线任务和数据质量都需要统一监控。

## 推荐建设顺序

### 第一阶段：车辆接入与实时监控

优先建设 API 网关、认证、车辆设备、数据接入、协议解析、实时计算、GIS 轨迹、车辆监控、基础权限和可观测性，形成车辆数据从接入到展示的完整链路。

### 第二阶段：风险与数据资产

建设预警风控、数据湖仓、数据治理、指标标签、通知、调度任务和报表驾驶舱，形成稳定的数据资产和业务闭环。

### 第三阶段：运营业务

建设车队调度、运营分析、能源管理、维修售后和开放平台，支撑车辆运营和外部系统协同。

### 第四阶段：智能化

在数据质量、历史样本和业务反馈稳定后建设 AI 模型能力，逐步上线故障预测、风险评分、续航预测和运力预测。

## 项目命名约定

- 平台英文名称：Vehicle Data Platform
- 平台简称：VDP
- 根项目名称：vehicle-data-platform
- 后端模块名称：vdp-{domain-name}
- 前端模块名称：vdp-{application-name}-web
- Java 基础包名建议：com.company.vdp

后续初始化具体技术栈时，应在各模块目录内增加独立的模块说明，明确模块职责、对外接口、事件、数据归属、运行依赖和本地启动方式。
