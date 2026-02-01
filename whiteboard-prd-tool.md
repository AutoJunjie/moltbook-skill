# Whiteboard PRD Tool - LitePRD

## 概述

一个基于Kanban看板的协作白板工具，让产品经理、开发、运维、QA四个角色通过各自的AI Agent协作完成PRD文档的生成。

---

## 问题与背景

### 当前痛点
- PRD编写通常由产品经理单独完成，其他角色只能被动评审
- 前期brainstorming阶段缺乏结构化工具
- 各角色的专业视角难以在早期融入
- 最终PRD常常缺少技术可行性、运维考量、测试策略等关键内容

### 目标用户
| 角色 | 职责 | Agent能力 |
|------|------|----------|
| PM | 定义需求、用户故事、优先级 | 创建需求卡片、设定优先级 |
| Dev | 技术方案、可行性评估、工作量 | 添加技术备注、拆分任务 |
| Ops | 部署方案、监控告警、资源评估 | 添加运维检查项 |
| QA | 测试策略、验收标准、边界case | 添加测试用例、验收条件 |

---

## 核心功能

### 1. Kanban看板

**列定义：**
```
┌──────────┬──────────┬──────────┬──────────┬──────────┐
│  Ideas   │ Requirements │ Tech Design │ QA Plan  │  Ready   │
│  创意池   │   需求定义   │   技术设计   │  测试计划  │  完成    │
└──────────┴──────────┴──────────┴──────────┴──────────┘
```

**卡片结构：**
```
┌─────────────────────────────┐
│ [优先级] 标题                │
├─────────────────────────────┤
│ 描述内容...                  │
├─────────────────────────────┤
│ 💬 PM: 用户需要这个功能       │
│ 💬 Dev: 预估2天工作量         │
│ 💬 Ops: 需要新增监控指标       │
│ 💬 QA: 需要覆盖边界case       │
├─────────────────────────────┤
│ 标签: [feature] [P0]         │
└─────────────────────────────┘
```

### 2. Agent Skills

每个角色的Agent通过API操作看板：

```yaml
# 通用Skills
- create_card      # 创建卡片
- move_card        # 移动卡片到其他列
- add_comment      # 添加评论
- add_label        # 添加标签

# PM专属
- set_priority     # 设置优先级 (P0/P1/P2)
- define_user_story # 定义用户故事
- set_acceptance_criteria # 设置验收标准

# Dev专属
- add_tech_note    # 添加技术备注
- estimate_effort  # 评估工作量
- split_task       # 拆分子任务
- flag_risk        # 标记技术风险

# Ops专属
- add_ops_checklist # 添加运维检查项
- define_monitoring # 定义监控需求
- estimate_resources # 评估资源需求

# QA专属
- add_test_case    # 添加测试用例
- define_edge_cases # 定义边界case
- set_qa_criteria  # 设置QA验收条件
```

### 3. PRD生成

点击"Generate PRD"按钮，自动将看板内容汇总为Markdown文档：

```markdown
# PRD: [项目名称]

## 1. 概述
[从Ideas列汇总]

## 2. 需求列表
[从Requirements列汇总，按优先级排序]

### 2.1 [需求标题]
- **用户故事**: ...
- **验收标准**: ...
- **优先级**: P0

## 3. 技术方案
[从Tech Design列汇总Dev的评论]

## 4. 运维方案
[汇总Ops的评论和检查项]

## 5. 测试计划
[从QA Plan列汇总]

## 6. 附录
- 工作量估算汇总
- 风险列表
- 资源需求
```

---

## 数据结构

```javascript
// 看板状态
const board = {
  projectName: "示例项目",
  columns: ["ideas", "requirements", "tech_design", "qa_plan", "ready"],
  cards: [
    {
      id: "card_001",
      title: "用户登录功能",
      description: "支持邮箱和手机号登录",
      column: "requirements",
      priority: "P0",
      labels: ["feature", "auth"],
      userStory: "作为用户，我希望能用手机号登录...",
      acceptanceCriteria: ["支持验证码登录", "记住登录状态"],
      comments: [
        { role: "pm", content: "核心功能，必须首批上线", timestamp: "..." },
        { role: "dev", content: "预估3天，需要对接短信服务", timestamp: "..." },
        { role: "ops", content: "短信服务需要申请配额", timestamp: "..." },
        { role: "qa", content: "需要测试验证码过期场景", timestamp: "..." }
      ],
      techNotes: ["使用JWT token", "Redis存储session"],
      opsChecklist: ["配置短信告警", "监控登录失败率"],
      testCases: ["正常登录", "验证码错误", "频繁请求限流"],
      effort: "3d",
      risks: ["短信服务商稳定性"]
    }
  ]
};
```

---

## 交互流程

```
1. PM Agent 创建初始卡片到 Ideas 列
         ↓
2. 团队讨论，PM 补充用户故事，移动到 Requirements
         ↓
3. Dev Agent 添加技术备注和工作量，移动到 Tech Design
         ↓
4. Ops Agent 添加运维检查项和资源评估
         ↓
5. QA Agent 添加测试用例，移动到 QA Plan
         ↓
6. 全部Ready后，点击生成PRD
         ↓
7. 预览/导出 Markdown 文档
```

---

## MVP范围

### 包含
- [x] 单页HTML应用
- [x] Kanban看板UI（拖拽可选，按钮移动也可）
- [x] 卡片CRUD操作
- [x] 四种角色的评论区分
- [x] PRD Markdown生成
- [x] Markdown实时预览
- [x] Skill API定义文档

### 不包含
- [ ] 真实的Agent集成（模拟即可）
- [ ] 多人实时协作（WebSocket）
- [ ] 数据持久化（刷新丢失OK）
- [ ] 用户认证

---

## 文件结构

```
/whiteboard-prd/
├── index.html      # 主页面（包含CSS/JS）
├── skill.md        # Agent Skill定义文档
└── README.md       # 使用说明
```

---

## 待确认问题

1. **Agent模拟方式**: MVP阶段是否需要模拟Agent自动操作的演示？还是纯手动操作UI？

2. **Skill调用格式**: 参考moltbook用curl命令风格，还是用其他格式？

3. **看板列是否可自定义**: 固定5列还是允许用户自定义？

4. **多项目支持**: MVP是否只支持单个项目/看板？

---

## 下一步

确认以上问题后，开始实现：
1. 创建 index.html 主页面
2. 编写 skill.md Agent技能文档
3. 测试完整流程
