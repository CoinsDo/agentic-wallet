<p align="center"><img src="logo.svg" alt="CoinsDo" width="240"></p>

# CoinWallet スキル

[English](../../README.md) · [简体中文](README.zh-Hans.md) · [繁體中文](README.zh-Hant.md) · 日本語

**Installing with an AI agent:** the agent runs the "Install steps" in the English [README.md](../../README.md).

AI エージェントが CoinWallet の MPC ウォレットで暗号資産を受け取り、送金できるようになります。送金はすべて、あなたが CoinWallet アプリで承認します。

次の一文をそのまま、エージェントのチャットに貼り付けてください（Claude Code、Codex、Hermes、OpenClaw のどれでも使えます）。

```text
Install the CoinWallet skill from https://github.com/CoinsDo/agentic-wallet
```

## 使い方

1. 上の一文をエージェントのチャットに貼り付けます。
2. エージェントがスキルと CoinsDo ウォレットサービスをインストールします。ほかに入れるものはありません。macOS か Linux と、Python 3.9 以降が必要です。
3. エージェントが CoinWallet アプリのリンク（iPhone と Android）と、アプリでウォレットを作る手順を教えてくれます。
4. アプリに 6 文字の招待コードが表示されます。60 分以内にチャットに貼り付けてください。Claude Code か Codex では、新しいチャットを開いてから貼り付けます。
5. アプリで「作成」をタップし、続けて「MPCキーシャードを取得する」をタップします。これでウォレットの完成です。

## こんなことを頼めます

ふだんの言葉で頼んでください。たとえば：

- 「USDT のアドレスを教えて」
- 「ウォレットにいくら入ってる？」
- 「新しい TRX アドレスを作って」
- 「10 USDT を TX… に送って」
- 「私の送金を承認して」（あなたがアプリで始めた送金）
- 「送金履歴を見せて」
- 「CoinWallet をアップデートして」

## 送金はすべてアプリで承認します

エージェントが勝手に送金することはできません。送金には 2 つのステップがあります。

1. **チャットで：** エージェントが金額、通貨、チェーン、ウォレット、送金先の完全なアドレスを 1 行で見せます。よく確認してください。「はい」か「yes」と返すと先に進みます。それ以外の返事では何も送られません。
2. **アプリで：** 「Activity」→「未確認」を開き、その送金を開きます。**完全なアドレスが一致しているか確認してください。** そのあと 15 分以内に「承認」をタップします。やめたいときは「拒否」をタップするか、15 分待てば期限切れになります。

新しいアドレスにも、アプリでの承認が必要です（「Activity」にある新しいアドレスの申請）。

アプリでは承認待ちの送金が「未確認」と表示されます。これは「承認待ち」という意味です。

## 知っておくこと

- **Mac でアップデートしたあと：** 「security wants to use … com.coinsdo.wallet.secure」というポップアップが出て、Mac のログインパスワードを求められます。パスワードを入力して **Allow**（許可）をクリックしてください。**Deny**（拒否）は絶対にクリックしないでください。「Keychain Not Found」ダイアログに **Reset To Defaults** が出たら、**Cancel**（キャンセル）をクリックしてください。
- **Mac の既知の問題（ウォレットサービス 1.0.9）：** あなたのユーザーで動くほかのプログラムが、キーチェーン内のエージェントの鍵シェアを読み取れます。送金はすべて、引き続き CoinWallet アプリでのあなたの承認が必要です。CoinsDo が修正中です。
- **OpenClaw と DeepSeek Flash 4.1：** 一度だけ `openclaw config set agents.defaults.thinkingDefault medium` を実行してください。設定しないと、エージェント自身の思考が返信に出ることがあります。
- **Linux：** マスターキーのファイルとウォレットのデータフォルダは、絶対に削除したり置き換えたりしないでください。新しいサーバーに移るときは、ウォレットの Room を作り直します。
- **テストネット：** アプリには最初メインネットだけが表示されます。先にテストネットで試したいときは、エージェントに聞いてください。

## 手動でインストール

エージェントがインストールしてくれた場合は不要です。使っている Host を開いてください。

<details>
<summary>Claude Code</summary>

インストール：

```sh
claude plugin install coinwallet --marketplace CoinsDo/agentic-wallet
```

そのあと新しいチャットを開いて、「Set up the CoinWallet service.」と頼みます。

アンインストール（先に下の警告を読んでください）：

```sh
claude mcp remove --scope user coinwallet
claude plugin marketplace remove coinsdo
```

</details>

<details>
<summary>Codex</summary>

インストール：

```sh
codex plugin marketplace add CoinsDo/agentic-wallet && codex plugin add coinwallet@coinsdo
```

そのあと新しいチャットを開いて、「Set up the CoinWallet service.」と頼みます。

アンインストール（先に下の警告を読んでください）：

```sh
codex mcp remove coinwallet
codex plugin remove coinwallet@coinsdo && codex plugin marketplace remove coinsdo
```

</details>

<details>
<summary>Hermes</summary>

インストール：

```sh
hermes skills install CoinsDo/agentic-wallet/skills/coinwallet --yes
```

そのあと「Set up the CoinWallet service.」と頼みます。

アンインストール（先に下の警告を読んでください）：

```sh
hermes config unset mcp_servers.coinwallet
hermes skills uninstall coinwallet --yes
```

</details>

<details>
<summary>OpenClaw</summary>

インストール：

```sh
openclaw plugins install coinwallet --marketplace CoinsDo/agentic-wallet --force --accept-capabilities
```

そのあと「Set up the CoinWallet service.」と頼みます。

アンインストール（先に下の警告を読んでください）：

```sh
openclaw mcp unset coinwallet
openclaw plugins uninstall coinwallet --force
```

</details>

> [!WARNING]
> **アンインストールの前に：** ウォレットに資産があるうちは、ウォレットのデータフォルダとそのマスターキーを絶対に削除しないでください。そこにエージェントのキーシャードが入っています。これがないとエージェントは署名できず、2/2 のウォレットはまったく送金できなくなります。スキルをアンインストールしても、これらは残ります。
>
> - macOS：`~/Library/Application Support/coinsdo-wallet-mcp`（マスターキーは Mac のキーチェーンに「com.coinsdo.wallet.secure」として入っています。削除しないでください）
> - Linux：`~/.config/coinsdo-wallet-mcp`（マスターキーはその中の `.key/master.key` です）
>
> 先にアプリで資産を移しておいてください。
