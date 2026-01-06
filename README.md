# Opencode Configuration

This repository contains my personal Opencode configuration. If you are copying these files, you will need to follow these steps to authenticate the plugins and install dependencies.

## Setup

### 1. Install Antigravity
You must have [`antigravity`](https://antigravity.google/) installed for the Google models and the authentication plugin to function correctly:

### 2. Authenticate Plugins
Run the following commands to authenticate the two core authentication plugins:

```bash
opencode auth openai-codex # Requires an OpenAI ChatGPT subscription
opencode auth antigravity
```

## Features

- **Custom Agents**:
  - `opencode-insight-curator`: Background agent that extracts durable rules and proposes permanent configuration changes.
  - `web-qa-automation`: specialized agent for Playwright-based web testing.
- **Pre-configured Permissions**: Extensive list of allowed bash commands for a smoother workflow.
- **Model Presets**: Pre-configured reasoning models for OpenAI and Google (via Antigravity).

