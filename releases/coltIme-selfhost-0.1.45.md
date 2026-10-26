Windows x64向けのSelfHost実験版です。最適化と診断ログを有効にしています。MSIは未署名です。

## 今回の内容

- 入力更新のたびに繰り返していた、確定文脈の形態素解析を予測候補の通常変換行で再利用します。辞書・確定文脈・ユーザー辞書revisionが変わると再解析します。
- この最適化で、報告されているキー欠落・母音欠落が解消したとは確認していません。実アプリでの入力確認が必要です。
- 製品辞書は2026-10-26 r5です。803,933語、word bigram 6,000,000件、word trigram 12,000,000件、phrase 81,489件を含みます。

## 識別情報

- MSI: `0.1.45`、SelfHost、Windows x64、最適化済み、診断有効、未署名
- MSIサイズ: `64,849,895` bytes
- MSI SHA-256: `feaef67c962fa82b58c557db46fbbdc7ceacef496c8c7c49b6545682070d6adf`
- ソース: `879e43f0bd9407602581bcbd4cbdaa8bfe975e68`
- build: `20261026-160546-892`
- 辞書: `coltIme-dictionary-20261026-r5`、format v9、107,406,502 byte
- product.sdict SHA-256: `31c368d01f684dc7568c70e75148efddd9cd1f7d1d76b2c150052b2ee5fadd51`

## 検証

- GitHub Actions手動実行（run 40354905955、number 45）はbuild、native mode、HTML、Telemetry、Rust core・製品辞書受入テスト、MSI梱包、artifact uploadまで成功しました。
- MSIの管理イメージ展開でpackage.jsonを確認し、ProductVersion `0.1.45`、SelfHostモード、診断有効、ソースコミット、辞書hashを照合しました。payload 303ファイルはすべてmanifestのサイズ・SHA-256と一致しました。登録・インストールはしていません。
- 配布noticesはMSI内279ファイルとパス・SHA-256が全件一致しました。
- 利用者の指定により、VM上のインストール・実入力確認は行っていません。利用者による実入力確認もこれからです。

## 導入

`INSTALL.txt`を参照してください。Microsoft Edge WebView2 Runtimeが必要です。更新後はサインアウトしてサインインし、入力切替から`coltIme (selfhost)`を選んでください。既定IMEは自動変更しません。

本体はMITライセンスです。同梱の`COLTIME-NOTICE.txt`とnoticesアーカイブに、本体・第三者・辞書それぞれの条件を収録しています。SelfHostの診断ログは`%LOCALAPPDATA%\coltIme\logs`に保存されます。AI失敗ログには再現のため入力本文・前文脈・補助文脈・AI応答が含まれる場合があります。APIキー値は保存せず、ログを外部へ自動送信しません。

通常の64bit Windowsアプリを対象にしています。32bitアプリ、ARM64、管理者アプリの動作は対象外です。個別アプリでの動作は利用者の確認が必要です。
