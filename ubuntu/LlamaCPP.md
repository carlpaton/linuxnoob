# Local Monitor
nvtop

# Run llama.cpp server (Vulkan)

This command starts the `llama.cpp` HTTP server in a Docker container with GPU acceleration (Vulkan), loads a GGUF model from your local `models` folder, and exposes the API on port `8080`.

```bash
sudo docker run --rm -it \
	-v ./models:/models \
	--device /dev/dri:/dev/dri \
	-p 8080:8080 \
	ghcr.io/ggml-org/llama.cpp:server-vulkan \
	-m /models/Qwen3.6-27B-Q4_1.gguf -ngl 999 \
	--n-cpu-moe 35 \
	--no-mmap --mlock \
	--cache-type-k q8_0 --cache-type-v q8_0 \
	-c 90000 --host 0.0.0.0
```

## What each part does

- `docker run --rm -it`
	- `--rm`: remove container when it exits.
	- `-it`: interactive terminal session.
- `-v ./models:/models`
	- Mount local `./models` directory into container at `/models` so the model file is accessible.
- `--device /dev/dri:/dev/dri`
	- Pass host GPU device nodes into the container (required for Vulkan on Linux).
- `-p 8080:8080`
	- Publish container port `8080` to host port `8080`.
- `ghcr.io/ggml-org/llama.cpp:server-vulkan`
	- Use the prebuilt `llama.cpp` image that includes the Vulkan-enabled server binary.
- `-m /models/qwen2.5-coder-14b-instruct-q5_k_m.gguf`
	- Load this GGUF model file.
- `-ngl 999`
	- Offload as many layers as possible to GPU.
- `--n-cpu-moe 35`
	- Set number of CPU threads used for MoE experts/routing work.
- `--no-mmap --mlock`
	- `--no-mmap`: read model into regular memory instead of mmap.
	- `--mlock`: lock model pages in RAM to reduce swapping.
- `--cache-type-k q8_0 --cache-type-v q8_0`
	- Select KV cache formats (performance/memory tradeoff options).
- `-c 90000`
	- Set context length to `90000` tokens 
	- Roughly `60,000`-`70,000` words in English text (rule of thumb: 1 token ~= 0.75 words), or around `120`-`140` single-spaced pages.
- `--host 0.0.0.0`
	- Bind server on all interfaces so it is reachable from other machines.

## Result

After startup, the API is available at `http://localhost:8080` (and from your LAN if firewall rules allow it).

## Where to download models

https://huggingface.co/models?search=GGUF

# VS Code
- Ctrl+Shift+P -> `Chat: Manage Language Models`
- Add models -> Custom Endpoint
- Group Name -> `llama.cpp`
- API Key -> empty

```
[
	{
		"name": "llama.cpp",
		"vendor": "customendpoint",
		"apiType": "chat-completions",
		"models": [
			{
				"id": "llama.cpp",
				"name": "llama.cpp",
				"url": "http://localhost:8080/v1",
				"toolCalling": true,
				"vision": true,
				"maxInputTokens": 128000,
				"maxOutputTokens": 16000
			}
		]
	}
]
```