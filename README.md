# AgentHP Server

AgentHP の iPhone アプリとウィジェットに、Mac 上の Codex 使用状況を渡すサーバーです。
ソースコードはこの配布リポジトリには含まれません。

## 必要なもの

- macOS の Apple Silicon または Intel Mac
- ChatGPT アカウントでログイン済みの [Codex CLI](https://developers.openai.com/codex/cli/)
- iPhone と Mac の両方で接続済みの Tailscale

## インストール

1. [Releases](https://github.com/reirei-lab/agent-hp-server/releases) から、Apple Silicon なら `arm64`、Intel Mac なら `x64` の ZIP をダウンロードします。
2. ZIP を展開し、ターミナルでバイナリを起動します。以下の `100.x.y.z` は Mac の Tailscale IPv4 アドレスに置き換えてください。

   ```sh
   HOST=100.x.y.z PORT=8787 ./agent-hp-server-macos-arm64
   ```

   Intel Mac では末尾を `./agent-hp-server-macos-x64` にします。ターミナルを閉じるとサーバーも終了します。
3. iPhone の AgentHP アプリの設定で `http://100.x.y.z:8787` を接続先に指定します。

Mac 上で `curl http://100.x.y.z:8787/v1/usage` を実行し、JSON が返れば接続できています。Codex CLI をインストール・ログインしたユーザーと同じmacOSユーザーでサーバーを起動してください。Mac がスリープするとウィジェットは更新できません。

履歴は `~/Library/Application Support/AgentHP/` に保存します。5分おきに観測し、サーバー停止中のデータは補完されません。API は `/v1/usage` と `/v1/token-usage` です。

Tailscale IPv4 アドレスへの待ち受けでは追加のアクセストークンは不要です。Tailscale 以外のアドレスで待ち受ける場合は `ACCESS_TOKEN` が必須です。公開インターネットに直接ポートを開けないでください。

各リリースの `SHA256SUMS` でダウンロードしたZIPを検証できます。

問い合わせ: hiragram+support@gmail.com
