# Install
- Download AppImage from https://lmstudio.ai/
- sudo apt update
- sudo apt install libfuse2
- chmod +x LM-Studio-0.4.13-1-x64.AppImage
- Then run from Downloads as ./LM-Studio-0.4.13-1-x64.AppImage --no-sandbox

# Config & Model
- Download model `Qwen3.6-27B-Q4_K_M.gguf` (16.5gb)
- Set context to 54000 (this will stay within the GPUs 24GB)

# Harness
- Cline, this should then keep the context managed
