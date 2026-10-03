# Bypass Claude Code: Run It with OpenRouter

Use Claude Code with any OpenRouter model instead of an Anthropic login. Commands are given for **Linux / macOS** and **Windows**.

> **Security:** Never commit your real API key to Git. Keep it only in your local environment variables.

## Step 1: Install Claude Code

Works the same on Linux, macOS and Windows (Node.js and npm must be installed first):

```bash
npm install -g @anthropic-ai/claude-code
```

## Step 2: Create an OpenRouter API Key

- Create an OpenRouter account.
- Generate an API key (`sk-or-v1-...`).
- Add credits if you're using paid models.

## Step 3: Configure Claude Code to Use OpenRouter

### Linux / macOS

Add the following to your `~/.zshrc` or `~/.bashrc`:

```bash
export OPENROUTER_API_KEY="sk-or-v1-..."

export ANTHROPIC_BASE_URL="https://openrouter.ai/api"
export ANTHROPIC_AUTH_TOKEN="$OPENROUTER_API_KEY"
export ANTHROPIC_API_KEY=""
```

Restart your terminal (or run `source ~/.zshrc` / `source ~/.bashrc`) after saving.

### Windows (PowerShell)

Permanent (applies to new terminals):

```powershell
setx OPENROUTER_API_KEY "sk-or-v1-..."

setx ANTHROPIC_BASE_URL "https://openrouter.ai/api"
setx ANTHROPIC_AUTH_TOKEN "sk-or-v1-..."
setx ANTHROPIC_API_KEY ""
```

Close and reopen PowerShell after running these.

Current session only (temporary):

```powershell
$env:OPENROUTER_API_KEY = "sk-or-v1-..."

$env:ANTHROPIC_BASE_URL = "https://openrouter.ai/api"
$env:ANTHROPIC_AUTH_TOKEN = $env:OPENROUTER_API_KEY
$env:ANTHROPIC_API_KEY = ""
```

### Windows (Command Prompt / CMD)

```cmd
setx OPENROUTER_API_KEY "sk-or-v1-..."

setx ANTHROPIC_BASE_URL "https://openrouter.ai/api"
setx ANTHROPIC_AUTH_TOKEN "sk-or-v1-..."
setx ANTHROPIC_API_KEY ""
```

Close and reopen Command Prompt after running these.

## Step 4: Map Claude Model Classes to Your OpenRouter Model

Replace `<provider>/<model-name>` with the model ID from OpenRouter's model page.

### Linux / macOS

```bash
export ANTHROPIC_DEFAULT_HAIKU_MODEL="<provider>/<model-name>"
export ANTHROPIC_DEFAULT_SONNET_MODEL="<provider>/<model-name>"
export ANTHROPIC_DEFAULT_OPUS_MODEL="<provider>/<model-name>"
```

**(Optional)** Sub-agents:

```bash
export CLAUDE_CODE_SUBAGENT_MODEL="<provider>/<model-name>"
```

### Windows (PowerShell)

```powershell
setx ANTHROPIC_DEFAULT_HAIKU_MODEL "<provider>/<model-name>"
setx ANTHROPIC_DEFAULT_SONNET_MODEL "<provider>/<model-name>"
setx ANTHROPIC_DEFAULT_OPUS_MODEL "<provider>/<model-name>"
```

**(Optional)** Sub-agents:

```powershell
setx CLAUDE_CODE_SUBAGENT_MODEL "<provider>/<model-name>"
```

### Windows (Command Prompt / CMD)

```cmd
setx ANTHROPIC_DEFAULT_HAIKU_MODEL "<provider>/<model-name>"
setx ANTHROPIC_DEFAULT_SONNET_MODEL "<provider>/<model-name>"
setx ANTHROPIC_DEFAULT_OPUS_MODEL "<provider>/<model-name>"
setx CLAUDE_CODE_SUBAGENT_MODEL "<provider>/<model-name>"
```

Close and reopen your terminal afterwards.

## Step 5: Clear Any Existing Anthropic Login

If you've previously logged into Claude Code using Anthropic, run this inside Claude Code (all platforms):

```
/logout
```

Then restart Claude Code to avoid authentication conflicts.

## Step 6: Launch Claude Code and Verify

Start Claude Code (all platforms):

```bash
claude
```

Inside Claude Code, run:

```
/status
```

Verify that:

- Anthropic Base URL is `https://openrouter.ai/api`
- Auth Token is `ANTHROPIC_AUTH_TOKEN`

Finally, send a prompt and open the OpenRouter **Activity** dashboard to confirm the request is being processed by the model you selected.

## Troubleshooting

- **Variables not picked up:** open a new terminal window. `setx` and shell profile changes only apply to new sessions.
- **Check a variable on Linux / macOS:** `echo $ANTHROPIC_BASE_URL`
- **Check a variable on Windows (PowerShell):** `echo $env:ANTHROPIC_BASE_URL`
- **Check a variable on Windows (CMD):** `echo %ANTHROPIC_BASE_URL%`
