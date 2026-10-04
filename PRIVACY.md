# プライバシー / Privacy

アプリは個人情報・利用統計を収集する機能を実装していません。図面・フォント・CTBを外部サーバーへ送信しません。アカウント登録、広告、トラッキング、テレメトリはありません。

図面の解析用コピーとJSONはOS一時領域に作成し、通常終了・例外時に削除します。強制終了・電源断では残る場合があります。PDF・設定・解析JSONは利用者が保存操作した場合に保存します。解析JSONやPDFも機密情報を含む場合があります。

画面スポイトは利用者が起動したときだけ取得します。Windowsスポイトはカーソル周囲を読み取り、色を返します。ブラウザによる画面取得では共有許可が必要です。スクリーン画像を外部送信する処理はありません。

外部ブラウザの履歴・同期・拡張機能、OSの通信はブラウザ・OS側の設定に従います。公開Issueへ図面やスクリーンショットを投稿すると第三者に公開されるため、機密情報を含めないでください。

English: The application implements no personal-data collection, analytics or telemetry. It does not upload drawings, fonts or CTB files and requires no account. Local temporary parser files are normally removed; forced termination can leave them behind. PDF/settings/JSON are saved only on explicit user action. The user-initiated eyedropper captures locally. Browser/OS history, extensions, synchronization and networking are outside application control. Public issue submissions are public.
