# ✈️ Multi-Agent Travel Planner on AWS
### Event-Driven AI Agents using Choreography & Orchestration Patterns

> A hands-on implementation of scalable multi-agent AI architecture using AWS, Strands Agents, Amazon Bedrock, AWS Lambda, Amazon EventBridge, AWS Step Functions, Amazon S3, SNS, and Amazon CloudWatch.

---

## 🚀 Project Overview

This project explores how multiple specialized AI agents can collaborate to solve a complex travel-planning problem.

Instead of building a single monolithic AI agent, the system decomposes the travel-planning workflow into specialized agents:

- ✈️ **Flight Agent** — handles flight-related recommendations
- 🏨 **Hotel Agent** — recommends hotels based on destination and budget
- 🌤️ **Weather Agent** — provides destination weather information
- 🧠 **Planner Agent** — coordinates the overall travel request

The project implements and compares two fundamental multi-agent communication patterns:

1. **Event-Driven Choreography**
2. **Centralized Orchestration**

The same travel-planning problem can therefore be solved using two different architectural approaches.

---

# 🎯 Objectives

The project was designed to demonstrate:

- Multi-agent system design
- Specialized AI agents
- Event-driven architecture
- Agent-to-agent communication
- Workflow orchestration
- Asynchronous processing
- Persistent agent context
- Tool calling
- AWS serverless architecture
- Observability through CloudWatch
- Failure isolation and modularity
- Comparison between decentralized and centralized coordination

---

# 🏗️ High-Level Architecture

```text
                         ┌───────────────────────┐
                         │      Travel User      │
                         └───────────┬───────────┘
                                     │
                                     ▼
                         ┌───────────────────────┐
                         │   Travel Request      │
                         │   bookingID, budget,  │
                         │   destination, dates  │
                         └───────────┬───────────┘
                                     │
                         ┌───────────▼───────────┐
                         │   Planner Agent       │
                         │  Strands + Bedrock    │
                         └───────────┬───────────┘
                                     │
                  ┌──────────────────┴──────────────────┐
                  │                                     │
                  ▼                                     ▼
        ┌───────────────────┐                 ┌────────────────────┐
        │  CHOREOGRAPHY    │                 │   ORCHESTRATION    │
        │                   │                 │                    │
        │   EventBridge     │                 │   Step Functions   │
        │   Event Bus       │                 │   Workflow         │
        └─────────┬─────────┘                 └──────────┬─────────┘
                  │                                      │
        ┌─────────┼─────────┐                  ┌─────────┼─────────┐
        ▼         ▼         ▼                  ▼         ▼         ▼
     Flight    Hotel     Weather             Flight    Hotel    Weather
     Agent     Agent      Agent              Agent     Agent     Agent
        │         │         │                  │         │         │
        └─────────┼─────────┘                  └─────────┼─────────┘
                  │                                      │
                  ▼                                      ▼
          EventBridge Events                       Workflow Results
                  │                                      │
                  └──────────────────┬───────────────────┘
                                     ▼
                           ┌─────────────────────┐
                           │ Final Travel Plan   │
                           └─────────────────────┘
