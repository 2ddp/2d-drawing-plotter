# セキュリティ報告 / Security

外部通信を必要としない設計、ローカル処理、第三者依存関係の開示を基本とします。脆弱性がないことや商用製品と同等のSLAを保証しません。

## 報告方法

公開開始時はGitHub Security AdvisoriesのPrivate vulnerability reportingを有効化し、非公開報告を受け付ける方針です。現在は公開リポジトリと受付先が未設定です。受付先の設定・確認が公開前の必須項目です。

公開Issueには機密DWG、PDF、SHX、個人情報、未修正脆弱性の詳細や再現攻撃ファイルを投稿しないでください。通常の表示・PDF不具合は匿名化した情報だけで報告できます。

## 対応範囲

最新の公開安定版をbest effortで対応します。現在のdev.39は検証候補であり安定版・長期サポート版ではありません。修正・期限・個別サポートを保証しません。古い版は原則対象外です。

第三者解析器にも不正ファイル処理のリスクがあります。信頼できない図面は隔離環境で扱ってください。一般公開前にWindows実機で外部通信、管理者権限なし、オフライン操作を検証します。SHA-256は同一性確認であり、安全性・配布元の真正性の証明ではありません。

English: Security reports should use GitHub private vulnerability reporting once configured. No private endpoint exists yet; configuring and testing it is a release gate. Do not post confidential drawings or unpatched exploit details in public issues. The latest stable release receives best-effort attention, with no guaranteed fix, response time or SLA. dev.39 is a candidate. Local processing and hashes are not a guarantee of security.
