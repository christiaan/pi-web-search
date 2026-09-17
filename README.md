# pi-web-search

Web search and fetch tools for the [pi](https://github.com/mariozechner/pi-coding-agent/) coding
agent. Uses your Ollama instance's `web_search` and `web_fetch` APIs.

This is a community fork/maintainer version of [`@ollama/pi-web-search`](https://www.npmjs.com/package/@ollama/pi-web-search).
The original package hard-coded `http://localhost:11434`, which broke whenever your Ollama server runs
on a non-default host (a VM, another workstation, etc.). This version honors the `OLLAMA_HOST`
environment variable so remote instances work out of the box.

## Features

- `web_search` – Search the web for real-time information
- `web_fetch` – Fetch and extract content from web pages
- `OLLAMA_HOST` support – Works with Ollama on any host, not just localhost

## Requirements

- pi coding agent installed
- Ollama running (locally or remotely)
- Web search/fetch endpoints enabled on your Ollama instance
- For web search: an authenticated user, usually via `ollama signin`

## Installation

### From GitHub / git

```bash
pi install git:github.com/christiaan/pi-web-search
```

### From a local path (development)

```bash
pi install ./path/to/pi-web-search
```

## Configuration

Set the `OLLAMA_HOST` environment variable so the tools talk to wherever Ollama is running:

```bash
export OLLAMA_HOST="http://192.168.1.6:11434"   # remote host instead of localhost
```

If `OLLAMA_HOST` is unset, the tools fall back to `http://localhost:11434`.
`OLLAMA_HOST` should point at the Ollama base URL **without** the `/v1` suffix — it is used as
`<OLLAMA_HOST>/api/experimental/web_search` and `<OLLAMA_HOST>/api/experimental/web_fetch`.

## Troubleshooting

If you get connection errors:

1. Make sure Ollama is running/reachable (`ollama serve`).
2. Verify `OLLAMA_HOST` matches where your Ollama instance is listening.
3. Confirm web search/fetch is enabled on your Ollama configuration
   (the endpoints live under `/api/experimental/`).
4. Web search may require authentication — run `ollama signin` on the machine running Ollama.

## Reinstalling into pi

After this package is updated, reinstall it so pi picks up the new code:

```bash
pi install git:github.com/christiaan/pi-web-search
```

## License

MIT
