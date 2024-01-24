# helix-gpt

Code completion LSP for Helix utilising the OpenAI chat API.

## Goals
- No dependencies
- Straight completion. No code improvements/explanations.
- No key bindings, just automatic completion suggestions.

## Usage

### Configuration
You can configure helix-gpt by exposing either the environment variables below, or passing the command line options directly to helix-gpt in the helix configuration step.

Environment vars
```
OPENAI_MODEL=gpt-3.5-turbo # Optional
OPENAI_KEY=123 # required
LOG_FILE=/app/debug-helix-gpt.log # Optional
OPENAI_CONTEXT="A terrible code completion assistant" # Optional
```

Args (add to `command = "helix-gpt"` below)

```--openaiModel gpt-3.5-turbo --openaiKey 123 --logFile /app/debug-helix-gpt.log --openaiContext "A terrible code completion assistant"```

### Helix configuration

TypeScript example `.helix/languages.toml` tested with helix 23.10 (older versions may not support multiple LSPs)

```
[language-server.gpt]
command = "helix-gpt"

[language-server.ts]
command = "typescript-language-server"
args = ["--stdio"]
language-id = "javascript"

[[language]]
name = "typescript"
auto-format = true
indent = { tab-width = 2, unit = " " }
language-servers = [
    "ts",
    "gpt"
]
```

If you choose not to use the precompiled binary, modify the first command to be:
```
[language-server.gpt]
command = "bun"
args = ["run", "/app/helix-gpt.js"]
```

### helix-gpt install

This was made to run with [Bun](https://bun.sh/), but you can find a binary below with the runtime included.

Without bun
`wget -o /usr/bin/helix-gpt `

With bun (must use the args option in the previous step)
`wget `

