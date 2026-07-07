---
name: mermaid
description: 使用Mermaid语法生成各种图表（流程图、时序图、类图、ER图、状态图、甘特图、饼图、用户旅程图等），支持导出为PNG/SVG，适用于文档、PPT、技术博客
---

# Mermaid Diagram Skill

根据用户需求生成 Mermaid 图表代码，并渲染为可视化图片。

## 图表类型速查

| 图表类型 | Mermaid关键字 | 用途 |
|---------|--------------|------|
| 流程图 | graph / flowchart | 业务流程、算法逻辑 |
| 时序图 | sequenceDiagram | 交互流程、API调用 |
| 类图 | classDiagram | OO设计、领域模型 |
| 状态图 | stateDiagram-v2 | 状态机、工作流 |
| ER图 | erDiagram | 数据库设计 |
| 甘特图 | gantt | 项目排期 |
| 饼图 | pie | 数据占比 |
| 用户旅程图 | journey | 用户体验 |
| Git分支图 | gitGraph | Git工作流 |
| 象限图 | quadrantChart | 战略分析 |
| XY图表 | xychart | 数据可视化 |
| 思维导图 | mindmap | 头脑风暴 |
| 时间轴 | timeline | 时间线展示 |

## 工作流

1. 确认用户想要的图表类型和内容
2. 生成合法的 Mermaid 代码
3. 使用 `npx -y @mermaid-js/mermaid-cli@latest` 渲染为图片（可选，默认只输出代码块）
4. 将生成的图片保存到用户指定的路径

## Mermaid语法规范

### 流程图
```mermaid
graph TD
    A[开始] --> B{判断}
    B -->|是| C[处理]
    B -->|否| D[结束]
```

方向: TB(从上到下), TD(同TB), BT(从下到上), RL(从右到左), LR(从左到右)
节点形状: `[矩形]`, `(圆角矩形)`, `{菱形}`, `>不对称]`, `((圆形))`

### 时序图
```mermaid
sequenceDiagram
    participant A as 客户端
    participant B as 服务端
    A->>B: 请求
    B-->>A: 响应
```

箭头: `->`(实线), `-->`(虚线), `->>`(实线带箭头), `-->>`(虚线带箭头)

### 类图
```mermaid
classDiagram
    class Animal {
        +String name
        +eat() void
    }
    class Dog {
        +bark() void
    }
    Animal <|-- Dog
```

关系: `<|--`(继承), `*--`(组合), `o--`(聚合), `-->`(关联), `..|>`(实现)

### ER图
```mermaid
erDiagram
    CUSTOMER ||--o{ ORDER : places
    ORDER ||--|{ LINE-ITEM : contains
```

### 状态图
```mermaid
stateDiagram-v2
    [*] --> 待审核
    待审核 --> 已通过: 通过
    待审核 --> 已驳回: 驳回
    已通过 --> [*]
```

### 甘特图
```mermaid
gantt
    title 项目计划
    dateFormat  YYYY-MM-DD
    section 阶段A
    任务1 :a1, 2024-01-01, 30d
    任务2 :after a1, 20d
```

### C4架构图
```mermaid
C4Context
    title System Context diagram
    Person(user, "用户", "系统用户")
    System(sys, "系统", "核心系统")
    Rel(user, sys, "使用")
```

## 最佳实践

1. 节点ID使用有意义的英文命名
2. 复杂图表添加注释说明
3. 合理使用subgraph对节点分组
4. 优先使用 `graph TD` 方向
5. 中文内容需要确保渲染环境支持中文字体
