# AI / ML & Data Science

**Role:** AI models, intelligent systems, predictive modeling, data pipelines (ETL).

## MLOps & Experiment Tracking
| Project | ★ | License | Link | Role |
|---|---|---|---|---|
| `mlflow/mlflow` | 26.7k | Apache-2.0 | https://github.com/mlflow/mlflow | #1 AI/ML experiment tracking, model registry, LLM observability |
| `vllm-project/vllm` | 85.9k | Apache-2.0 | https://github.com/vllm-project/vllm | High-throughput LLM inference + serving (PagedAttention) |
| `ray-project/ray` | 42.2k | Apache-2.0 | https://github.com/ray-project/ray | Distributed AI compute — training, serving, RL |
| `iterative/dvc` | 14k | Apache-2.0 | https://github.com/iterative/dvc | Data version control for ML pipelines |
| `bentoml/BentoML` | 10k | Apache-2.0 | https://github.com/bentoml/BentoML | Python-native model serving framework |

## LLM Routing & Gateway
| Project | ★ | License | Link | Role |
|---|---|---|---|---|
| `BerriAI/litellm` | 20k | MIT | https://github.com/BerriAI/litellm | OpenAI-proxy for 100+ LLMs, routing, fallbacks, spend tracking |

## Agent Frameworks & Model Workflows
| Project | ★ | License | Link |
|---|---|---|---|
| `microsoft/autogen` | 59.6k | CC-BY-4.0 | https://github.com/microsoft/autogen |
| `langchain-ai/langgraph` | 37k★ | MIT | https://github.com/langchain-ai/langgraph |
| `FoundationAgents/MetaGPT` | 69.3k | MIT | https://github.com/FoundationAgents/MetaGPT |
| `zai-org/CogVideo` (CogVideoX) | 12.9k | — | https://github.com/zai-org/CogVideo (text→video model) |
| `QwenLM/Qwen2.5-Omni` | 4k★ | — | https://github.com/QwenLM/Qwen2.5-Omni (multimodal) |

## Why
MLflow is the missing brain of the AI company — experiment tracking, model registry, LLM observability, AI gateway.
vLLM serves models at production scale (85.9k★). Ray distributes compute. LiteLLM routes across providers.
LangGraph builds resilient AI workflows. CogVideoX generates B-roll; Qwen-Omni does multimodal generation.

## Integration
AI ML Engineer tracks experiments in MLflow → serves models via vLLM/BentoML → manages data via DVC → routes via LiteLLM → LangGraph orchestrates → CogVideoX feeds Video dept.
