# Colab-mcp

An MCP server for bridging your local agent to a Colab session in the browser.

## This fork

This repository is a fork of [googlecolab/colab-mcp](https://github.com/googlecolab/colab-mcp). The upstream installation example, Discussions links and contribution policy below refer to the upstream project.

The `uvx` configuration below installs **googlecolab/colab-mcp**, not the code in `appletree-tech/colab-mcp`. To develop or run this checkout, use the local-source instructions in this section. Review branch changes before treating this fork as interchangeable with upstream.

### Requirements and local source

- A local MCP client with `notifications/tools/list_changed` support
- `uv`
- Python **3.13 or newer**, as declared in [pyproject.toml](pyproject.toml)
- A Colab session in the browser

```sh
git clone https://github.com/appletree-tech/colab-mcp.git
cd colab-mcp
uv sync
uv run colab-mcp
```

The local command starts the MCP server; the client and browser session still need to be connected for Colab interaction. For a client configuration using this checkout, use the local `uv run colab-mcp` command with the repository as its working directory, as illustrated in the development configuration below.

Local checks:

```sh
uv run pytest
uv run ruff check .
```

Logs are written to a temporary `colab-mcp-logs-*` directory by default. Use `uv run colab-mcp --log /path/to/log-directory` to choose a log directory.

## Supported Clients
This MCP server requires client support for `notifications/tools/list_changed` and for the client to be running locally on your device. 

Popular clients that fit these criteria include:
- Gemini CLI
- Claude Code
- Windsurf


## Setup

- Install `uv` (`pip install uv`)
- Configure for usage (eg for mcp.json style services):

```
...
  "mcpServers": {
    "colab-mcp": {
      "command": "uvx",
      "args": ["git+https://github.com/googlecolab/colab-mcp"],
      "timeout": 30000
    }
  }
...
```

(If you have a non-standard default package index (**Googlers**), you may also need to add `--index https://pypi.org/simple`)

## Issues & Discussions

We are using GitHub [discussions](https://github.com/googlecolab/colab-mcp/discussions) as the
place for issue discussion and feature requests. As discussions mature into action items, we
will add those items as issues. This helps us ensure that issues in the issue tracker are
well-understood, deduplicated, and actionable. For these reasons, **please do <u>NOT</u> open
issues directly.** 

## Contributing 
We unfortunately don't have the bandwidth to support review of external contributions, and we 
don't want user PRs to languish, so we aren't accepting any external contributions right now.

If you have a great idea or pain point, we would love to hear about it on our 
[discussions](https://github.com/googlecolab/colab-mcp/discussions) page - the preferred place 
for issue discussion and feature requests.

## Internal - For Colab Developers

### Prerequisites

- `uv` is required (`pip install uv`)
- Configure git hooks to run repo presubmits

```shell
git config core.hooksPath .githooks
```

### Gemini CLI setup

```
...
  "mcpServers": {
    "colab-mcp": {
      "command": "uv",
      "args": ["run", "colab-mcp"],
      "cwd": "/path/to/github/colab-mcp",
      "timeout": 30000
    }
  }
...
```
