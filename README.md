# 2D Drawing Plotter

**Lightweight DWG Viewer & PDF Plot Tool**

個人開発の、Windows向け2D DWGビューアー・PDF出力ツールです。編集機能を持たず、図面の確認と印刷設定に絞っています。日本語が主言語です。[English](docs/en/README.md)

## ダウンロード

[試用版と更新履歴](https://github.com/2ddp/2d-drawing-plotter/releases)から、`2D-Drawing-Plotter-0.12.0-dev.39-Windows-x64.zip` を取得してください。ZIPを自分が書込みできるフォルダーへすべて展開し、`START.cmd` を実行します。

Windows 11 x64向けです。Python 3.13.16 x64と解析器を同梱しており、別途インストール・初回ダウンロード・管理者権限を必要としない構成です。利用中はコンソールを開いたままにしてください。終了時はブラウザーのタブとコンソールを閉じます。

**開発中の試用版です。** クリーンなWindows環境でのオフライン受入・通信監視と代表DWGの回帰確認は未完了です。すべてのDWGの再現性や、重要な業務成果物への適合性を保証しません。出力は原図と照合してください。確認済みの範囲と未確認項目は[検証記録](docs/ja/validation.md)に記載しています。

## ローカル処理と通信

- 図面は利用者のPC内で解析・描画します。図面のクラウドアップロード機能はありません。
- アカウント登録、広告、解析SDK、テレメトリ、自動更新確認を実装していません。
- JavaScript、CSS、フォント、Python、解析器は配布内に固定しています。通常利用に外部サービスは必要ありません。
- ローカルサーバーとブラウザーは127.0.0.1で通信します。ブラウザー自身・OS自身の通信はアプリの制御範囲外です。
- 第三者コンポーネントと変更内容を開示し、配布ZIPのSHA-256を添付します。

[通信と保存の詳細](docs/ja/privacy-and-network.md) · [プライバシー](PRIVACY.md)

## 主な機能

- Model／Layout、画層の表示・印刷管理、移動・ズーム、矩形スナップ
- 用紙・向き・余白・尺度・印刷範囲、CTB、色別の出力色・線幅
- SHX線文字と代替フォント、検索可能なPDF、明示的な印刷設定の保存・読込み

DWG編集・保存は行いません。未対応要素や代替文字は診断へ表示します。

[使い方](docs/ja/user-guide.md) · [対応DWG](docs/ja/supported-dwg.md) · [既知の制約](docs/ja/known-limitations.md)

## 利用条件と第三者ソース

本体の保守用ソースコードは当面公開しません。実行用JavaScriptはブラウザーから取得・解析できます。Pythonバイトコードも機密化手段ではありません。

GNU LibreDWGの対応ソースは、各Releaseで `LibreDWG-source-for-2D-Drawing-Plotter-0.12.0-dev.39.zip` として本体と同じ場所から提供します。再配布時も同じ版の対応ソースを同等の条件・追加料金なしで取得できるようにしてください。対応名とSHA-256は本体ZIP内の `BUILD-INFO.json` に記録しています。

本体利用条件と第三者ライセンスを確認してください。GPLの適用範囲、権利帰属・通知の完全性などの最終レビューは残っており、法的確認完了を表明するものではありません。非公開の開発用バックアップは公開・再配布対象に含めません。

[利用条件案](LICENSE.txt) · [第三者通知](THIRD_PARTY_NOTICES.md) · [アーキテクチャ](docs/ja/architecture.md)

## 不具合・要望

[Issues](https://github.com/2ddp/2d-drawing-plotter/issues)で、表示崩れ、DWG互換性、PDF出力の問題や機能要望を受け付けます。バージョン・Windows／ブラウザーの種類・再現手順を添えてください。機密図面や個人情報は投稿しないでください。対応はbest effortで、期限やサポートを保証しません。

[報告方針](CONTRIBUTING.md) · [セキュリティ報告](SECURITY.md) · [更新履歴](CHANGELOG.md)
