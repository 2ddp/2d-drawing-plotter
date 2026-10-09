# 更新履歴 / Changelog

## 0.1.3

### 日本語

#### 画面・操作

- 日本語・英語の用紙／ペン設定の入力欄を揃え、長い項目名でも操作欄の高さを保つようにしました。ヘッダーの操作ボタンも一列に整理しました。
- 「基本線幅」の項目名を固定し、線幅モードの説明を分離しました。英語の印刷用語と出力範囲の説明を整理しました。

#### 描画・選択

- 非矩形ビューポートの境界として、凹形を含む閉じたポリライン、円、楕円、円弧付きポリライン、閉じたスプラインに対応しました。
- 画面・PDF・クリック／範囲選択・スナップに共通のクリップ境界を適用しました。境界の外にある図形を選択・スナップ候補から除外します。
- 直線、円、円弧、楕円、スプライン、幅のないポリラインで、文字・SHX記号入りの複雑な線種に対応しました。曲線の長さと接線に沿って配置し、尺度・位置オフセット・回転・反転を反映します。
- 楕円の軸比による文字サイズの変形を防ぎ、スプラインの不連続な区間をつなぐ不要な線を描かないようにしました。

#### PDF・描画データの再利用

- 曲線とクリップ境界をベクターとして出力し、文字検索・コピーとフォントサブセット埋め込みを維持しました。連続する同一ビューポートの境界データの重複を抑えます。
- 画面移動・ズームでは生成済みの描画データとクリップ境界を再利用します。説明書とリリースノートを日本語・英語で更新しました。

### English

#### Interface and controls

- Aligned paper and pen controls in Japanese and English, keeping paired fields at the same height when captions wrap. Arranged header controls on one row.
- Kept the Base lineweight label fixed and separated the mode explanation. Reviewed English plot terminology and descriptions of plot areas.

#### Rendering and selection

- Added nonrectangular viewport boundaries using closed polylines, including concave shapes, circles, ellipses, polylines with arc segments and closed splines.
- Applied shared clipping boundaries to viewing, PDF export, click and area selection, and snapping. Geometry outside a boundary is excluded from selection and snapping.
- Added complex linetypes with embedded text and SHX shapes on lines, circles, arcs, ellipses, splines and zero-width polylines. Placement follows curve length and local tangents, with scale, offsets, rotation and reflection.
- Kept symbol size independent of the ellipse axis ratio and avoided unwanted connecting strokes between discontinuous spline spans.

#### PDF and rendering reuse

- Preserved vector curves and clipping boundaries, text search and copying, and font subsetting. Reduced duplicate boundary data for consecutive objects in the same viewport.
- Reused resolved drawing data and clipping boundaries during pan and zoom. Updated manuals and release notes in both Japanese and English.

## 0.1.2

- 日本語／EnglishのUI切替を追加。図面と印刷設定を維持し、選択した言語を次回起動へ引き継ぎます。
- 用紙・尺度・画層・ペン・スポイト・フォント管理・診断の英語表示に対応。
- Added Japanese/English UI switching, including plot controls, layers, pens, color picking, fonts and diagnostics.

## 0.1.1 — 2026-10-06

- DWGの表示互換性と描画パフォーマンスを改善しました。
- 文字の配置、MTEXTの部分書式・色、背景マスクと重なり順の再現を改善しました。
- PDF出力で文字の部分色、字間、装飾を反映し、文字検索を維持しました。
- 図面表示エリアへのドラッグ＆ドロップ読込みに対応しました。
- アイコンと画面表示を調整しました。

English: Improved DWG rendering and performance, text positioning and MTEXT formatting, background masks and draw order, PDF text colors and spacing, drawing drag-and-drop, and application icons.

## 0.1.0 — 2026-10-05

2D Drawing Plotterの初回正式リリースです。

- Windows 11 x64向けポータブル配布
- DWGの2D表示、Model / Layout、画層の表示・印刷管理
- 用紙・尺度・印刷範囲・CTB・色別ペン設定とPDF出力
- SHXフォント読込み、検索可能なPDF、印刷設定の保存・読込み
- 日本語を主言語とする説明書、第三者ライセンス、対応ソース、SHA-256

English: First official release. Portable Windows distribution, local 2D DWG viewing, plot controls and PDF export.

