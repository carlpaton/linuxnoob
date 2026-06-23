## Notes
- CC currently wont work with LM Studio as thats a OpenAI-compatible api with partial / experimental Anthopic support
- CC should work with litellm

## Install CC

curl -fsSL https://claude.ai/install.sh | bash

echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

which claude

claude --help

## Run LM Studio
[Run LM Studio](./lmstudio.md)


## Config (LM Studio ~ Not working)
nano ~/.bashrc

The add

export ANTHROPIC_BASE_URL=http://localhost:1234
export ANTHROPIC_AUTH_TOKEN=lmstudio
export CLAUDE_CODE_ATTRIBUTION_HEADER=0

-- save
source ~/.bashrc

-- test value
echo $ANTHROPIC_BASE_URL

