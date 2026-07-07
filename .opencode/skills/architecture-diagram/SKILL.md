---
name: architecture-diagram
description: 绘制系统架构图，支持C4模型、云架构（AWS/Azure/GCP/阿里云）、微服务架构、网络拓扑等，多工具输出（Mermaid/D2/SVG）
---

# Architecture Diagram Skill

根据用户需求绘制系统架构图，支持多种呈现风格和输出格式。

## 支持的工具

| 工具 | 适用场景 | 安装/运行 |
|------|---------|----------|
| Mermaid | 快速内嵌Markdown，流程图/时序图/架构图 | `npx -y @mermaid-js/mermaid-cli@latest` |
| D2 | 专业架构图，自动布局 | `npx -y @terrastruct/d2` |
| SVG | 完全自定义的静态架构图 | 无需依赖 |

## 工作流

1. 明确用户描述的架构层级和组件
2. 选择最合适的工具（默认Mermaid）
3. 生成图表代码
4. 使用对应工具渲染为图片（可选）
5. 保存到用户指定路径

## C4架构模型

C4模型从4个层次描述系统架构：

### Level 1: System Context（系统上下文图）
```mermaid
C4Context
    title System Context diagram
    Person(customer, "客户", "使用系统的用户")
    System_Boundary(system, "系统边界") {
        System(mySystem, "我的系统", "核心业务系统")
    }
    System_Ext(external, "外部系统", "第三方服务")
    Rel(customer, mySystem, "使用")
    Rel(mySystem, external, "调用")
```

### Level 2: Container（容器图）
```mermaid
C4Container
    title Container diagram
    Person(user, "用户")
    Container_Boundary(backend, "后端") {
        Container(web, "Web应用", "React", "前端界面")
        Container(api, "API服务", "Spring Boot", "业务逻辑")
        Container(db, "数据库", "MySQL", "数据存储")
    }
    Rel(user, web, "访问")
    Rel(web, api, "API调用")
    Rel(api, db, "读写")
```

### Level 3: Component（组件图）
```mermaid
graph TB
    subgraph "API服务"
        Controller["Controller层"] --> Service["Service层"]
        Service --> Repository["Repository层"]
        Service --> Client["外部客户端"]
        Repository --> Database[("数据库")]
    end
```

## 云架构图风格

### AWS风格
- 使用圆角矩形表示服务
- 分类颜色: 计算(橙色), 存储(绿色), 网络(紫色), 安全(红色), 集成(粉色)
- 使用AWS标准图标样式

### 通用微服务架构
```mermaid
graph LR
    subgraph "客户端"
        A["移动端"]
        B["Web端"]
    end
    subgraph "网关层"
        C["API Gateway"]
    end
    subgraph "服务层"
        D["用户服务"]
        E["订单服务"]
        F["支付服务"]
    end
    subgraph "基础设施"
        G[("数据库")]
        H[("缓存 Redis")]
        I[("消息队列")]
    end
    A --> C
    B --> C
    C --> D & E & F
    D --> G & H
    E --> I --> F
```

## 最佳实践

1. 保持图表简洁，单个图表不超过15-20个节点
2. 分层绘制：先整体再局部
3. 使用颜色区分不同层级或模块
4. 标注关键协议（HTTP/gRPC/MQTT等）
5. 添加图例说明颜色和符号含义
6. 重要组件标注技术栈名称
