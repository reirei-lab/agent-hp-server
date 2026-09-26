# AgentHP Server

AgentHP Server provides the Codex usage data from your Mac to the AgentHP iPhone app and widgets. This distribution repository contains binaries, not the server source code.

## Requirements

- An Apple Silicon or Intel Mac running macOS
- [Homebrew](https://brew.sh/)
- [Codex CLI](https://developers.openai.com/codex/cli/) installed and signed in with your ChatGPT account
- A network path between your Mac and iPhone (for example, Tailscale or a local network)

## Install and run

1. Install the server from the [reirei-lab Homebrew tap](https://github.com/reirei-lab/homebrew-tap). Homebrew selects the correct binary for your Mac.

   ```sh
   brew install reirei-lab/tap/agent-hp-server
   ```

2. Start the server in Terminal. Replace `100.x.y.z` with the Mac IP address you want the server to listen on. This example uses a Tailscale IPv4 address; you can use a LAN address instead.

   ```sh
   HOST=100.x.y.z agent-hp-server
   ```

   The server stops when you close Terminal.
3. In the AgentHP iPhone app, set the server URL to `http://100.x.y.z:8787`.

To install a newer release later, run `brew update && brew upgrade reirei-lab/tap/agent-hp-server`. Homebrew verifies the download against the SHA-256 hash in the tap. You do not need Node.js or Bun to run the server.

To check the connection on your Mac, run `curl http://100.x.y.z:8787/v1/usage`. It should return JSON. Run the server under the same macOS user account that installed and signed in to Codex CLI. Widgets cannot refresh while your Mac is asleep.

The server samples usage about every five minutes and stores history in `~/Library/Application Support/AgentHP/`. It cannot fill gaps while it is stopped. The API endpoints are `/v1/usage` and `/v1/token-usage`.

The API has no application-level authentication. By default, it listens only on `127.0.0.1`; setting `HOST` makes it available through the network interface you choose. Use your network's access controls or firewall to decide which devices can connect. Do not expose the port directly to the public internet.

Signed and notarized binaries are also available under [Releases](https://github.com/reirei-lab/agent-hp-server/releases) for manual installation.

Support: hiragram+support@gmail.com
