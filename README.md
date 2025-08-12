# Arq AI

[![PyPI - Version](https://img.shields.io/pypi/v/arq-ai)](https://pypi.org/project/arq-ai/)
[![Python 3.12+](https://img.shields.io/badge/python-3.12+-blue.svg)](https://www.python.org/downloads/)
[![PyPI - Downloads](https://img.shields.io/pypi/dm/arq-ai)](https://pypi.org/project/arq-ai/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![codecov](https://img.shields.io/codecov/c/github/arq-ai/arq-ai/main.svg)](https://codecov.io/gh/arq-ai/arq-ai)
[![Build Status](https://img.shields.io/github/actions/workflow/status/arq-ai/arq-ai/ci.yml?branch=main)](https://github.com/arq-ai/arq-ai/actions/workflows/ci.yml)
[![Ruff Style](https://img.shields.io/badge/style-ruff-41B5BE)](https://github.com/astral-sh/ruff)

## Advanced AI Agent Framework

Build your AI agents in three lines of code!

## Why?
* Three lines of code setup
* Simple Agent Definition
* Fast Responses
* Enterprise Integration
* Multi-Agent Swarm
* Multi-Modal (Images & Audio & Text)
* Conversational Memory & History
* Internet Search
* Intelligent Routing
* Business Alignment
* Extensible Tooling
* Autonomous Operation
* Smart Workflows
* Structured Outputs
* Knowledge Base
* MCP Support
* Guardrails
* Image Generation
* Pydantic Logfire
* Tested & Secure
* Built in Python
* Powers [ArqHub](https://arqhub.com)
* Powers [Arq AI Platform](https://arq-ai.com)

## Unique Selling Proposition (USP) - Smart Workflows

Arq AI is the first AI agent framework to deliver truly intelligent, dynamic workflows.

With Arq AI, you can seamlessly define and integrate tools — such as Zapier MCP (for sending emails via Mailgun) and custom API integrations — directly into your agent's capabilities.

Then prompt your agent with natural language, for example:  
"Get my customer data from the CRM and then email a summary to my team."

Arq AI will automatically orchestrate the workflow:  
It will first use the CRM integration tool to retrieve your data, then invoke the Zapier MCP tool to send the results via email — all without manual intervention or brittle, hardcoded logic.

You can also chain tool outputs (structured or unstructured) as inputs for subsequent tasks, enabling complex, multi-step automations with ease.

**The result?**  
A framework that is both powerful and simple — eliminating the need for static, fragile workflow definitions.  
Smart workflows are as easy as combining your tools and prompts.

## Features

* Easy three lines of code setup
* Simple agent definition using JSON
* Designed for a multi-agent swarm 
* Fast multi-modal processing of text, audio, and images
* Smart workflows that keep flows simple and smart
* Integrate with any API or service with powerful tools
* MCP tool usage with first-class support for [Zapier](https://zapier.com/mcp)
* Integrated observability and tracing via [Pydantic Logfire](https://pydantic.dev/logfire)
* Persistent memory that preserves context across all agent interactions
* Quick Internet search to answer users' queries
* Streamlined message history for all agent interactions
* Intelligent query routing to agents with optimal domain expertise or your own custom routing
* Unified value system ensuring brand-aligned agent responses
* Powerful tool integration using standard Python packages and/or inline tools
* Assigned tools are utilized by agents automatically and effectively
* Integrated Knowledge Base with semantic search and automatic PDF chunking
* Input and output guardrails for content filtering, safety, and data sanitization
* Generate custom images based on text prompts with storage on S3 compatible services
* Deterministically return structured outputs
* Combine with event-driven systems to create autonomous agents

## Stack

### Tech

* [Python](https://python.org) - Programming Language
* [OpenAI](https://openai.com) - AI Model Provider
* [MongoDB](https://mongodb.com) - Conversational History (optional)
* [Zep Cloud](https://getzep.com) - Conversational Memory (optional)
* [Pinecone](https://pinecone.io) - Knowledge Base (optional)
* [Zapier](https://zapier.com) - App Integrations (optional)
* [Pydantic Logfire](https://pydantic.dev/logfire) - Observability and Tracing (optional)

### AI Models Used

**OpenAI**
* [gpt-4.1](https://platform.openai.com/docs/models/gpt-4.1) (agent & router)
* [text-embedding-3-large](https://platform.openai.com/docs/models/text-embedding-3-large) (embedding)
* [tts-1](https://platform.openai.com/docs/models/tts-1) (audio TTS)
* [gpt-4o-mini-transcribe](https://platform.openai.com/docs/models/gpt-4o-mini-transcribe) (audio transcription)

## Installation

You can install Arq AI using pip:

`pip install arq`

## Flows

In both flows of single and multiple agents - it is one user query to one agent using one or many tools (if needed).

An agent can have multiple tools and will choose the best ones to fulfill the user's query.

Routing is determined by optimal domain expertise of the agent for the user's query.

When the agent uses tools it feeds the tools output back to itself to generate the final response.

This is important as tools generally output unstructured and unformatted data that the agent needs to prepare for the user.

Keep this in mind while designing your agentic systems using Arq AI.

```ascii
                       Single Agent                                     
                                                                        
     ┌────────┐        ┌─────────┐        ┌────────-┐                    
     │        │        │         │        │         │                    
     │        │        │         │        │         │                    
     │  User  │◄──────►│  Agent  │◄──────►│  Tools  │                    
     │        │        │         │        │         │                    
     │        │        │         │        │         │                    
     └────────┘        └─────────┘        └────────-┘                    
                                                                        
                                                                        
                                                                        
                                                                        
                                                                        
                      Multiple Agents                                   
                                                                        
     ┌────────┐        ┌──────────┐        ┌─────────┐        ┌────────-┐
     │        │        │          │        │         │        │         │
     │        │        │          │        │         │        │         │
┌───►│  User  ├───────►│  Router  ├───────►│  Agent  │◄──────►│  Tools  │
│    │        │        │          │        │         │        │         │
│    │        │        │          │        │         │        │         │
│    └────────┘        └──────────┘        └────┬────┘        └────────-┘
│                                               │                       
│                                               │                       
│                                               │                       
│                                               │                       
└───────────────────────────────────────────────┘

## Usage

### Text/Text Streaming

```python
from arq_ai import ArqAI

config = {
    "openai": {
        "api_key": "your-openai-api-key",
    },
    "agents": [
        {
            "name": "research_specialist",
            "instructions": "You are an expert researcher who synthesizes complex information clearly.",
            "specialization": "Research and knowledge synthesis",
        },
        {
            "name": "customer_support",
            "instructions": "You provide friendly, helpful customer support responses.",
            "specialization": "Customer inquiries",
        }
    ],
}

arq_ai = ArqAI(config=config)

async for response in arq_ai.process("user123", "What are the latest AI developments?"):
    print(response, end="")
                
