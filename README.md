# 🤖 HomeImproveAI - AI Agents

![LangChain](https://img.shields.io/badge/LangChain-0.1.0-FF6B00)
![LangGraph](https://img.shields.io/badge/LangGraph-0.0.5-4B32C3)
![LangSmith](https://img.shields.io/badge/LangSmith-0.1.0-10B981)
![Python](https://img.shields.io/badge/Python-3.11+-3776AB)

**Modular AI Agent System** for home improvement project generation, featuring multi-agent collaboration with tracing and evaluation.

## 🌟 Key Features

- 🧩 **Multi-Agent Workflows**: Orchestrated agents for specialized tasks
- 🔍 **Execution Tracing**: Full visibility into agent reasoning
- 📊 **Performance Analytics**: Track quality and costs
- 🚦 **Stateful Control Flow**: Complex task handling with LangGraph
- 🛠️ **Tool Integration**: External APIs + custom functions

## Architecture Overview

graph LR
    A[User Input] --> B(Design Generator)
    B --> C(Materials Agent)
    B --> D(Cost Estimator)
    C --> E[Home Depot API]
    D --> F[Price Scraping]
    C --> G((LangGraph))
    D --> G
    G --> H[Project Plan]
🛠️ Tech Stack
Component	Technology
Core Framework	LangChain 0.1.0
Orchestration	LangGraph 0.0.5
Monitoring	LangSmith
LLM	OpenAI GPT-4/Claude 3 (with fallback)
Vector Store	pgvector (PostgreSQL)
Tools	SerpAPI, Home Depot API, Wikipedia
🚀 Getting Started
Prerequisites
Python 3.11+

LangSmith API key

OpenAI/Anthropic API key(s)

Installation
bash
git clone https://github.com/your-username/homeimproveai-agents.git
cd homeimproveai-agents
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
Configuration
bash
cp .env.example .env
Edit .env with your:

ini
OPENAI_API_KEY=sk-...
LANGSMITH_API_KEY=ls_...
SERPAPI_API_KEY=...
🧩 Agent Modules
Core Agents
Agent	Description	Tools
DesignGenerator	Creates design concepts	DALL-E, Stable Diffusion
MaterialsAgent	Generates shopping lists	Home Depot API, WikiHow
CostEstimator	Calculates project costs	SerpAPI, PriceScraper
InstallGuideAgent	Produces step-by-step instructions	Claude 3, DIY knowledge base
Example Workflow
python
from langgraph.graph import Graph
from agents import DesignGenerator, MaterialsAgent

# Define workflow
workflow = Graph()
workflow.add_node("generate", DesignGenerator.run)
workflow.add_node("materials", MaterialsAgent.run)
workflow.add_edge("generate", "materials")

# Compile
chain = workflow.compile()
📊 LangSmith Integration
python
# Enable tracing
import os
from langsmith import Client

os.environ["LANGCHAIN_TRACING_V2"] = "true"
client = Client()
View traces at: https://smith.langchain.com

🧪 Testing Agents
bash
# Run unit tests
pytest tests/

# Test specific agent
python -m tests.test_materials_agent
🏗️ Project Structure
text
agents/
├── core/
│   ├── design_generator.py   # Transform prompts → designs
│   ├── materials_agent.py    # Generate shopping lists
│   └── cost_estimator.py     # Calculate project costs
├── workflows/
│   ├── home_improvement.py   # LangGraph state machine
│   └── evaluation.py         # Agent quality checks
├── tools/
│   ├── hardware_store.py     # Home Depot API wrapper
│   └── price_scraper.py     # Web scraping utilities
└── tests/
💡 Example Usage
python
from agents.workflows import home_improvement_chain

result = home_improvement_chain.run(
    input="I want to remodel my kitchen in mid-century modern style"
)
print(result["materials_list"])
📈 Performance Monitoring
python
# Log custom metrics
client.create_feedback(
    run_id="...",
    key="cost_accuracy",
    score=0.95,
    comment="Actual cost within 5% of estimate"
)
🐳 Docker Deployment
dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["python", "-m", "agents.main"]
🤝 Contributing
Fork the repository

Create agent test cases in /tests

Add LangSmith traces for new workflows

Submit PR with:

Documentation updates

Type hints

Benchmark results

📄 License
MIT - See LICENSE
