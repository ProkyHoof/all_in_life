---
tags:
  - knowledge
introduction: 大模型应用开发
start_date: 2026-10-15
---

# 1 LangChain 1.2 概述  

## 1_1 单一的大语言模型的局限性  
1. 知识受限于训练数据。（大语言模型其实不能获取网络信息的）
2. 无法直接与外部系统交互。（无法查找实时数据，调用 API 或调取数据库）
3. 不具备状态保持能力。（难以进行连贯的多轮对话，遗忘之前的上下文）

## 1-2 LangChain 框架的定位  

> LangChain 作为大模型与应用间的中间层，可统一调用各类大模型、管理提示词与上下文，还能集成外部工具和数据源，快速搭建具备推理、行动能力的智能体。  

核心定位三点：  
1. 打通大模型与外部资源：统一接口对接数据库、检索引擎、API、文件系统等。
2. 封装底层复杂逻辑：抽象工具调用、记忆等功能，降低智能体开发难度。
3. 支撑多智能体协作：依托 LangGraph 等生态，从单智能体拓展至多智能体协作，可构建工业级智能体。

# 2 LangChain 
 
## 2-1 LangChain v 1.2 的主要模块  
- `langchain-core`：官方推荐的核心 API。
- `langchain-classic`：冗余代码或不推荐使用的经典 API 都移到此。
- `langchain-community`：第三方集成。
- `langgraph`：深度整合 LangGraph 1.0,协调多个 Chain，Agent，Tools 完成更复杂的任务，并且支持循环调用，是 langchain 图形化的增强版。

## 2-2 API 文档
[官网](https://reference.langchain.com/)  
[Github](https://github.com/langchain-ai)
[英文文档](https://docs.langchain.com/oss/python/deepagents/overview)
[中文文档](https://langchain-zh.cn/oss/python/langchain/overview)
[API 文档](https://reference.langchain.com/python/langchain/overview)

# 3 LangChain 生态四大支柱  

LangChain 技术生态的四大核心支柱构成：`LangChain`，`LangGraph`，`Deep Agent`，`LangSmith`。  
[官方解释](https://docs.langchain.com/oss/python/concepts/products)

![Drawing 2026-10-15 16.35.06.excalidraw](../../../03_attachments/Excalidraw/Python/Drawing%202026-10-15%2016.35.06.excalidraw.md)

- LangChain：是整个生态的基础框架层，它统一了不同大模型的接口，并提供了工具、记忆、检索等模块化工具。
- LangGraph：当任务变得复杂，需要多步骤、有状态的工作流时，就需要 LangGraph 这个编排运行时。它将工作流抽象为“状态图”，通过节点（步骤）和边（流转条件）来精确控制执行流程。
- Deep Agent：是构建在 LangChain 和 LangGraph 之上的智能体执行框架（Agent Harness），它预先封装了构建复杂 Agent 所需的高级能力。
	- 显示规则：能自主生成并执行多步任务计划。
	- 虚拟文件系统：用于管理中间结果和知识存储。
	- 子智能体：支持将任务。
	- 长期记忆：结合 LangGraph 的状态存储，实现跨对话的经验积累。
- LangSmith：是一个跨框架的可观测性、评估与部署平台。
	- 追踪与调试：可视化每一步执行过程，快速定位问题。
	- 评估与测试：管理数据集，对 Agent 的轨迹进行回归评测。
	- 部署与管理：提供生产环境下的部署、鉴权等托管基础设施。


