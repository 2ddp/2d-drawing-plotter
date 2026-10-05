# 2D Drawing Plotter

**Lightweight DWG Viewer & PDF Plot Tool**

Windows向けの2D DWGビューアー・PDF出力ツールです。図面の確認と印刷に必要な機能を、ローカルで利用できます。[English](docs/en/README.md)

## ダウンロード

[最新版をダウンロード](https://github.com/2ddp/2d-drawing-plotter/releases/latest)

`2D-Drawing-Plotter-0.1.1-Windows-x64.zip` を展開し、`START.cmd` を実行してください。

| 動作環境 | Windows 11 x64 |
|---|---|
| ブラウザー | Microsoft Edge / Google Chrome / Firefox |
| 導入 | インストール・管理者権限・Pythonの別途導入不要 |
| 接続 | インターネット接続不要（オフラインで完結） |
| 料金 | 個人・社内・商用利用ともに無償 |

利用中は起動したコンソールを開いたままにします。終了時はブラウザーのタブとコンソールを閉じてください。

## 主な機能

- DWGの2D表示、Model / Layout切替、画層の表示・印刷管理
- ズーム・移動・全体表示、図形選択、印刷範囲の矩形指定とスナップ
- 用紙・向き・尺度・余白の設定、CTB読込み、色別の出力色・線幅設定
- SHXフォントの読込み、ベクターPDF出力、文字検索に対応したPDF生成
- 印刷設定の書出し・読込み、解析JSONの保存

[使い方](docs/ja/user-guide.md) · [対応形式](docs/ja/supported-dwg.md)

## ローカル処理とプライバシー

図面は利用者のPC内で処理します。図面を外部サーバーへアップロードせず、アカウント登録・広告・トラッキング・テレメトリはありません。必要なプログラムと代替フォントは同梱し、すべての機能をオフラインで利用できます。

[プライバシー](PRIVACY.md) · [通信と保存](docs/ja/privacy-and-network.md)

## ライセンスと配布物

本体は無償で利用できます。本体ソースコードは公開していません。利用条件および同梱コンポーネントのライセンスは、以下をご確認ください。

GNU LibreDWGの対応ソースとビルド情報は、各リリースの `LibreDWG-source-for-2D-Drawing-Plotter-0.1.1.zip` で提供します。配布ZIPのSHA-256は `SHA256SUMS.txt` に記載しています。

[利用条件](LICENSE.txt) · [第三者ライセンス](THIRD_PARTY_NOTICES.md) · [配布ファイルの説明](docs/ja/distribution.md)

## お問い合わせ

不具合報告・機能要望は [Issues](https://github.com/2ddp/2d-drawing-plotter/issues) へお寄せください。バージョン、利用環境、再現手順を添えていただくと確認が円滑になります。機密図面や個人情報は投稿しないでください。

[報告方法](CONTRIBUTING.md) · [セキュリティ](SECURITY.md) · [更新履歴](CHANGELOG.md)
