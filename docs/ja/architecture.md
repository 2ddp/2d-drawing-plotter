# 構成と解析境界

DWGは独立したGNU LibreDWG CLIで解析し、CLIが通常出力するfull JSONをファイル経由で受け取ります。2D Drawing Plotter専用のDrawingDocumentを解析器へ持たせません。LibreDWGは直接リンクしません。

## CLI単体の利用

`bin/win64/dwgread.exe --version`

`bin/win64/dwgread.exe -O JSON -o parsed.json input.dwg`

CLIは本体・ブラウザを起動せず利用できます。バージョンは0.13.4です。Unicode JSON出力だけを修正し、描画・画層管理・PDFのロジックは加えていません。

## JSONと本体

入力JSONはLibreDWGの公開するバージョン依存の出力形式であり、標準化された共通CAD交換仕様と同義ではありません。作成者識別とOBJECTS等を検証し、AdapterだけがLibreDWG固有の構造を解釈します。独自DrawingDocumentから共通Sceneを作り、ViewerとPDFが同じSceneを使います。DXFへ変換しません。

プロセス分離は技術上の境界です。GPLの適用範囲の最終的な法的評価を保証するものではありません。
