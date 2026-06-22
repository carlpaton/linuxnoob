curl -fsSL https://ollama.com/install.sh | sh

ollama run gemma4:e4b

OLLAMA_LLM_LIBRARY=vulkan ollama run qwen3.6:27b