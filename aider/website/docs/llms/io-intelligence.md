---
parent: Connecting to LLMs
nav_order: 500
---

# IO Intelligence

Aider can connect to models served by [IO Intelligence](https://io.net),
io.net's model inference platform.
It exposes a standard **OpenAI-compatible** endpoint at:

```
https://api.intelligence.io.solutions/api/v1
```

You'll need an IO Intelligence API key, which you can create on
[io.net](https://io.net/docs/guides/intelligence/api-keys-and-secrets).

First, install aider:

{% include install.md %}

---

## Configure your environment

```bash
# macOS/Linux
export OPENAI_API_BASE=https://api.intelligence.io.solutions/api/v1
export OPENAI_API_KEY=***

# Windows (PowerShell)
setx OPENAI_API_BASE https://api.intelligence.io.solutions/api/v1
setx OPENAI_API_KEY <key>
# …restart the shell after setx commands
```

---

## Discover available models

IO Intelligence serves open models with Hugging Face-style ids
(`<org>/<model-name>`).
List the available models with:

```bash
curl -s https://api.intelligence.io.solutions/api/v1/models | jq -r '.data[].id'
```

Each returned ID can be used with aider by **prefixing it with `openai/`**:

```bash
aider --model openai/meta-llama/Llama-3.3-70B-Instruct
# or
aider --model openai/moonshotai/Kimi-K2.7-Code
```

The leading `openai/` tells aider to send the request to your
`OPENAI_API_BASE`; the rest of the string, e.g.
`meta-llama/Llama-3.3-70B-Instruct`, is sent to IO Intelligence as the
model id.

---

## Quick start

```bash
# change into your project
cd /to/your/project

# work with an IO Intelligence model
aider --model openai/meta-llama/Llama-3.3-70B-Instruct
```

---

## Optional config file (`~/.aider.conf.yml`)

```yaml
openai-api-base: https://api.intelligence.io.solutions/api/v1
openai-api-key:  "<key>"
model:           openai/meta-llama/Llama-3.3-70B-Instruct
weak-model:      openai/deepseek-ai/DeepSeek-V4.1-Flash
show-model-warnings: false
```

---

## FAQ

* Calls made through aider are billed through your io.net account.
* Aider's default edit formats (`diff`, `whole`) are plain text and work
  with any chat model. The opt-in function-calling edit formats
  (`whole-func`, `diff-func`) additionally rely on tool calls.
* See the [model warnings](warnings.html)
  section for information on warnings which will occur
  when working with models that aider is not familiar with.
