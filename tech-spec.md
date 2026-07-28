# 技术方案

> 版本 v1.0 | 2026-07-06 | Sasha

## 底座

基于 [MChat](https://github.com/windinwing/mchat) (MIT License) 开源 AI Agent 平台。

| 层次 | 技术 | 说明 |
|------|------|------|
| 后端框架 | FastAPI (Python 3.12) | 异步 Web 框架 |
| 前端框架 | React + TypeScript + Vite | SPA 管理后台 |
| 数据库 | MySQL 8.0 (Docker) | 主存储 |
| LLM | DeepSeek API | OpenAI 兼容，¥1/百万 token |
| Embedding | BGE-large-zh-v1.5 (硅基流动) | 1024 维，中文优化 |
| 向量检索 | FAISS (内置) | 内存模式 |
| 混合检索 | BM25 + 向量 + RRF | MChat 原生 |
| 部署 | Docker Compose (MySQL) + 裸跑 (Python/Node) | 开发模式 |

## 自定义模块技术栈

与底座保持一致：FastAPI + SQLAlchemy + React。

## 数据库扩展

### 新增表

| 表名 | 模块 | 用途 |
|------|------|------|
| `agent_sessions` | A | 坐席在线状态 |
| `escalation_rules` | A | 转人工触发规则 |
| `feedbacks` | B | 满意度反馈 |
| `sla_metrics` | B | SLA 响应时间记录 |

### 扩展表

| 表名 | 扩展字段 | 模块 |
|------|----------|------|
| `conversations` | `assigned_agent_id`, `escalated_at`, `first_response_at` | A+B |
| `messages` | `feedback_id` | B |

## API 路由

### 模块 A：人工坐席路由

| 方法 | 路径 | 说明 |
|------|------|------|
| POST | `/api/agent/online` | 坐席上线 |
| POST | `/api/agent/offline` | 坐席下线 |
| GET | `/api/agent/status` | 坐席状态 |
| POST | `/api/conversations/{id}/escalate` | 升级人工 |
| POST | `/api/conversations/{id}/assign` | 分配坐席 |
| GET | `/api/agent/conversations` | 我的待处理 |

### 模块 B：CSAT + SLA

| 方法 | 路径 | 说明 |
|------|------|------|
| POST | `/api/feedback` | 提交满意度 |
| GET | `/api/dashboard/csat` | CSAT 统计 |
| GET | `/api/dashboard/sla` | SLA 统计 |

## 安全

- JWT 认证（复用 MChat 机制）
- API 权限控制（复用 MChat Permission 中间件）
- 开发模式关闭生产安全检查
