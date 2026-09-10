# agentguard-sdk

Runtime security & observability guard for AI agents. Wraps LLM calls and
tool calls, checks them against policy before execution, and streams
telemetry to your AgentGuard collector.

## Install

```bash
pip install agentguard-sdk
```

## Quick start

```python
from agentguard_sdk import AgentGuard

guard = AgentGuard(
    collector_url="https://YOUR_AGENTGUARD_HOST",
    api_key="YOUR_AGENTGUARD_API_KEY",
    agent_id="my-agent",
)

@guard.guard_llm_call
def call_model(prompt, model="gpt-5"):
    from openai import OpenAI
    return OpenAI().responses.create(model=model, input=prompt)

@guard.guard_tool_call("search_customer")
def search_customer(query):
    return your_search_function(query)
```

See https://app.cerbereag.site for the dashboard, policy docs, and other
framework integrations (MCP, LangGraph, CrewAI, Composio, HTTP gateway).

## Optional extras

```bash
pip install "agentguard-sdk[signing]"  # verify signed policy decisions (Ed25519)
pip install "agentguard-sdk[pii]"      # advanced PII detection via Presidio
```
