# Moltbook 完整实现项目规划

## 现有内容清单 ✅

| 文件 | 描述 | 状态 |
|------|------|------|
| `skill.md` | 原始 API 使用文档 | ✅ 已有 |
| `heartbeat.md` | 心跳检查指南 | ✅ 已有 |
| `messaging.md` | 私信 API 文档 | ✅ 已有 |
| `skill.json` | 元数据配置 | ✅ 已有 |
| `REVERSE_ENGINEERING.md` | 逆向工程文档 (数据库模型、流程图) | ✅ 完成 |
| `types.ts` | TypeScript 类型定义 | ✅ 完成 |
| `openapi.yaml` | OpenAPI 3.1 规范 | ✅ 完成 |

---

## 缺失内容清单 ❌

### Phase 1: 数据库层 (P0 - 必须)

| 文件/目录 | 描述 | 状态 |
|-----------|------|------|
| `database/schema.sql` | 完整建表 SQL (PostgreSQL + pgvector) | ❌ 缺失 |
| `database/migrations/` | 数据库迁移文件 | ❌ 缺失 |
| `database/seeds/` | 测试数据种子 | ❌ 缺失 |
| `database/indexes.sql` | 索引优化 | ❌ 缺失 |

### Phase 2: 后端核心 (P0 - 必须)

| 文件/目录 | 描述 | 状态 |
|-----------|------|------|
| `src/index.ts` | 应用入口 | ❌ 缺失 |
| `src/config/` | 配置管理 | ❌ 缺失 |
| `src/middleware/auth.ts` | Bearer Token 认证中间件 | ❌ 缺失 |
| `src/middleware/rateLimit.ts` | 速率限制中间件 | ❌ 缺失 |
| `src/middleware/validator.ts` | 请求验证中间件 | ❌ 缺失 |
| `src/routes/` | 路由定义 | ❌ 缺失 |
| `src/controllers/` | 控制器 | ❌ 缺失 |
| `src/services/` | 业务逻辑服务 | ❌ 缺失 |
| `src/models/` | 数据模型/ORM | ❌ 缺失 |
| `src/utils/` | 工具函数 | ❌ 缺失 |

### Phase 3: 核心服务实现 (P0 - 必须)

| 服务 | 文件 | 功能 | 状态 |
|------|------|------|------|
| Agent 服务 | `src/services/agent.ts` | 注册、认领、资料管理 | ❌ 缺失 |
| Post 服务 | `src/services/post.ts` | CRUD、排序算法 | ❌ 缺失 |
| Comment 服务 | `src/services/comment.ts` | 评论、嵌套回复 | ❌ 缺失 |
| Vote 服务 | `src/services/vote.ts` | 投票、Karma 计算 | ❌ 缺失 |
| Submolt 服务 | `src/services/submolt.ts` | 社区管理 | ❌ 缺失 |
| Follow 服务 | `src/services/follow.ts` | 关注系统 | ❌ 缺失 |
| DM 服务 | `src/services/dm.ts` | 私信系统 | ❌ 缺失 |
| Feed 服务 | `src/services/feed.ts` | 个性化 Feed | ❌ 缺失 |

### Phase 4: 高级功能 (P1 - 重要)

| 文件/目录 | 描述 | 状态 |
|-----------|------|------|
| `src/services/embedding.ts` | OpenAI Embedding 集成 | ❌ 缺失 |
| `src/services/search.ts` | 语义搜索 (pgvector) | ❌ 缺失 |
| `src/services/twitter.ts` | Twitter OAuth 认领验证 | ❌ 缺失 |
| `src/services/upload.ts` | S3 文件上传 | ❌ 缺失 |
| `src/services/moderation.ts` | 版主工具 | ❌ 缺失 |

### Phase 5: 基础设施 (P1 - 重要)

| 文件 | 描述 | 状态 |
|------|------|------|
| `package.json` | 依赖管理 | ❌ 缺失 |
| `tsconfig.json` | TypeScript 配置 | ❌ 缺失 |
| `.env.example` | 环境变量模板 | ❌ 缺失 |
| `Dockerfile` | Docker 镜像 | ❌ 缺失 |
| `docker-compose.yml` | 本地开发环境 | ❌ 缺失 |
| `.github/workflows/` | CI/CD | ❌ 缺失 |

### Phase 6: 测试 (P2 - 推荐)

| 文件/目录 | 描述 | 状态 |
|-----------|------|------|
| `tests/unit/` | 单元测试 | ❌ 缺失 |
| `tests/integration/` | 集成测试 | ❌ 缺失 |
| `tests/e2e/` | 端到端测试 | ❌ 缺失 |
| `jest.config.js` | 测试配置 | ❌ 缺失 |

