# 更新履歴 / Changelog

## 0.1.4

### 日本語

#### 幅付きポリラインと線種

- 一定幅・可変幅の開閉ポリラインで、通常の破線、ゼロ長の点、文字・SHX記号入り線種の対応範囲を拡張しました。直線・円弧、継ぎ目、先細り、幅の段差、点から始まる線種と、変換後の文字・記号の正立方向を扱います。
- PSLTSCALEを読み、設定が1の場合はビューポート倍率が違っても紙上の線種尺度を揃えます。画面・ベクトルPDF・画層・クリップ・選択・スナップで描画データを共有します。

#### MTEXTの書式・段落・双方向文字

- MTEXTの部分SHX／TrueTypeフォント、固定TTF／OTFの読込み、左右余白・字下げ、左／中央／右・両端／均等配置、左／中央／右タブ、最小／固定行間に対応範囲を追加しました。測定・折返し・画面・PDFが同じ文字配置を使います。
- 結合文字を改行やフォント代替で分断しないよう改善しました。基本的なアラビア語・ヘブライ語の双方向配置と、方向記号・埋め込み・上書き・分離に対応し、元の文字列を検索用PDFへ保持します。
- 同じ書体のアラビア文字・結合記号だけの単語では、確認できた字形の所属に基づき、部分色・装飾・幅・傾き・高さ・上下位置を適用して単語全体の字形を維持します。完全なUAX #9準拠や全言語・全書式への対応は意味しません。

#### マルチ引出線の表示とプレビュー

- 平面・横書き・単一段組みの文字背景で、図面背景色、保存ACI／RGB色、明示アルファによる透過をプレビュー表示します。保存値に基づく文字枠と、左右5／6・上下10の文字接続の下線／上線も追加しました。背景・枠・接続線・文字の色と透過を分離します。
- 非表示・空の枝だけの場合に孤立した接続線を残さず、上下接続に横向きのdoglegを加えません。枝の表示上書き、共有接続線、保存された最小／固定行間を反映し、保存座標・間隔の二重尺度化を防ぎます。
- 元CADとの外観比較は未完了のため、背景・枠・接続装飾線のプレビュー警告を維持します。全行接続形式8、曲線／線切断、複雑な接続線種、段組み・縦書き・傾斜平面、旧矢印・属性上書きなどの未対応条件は診断します。

#### 空白レイアウトの診断と確認範囲

- 保存ビューポートがモデルの表示範囲外にある空白と、画層・凍結・クリップ等による空表示を区別して通知します。保存カメラや図形は自動変更しません。
- dev26までに通常版／minify版JavaScript各1,076件、Python44件、元の2図面の回帰確認と専用サンプルのCanvas／ベクトルPDFを確認しています。Windows実機・元CADとの外観／枠／透過／CTB比較、フィット点のみのスプライン、代替フォント、予約線幅の照合は継続課題です。

### English

#### Wide polylines and linetypes

- Extended simple and text/SHX complex linetypes on supported open/closed constant- and variable-width polylines, including line/arc segments, seams, tapering, width steps, zero-length dots, dot-first patterns and upright symbols after transforms.
- Read PSLTSCALE and keep paper-space linetype size consistent across viewport scales when enabled. Share resolved geometry across Canvas, vector PDF, layers, clipping, selection and snapping.

#### MTEXT formatting, paragraphs and bidirectional text

- Extended inline SHX/TrueType fonts and fixed TTF/OTF loading, paragraph margins/indents, left/center/right/justified/distributed alignment, left/center/right tabs and at-least/exact line spacing. Measurement, wrapping, Canvas and PDF share text layout.
- Protect combining clusters during wrapping and fallback. Support basic Arabic/Hebrew bidirectional layout and directional marks, embeddings, overrides and isolates, preserving original text in searchable PDF output.
- For same-font Arabic-letter/mark-only words, apply inline paint, rules, width, oblique, height and vertical alignment through verified glyph ownership while retaining whole-word shaping. Full UAX #9 or unrestricted script/format support is not claimed.

#### Multileader rendering and previews

- Preview drawing-background/ACI/RGB fills and explicit-alpha transparency on planar horizontal single-column text. Add stored text frames and attachment rules for horizontal types 5/6 and vertical type 10, keeping background, frame, rule and text paint separate.
- Avoid detached doglegs for hidden-only/empty branches and horizontal doglegs for vertical attachments. Respect branch visibility overrides, shared connections and stored line spacing without rescaling stored coordinates/gaps twice.
- Keep preview diagnostics because original CAD appearance is unverified. Diagnose unsupported all-line type 8, curved/broken connections, complex attachment linetypes, columns, vertical/tilted text and remaining legacy arrow/attribute overrides.

#### Empty-layout diagnostics and verification scope

- Distinguish saved viewports outside model geometry from empty results caused by visibility, freezing or clipping. Keep stored cameras and geometry unchanged.
- Through dev26, verified 1,076 JavaScript tests on both source and minified builds, 44 Python tests, two original-drawing regressions and authored Canvas/vector-PDF samples. Windows/original CAD appearance/frame/alpha/CTB acceptance, fit-only spline comparison, fallback fonts and reserved lineweights remain pending.

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

