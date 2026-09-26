# AgentHP Server

AgentHP Server provides the Codex usage data from your Mac to the AgentHP iPhone app and widgets. This distribution repository contains binaries, not the server source code.

## Requirements

- An Apple Silicon or Intel Mac running macOS
- [Codex CLI](https://developers.openai.com/codex/cli/) installed and signed in with your ChatGPT account
- Tailscale connected on both your Mac and iPhone

## Install and run

1. Download the `arm64` ZIP for an Apple Silicon Mac or the `x64` ZIP for an Intel Mac from [Releases](https://github.com/reirei-lab/agent-hp-server/releases).
2. Extract the ZIP and run the binary in Terminal. Replace `100.x.y.z` with your Mac's Tailscale IPv4 address.

   ```sh
   HOST=100.x.y.z PORT=8787 ./agent-hp-server-macos-arm64
   ```

   On an Intel Mac, use `./agent-hp-server-macos-x64` instead. The server stops when you close Terminal.
3. In the AgentHP iPhone app, set the server URL to `http://100.x.y.z:8787`.

To check the connection on your Mac, run `curl http://100.x.y.z:8787/v1/usage`. It should return JSON. Run the server under the same macOS user account that installed and signed in to Codex CLI. Widgets cannot refresh while your Mac is asleep.

The server samples usage about every five minutes and stores history in `~/Library/Application Support/AgentHP/`. It cannot fill gaps while it is stopped. The API endpoints are `/v1/usage` and `/v1/token-usage`.

No additional access token is required when listening on a Tailscale IPv4 address. Listening on any other non-loopback address requires `ACCESS_TOKEN`. Do not expose the port directly to the public internet.

Each release includes `SHA256SUMS` so you can verify the downloaded ZIP files.

Support: hiragram+support@gmail.com