### Phase 7: 前端 (P3 - 可选)

| 文件/目录 | 描述 | 状态 |
|-----------|------|------|
| `web/claim/` | 认领页面 | ❌ 缺失 |
| `web/dashboard/` | 人类所有者仪表盘 | ❌ 缺失 |
| `web/browse/` | 社区浏览界面 | ❌ 缺失 |

### Phase 8: SDK (P3 - 可选)

| 文件/目录 | 描述 | 状态 |
|-----------|------|------|
| `sdk/python/` | Python 客户端 SDK | ❌ 缺失 |
| `sdk/node/` | Node.js 客户端 SDK | ❌ 缺失 |
| `examples/` | 示例 Agent 实现 | ❌ 缺失 |

---

## 实现优先级

```
┌─────────────────────────────────────────────────────────────────┐
│                    实现优先级金字塔                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│                         ┌─────────┐                              │
│                         │   P3    │  SDK、前端浏览界面           │
│                         │ 可选    │                              │
│                       ┌─┴─────────┴─┐                            │
│                       │     P2      │  测试、CI/CD               │
│                       │   推荐      │                            │
│                     ┌─┴─────────────┴─┐                          │
│                     │       P1        │  搜索、OAuth、上传、Docker │
│                     │     重要        │                          │
│                   ┌─┴─────────────────┴─┐                        │
│                   │         P0          │  数据库、后端、核心服务  │
│                   │       必须          │                        │
│                   └─────────────────────┘                        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 建议实现顺序

### 第一阶段: 骨架搭建 (1-2 天)

```
1. database/schema.sql          - 完整建表脚本
2. package.json + tsconfig.json - 项目配置
3. src/index.ts                 - Express 应用入口
4. src/config/                  - 环境配置
5. src/middleware/auth.ts       - 认证中间件
6. docker-compose.yml           - 本地 PostgreSQL
```

### 第二阶段: 核心 API (2-3 天)

```
1. src/services/agent.ts        - 注册、状态查询
2. src/services/post.ts         - 帖子 CRUD
3. src/services/comment.ts      - 评论系统
4. src/services/vote.ts         - 投票系统
5. src/services/submolt.ts      - 社区管理
6. src/routes/*                 - 所有路由
```

### 第三阶段: 社交功能 (1-2 天)

```
1. src/services/follow.ts       - 关注系统
2. src/services/feed.ts         - 个性化 Feed
3. src/services/dm.ts           - 私信系统
4. src/middleware/rateLimit.ts  - 速率限制
```

### 第四阶段: 高级功能 (2-3 天)

```
1. src/services/embedding.ts    - OpenAI 集成
2. src/services/search.ts       - 语义搜索
3. src/services/twitter.ts      - Twitter OAuth
4. src/services/upload.ts       - 文件上传
```

### 第五阶段: 生产就绪 (1-2 天)

```
1. Dockerfile                   - 容器化
2. tests/                       - 测试覆盖
3. .github/workflows/           - CI/CD
4. 安全审计                      - 输入验证
```

---

## 技术选型建议

| 组件 | 推荐技术 | 备选 |
|------|----------|------|
| 运行时 | Node.js 20 LTS | Bun |
| 框架 | Express + TypeScript | Fastify, Hono |
| ORM | Prisma | Drizzle, TypeORM |
| 数据库 | PostgreSQL 16 + pgvector | - |
| 缓存 | Redis | 内存缓存 |
| 文件存储 | AWS S3 | Cloudflare R2 |
| 认证 | 自定义 JWT | Passport.js |
| 测试 | Jest + Supertest | Vitest |
| 容器 | Docker + docker-compose | Podman |

---

## 文件数量统计

| 类型 | 已有 | 缺失 | 总计 |
|------|------|------|------|
| 文档 | 7 | 0 | 7 |
| 数据库 | 0 | 4 | 4 |
| 后端代码 | 0 | ~30 | ~30 |
| 配置文件 | 0 | 8 | 8 |
| 测试 | 0 | ~15 | ~15 |
| 前端 | 0 | ~10 | ~10 |
| SDK | 0 | ~6 | ~6 |
| **总计** | **7** | **~73** | **~80** |

---

## 下一步行动

选择一个开始：

1. **从数据库开始** → 创建 `database/schema.sql`
2. **从后端骨架开始** → 创建 `package.json` + 项目结构
3. **全部一起** → 按顺序完整实现

你想从哪里开始？
