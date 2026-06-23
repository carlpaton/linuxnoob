## Notes
This is just a proxy, LM Studio runs the model

## Install

sudo apt install pipx
pipx ensurepath
pipx install litellm

## Run

litellm --help

litellm --model openai/qwen2.5-coder-32b-instruct --api_base http://localhost:1234/v1 --port 4000