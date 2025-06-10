# Purpose
This repo contains AI agent logic for a DIY Home Improvement app. It is structured to work with LangChain, LangGraph, and LangSmith.

# Agent Goals
- Understand user intent from text/image.
- Generate 4 decorative renderings.
- Create a detailed decoration plan.
- Output shopping list, installation guide, estimated cost & time.

# Code Organization
- `agents/`: Modular agents as LangChain tools or functions.
- `graphs/`: LangGraph workflows combining these agents.
- `tools/`: External API wrappers (image generation, material DB).
- `prompts/`: Prompt templates (Jinja2 or plain text).
- `tests/`: Unit tests for agents and flow.

# Expectations from Copilot
- Help structure modular agent functions.
- Suggest LangChain tools and LangGraph graph logic.
- Assist with prompt design and validation schemas.
- Write JSON schemas for plan outputs.
