Windows x64向けのSelfHost実験版です。最適化と診断ログを有効にしています。MSIは未署名です。

## 今回の内容

- 予測候補の数字を候補番号として扱わず、入力した数字の文字として挿入するようにしました。全変換の候補一覧での数字選択は維持しています。
- 空欄へフォーカスしただけでユーザー履歴の候補が開く問題を修正しました。入力中の読み検索と、確定文脈からの次語予測は維持します。
- 製品辞書は2026-10-26 r5です。803,933語、word bigram 6,000,000件、word trigram 12,000,000件、phrase 81,489件を含みます。

## 識別情報

- MSI: `0.1.44`、SelfHost、Windows x64、最適化済み、診断有効
- ソース: `fb219f83174c67413c2705b2738b11a7a54ab0a2`
- 辞書: `coltIme-dictionary-20261026-r5`、format v9、107,406,502 byte
- product.sdict SHA-256: `31c368d01f684dc7568c70e75148efddd9cd1f7d1d76b2c150052b2ee5fadd51`
- MSI SHA-256: `4741cbaee13560ae3ba51ffe75e500839b8b70d12bff79c7107d72154a628ca9`

## 検証

- GitHub Actionsの手動実行（run 40346197960）は、ビルド、native／HTML検査、telemetry検査、Rust core検査、MSI梱包、成果物アップロードまで成功しました。
- 製品辞書の語彙・候補順位を固定期待値にした1検査は、辞書内容への依存を避ける方針に従い、今回のSelfHost CI実行対象から除外しています。
- MSIをインストールせず展開し、ProductVersion `0.1.44`、SelfHostモード、診断有効、ソースコミット、辞書のサイズとSHA-256を確認しました。MSIに含まれる303ファイルは、配布対象外の`Verify.ps1`を除き、package manifestのサイズとSHA-256に一致しました。
- 利用者の指定により、今回のインストール、VM上の実入力確認は行っていません。利用者による実入力確認もこれからです。

## 導入

`INSTALL.txt`を参照してください。Microsoft Edge WebView2 Runtimeが必要です。更新後はサインアウトしてサインインし、入力切替から`coltIme (selfhost)`を選んでください。既定IMEは自動変更しません。

本体はMITライセンスです。同梱の`COLTIME-NOTICE.txt`とnoticesアーカイブに、本体・第三者・辞書それぞれの条件を収録しています。SelfHostの診断ログは`%LOCALAPPDATA%\coltIme\logs`に保存されます。AI失敗ログには再現のため入力本文・前文脈・補助文脈・AI応答が含まれる場合があります。APIキー値は保存せず、ログを外部へ自動送信しません。

通常の64bit Windowsアプリを対象にしています。32bitアプリ、ARM64、管理者アプリの動作は対象外です。個別アプリでの動作は利用者の確認が必要です。

