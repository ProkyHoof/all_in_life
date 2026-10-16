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

## 3_1 LangChain
LangChain 是整个生态的核心与起点，为开发者提供了模型调用、工具与中间件集成、智能体构建等一整套基础能力。
其核心价值如下：
- 统一的模型抽象层：屏蔽了不同模型服务提供商（如 OpenAI、Anthropic、Ollama 等）的接口差异，提供一致的调用方式。
- 高度模块化的设计：使用 Message、Tool、Agent、Middleware 等组件实现灵活的组合与扩展。
- 丰富的集成生态：预置了丰富的数据源、API、中间件等，构成了强大的 AI 能力枢纽。

在整体框架中，LangChain 如同智能体的操作系统内核，是所有上层能力构建的基础。  

> 结论：如果你需要构建简单的智能体应用，无需复杂的编排需求，那就选择 LangChain 。  

## 3_2 LangGraph  
当智能体的任务从单一指令执行扩展为多步骤、有状态的复杂工作流，LangGraph 营运而生。  
其核心思想是**将智能体内部抽象为一张有向图**。  
- 节点（Node）：代表独立的功能单元或决策点。
- 边（Edge）：定义了节点之间的流转条件与路径。
- 状态（State）：作为一个共享上下文，在节点间传递并持久化存储任务信息。

通过这种图式结构，LangGraph 让智能体的工作流节点交互变得显式、可控、可观测。  

> 官方也强调“快速起步用 LangChain，复杂控制用 LangGraph，二者并行协同”。  

![](../../../03_attachments/Images/knowledge_images/Python/Agent_develop/Python_20261016_1.png)

> LangChain = 能力抽象层（LLM / Tool / Message 标准化），负责“有什么能力”。  
> LangGraph = 执行与编排层（状态机 / 工作流 / 多 Agent 系统），负责“怎么跑”。  

## 3_3 Deep Agent  
Deep Agent 是新推出的全新组件，被定位为 Agent Harness（智能体执行框架）。它构建于 LangChain 与 LangGraph 之上，增加了规划能力、文件系统、子 Agent 等高级功能。  旨在让开发者无须从零构建复杂的控制逻辑，即可创造具备深度规划、长期记忆与多专家协作能力的智能体。  
Deep Agent 的核心能力如下：
- 显式规划：自主生成、执行并动态调整多步任务计划。
- 虚拟文件系统：为智能体提供结构化的中间结果与知识存储。
- 子智能体：支持任务在多个智能体之间的分解与协作。
- 长期记忆：通过与 LangGraph 


