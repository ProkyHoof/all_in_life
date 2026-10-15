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


Deep Agent
$\down$ (高级 Agent Harness)
LangChain
LangGraph


