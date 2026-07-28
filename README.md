# customer_service | 开源 AI 客服引擎

面向中国电商小商家的开源智能客服引擎。基于 MChat 开源 AI 平台，自研补齐人工坐席路由、CSAT 满意度反馈、RAG 忠实度护栏三大客服运营模块。

## Demo

→ [观看完整演示（2.5 分钟）](https://github.com/SashaQVQ/customer_service/releases)

## 项目背景

中国电商小商家面临 AI 客服"买不起"的困境——晓多年费 5-15 万，免费工具功能弱且不可控。技术服务商（1 人服务 10-20 个商家）想提供 AI 客服但找不到便宜可控的方案。

基于开源 AI 引擎 MChat（MIT 协议），打造了一款开源免费、可自部署、可规模化推给多个客户的智能客服。

## PM 核心产出

- [PRD（12 章）](docs/PRD-智能客服Agent.md)
- [竞品分析（8 玩家四象限 + TCO 对比）](docs/competitive-analysis.md)
- [技术方案](docs/tech-spec.md)
- [架构文档](docs/architecture.md)
- [事实校验护栏架构设计](docs/fact-check-flow.md)

## 自研模块

| 模块 | 说明 |
|------|------|
| 人工坐席路由 | 三级 escalation 规则 + Agent 控制台 |
| CSAT 反馈闭环 | 满意度采集 + 统计面板 |
| RAG 忠实度护栏 | 正则提取实体 → KB 上下文比对 → 标注 ✅/⚠️ |

## 技术栈

Python + FastAPI + React + TypeScript + MySQL

## 产品边界

三个自研模块独立解耦，可单独交付和测试。电商平台 API 需企业资质，标为已知限制。
