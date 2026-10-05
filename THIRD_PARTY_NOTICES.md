# 第三者コンポーネント / Third-party notices

独自部分の利用条件は第三者の許諾を置き換えません。原文通知はlicenses以下とruntime/LICENSE.txtに保持します。以下は同梱コンポーネントの一覧です。

| Component | Version | Copyright / attribution | License | Purpose | Modified |
|---|---|---|---|---|---|
| GNU LibreDWG | 0.13.4; e3774bd4020fcfebb68150361db74b8b34d170fe | 原ソースのCOPYING・AUTHORS・各ファイルを保持 / upstream notices retained | GPL-3.0-or-later | 別プロセスでDWGをfull JSONへ解析 | Yes: src/out_json.c Unicode JSON patch |
| CPython Windows embeddable x64 | 3.13.16 | Python Software Foundationほか。runtime/LICENSE.txt原文 | PSFと同梱部品の条件 | 本体サーバー・スポイトの実行 | No: official embed package, unmodified |
| Noto Sans JP static Regular | 2.004 (font metadata) | Adobe 2014–2021; Reserved Font Name 'Source' | OFL-1.1 | 日本語代替表示・PDFサブセット | Yes: glyf offsets normalized; outlines/advances retained |
| pdf-lib | 1.17.1 | Andrew Dillon 2019 | MIT + embedded component terms | PDF生成 | Yes: only trailing sourceMappingURL removed |
| @pdf-lib/fontkit | 1.1.1 | Andrew Dillon, Devon Govett; package declarations and original bundle comments | Declared MIT + embedded component terms | PDFフォントサブセット | No |
| ezdxf acadctb.py | Pinned byte hash in config | Manfred Moitzi 2010–2023 | MIT | CTB読込 | No: retained vendor source bytes |
| Microsoft VC runtime (vcruntime140.dll / vcruntime140_1.dll) | Bundled with CPython 3.13.16 | Microsoft | runtime/LICENSE.txt Additional Conditions | Python C runtime | No |
| OpenSSL | 3.5.9 (CPython pinned build recipe) | OpenSSL contributors | Apache-2.0 | Official Python crypto/SSL runtime | No |
| libffi | 3.4.4 (CPython pinned build recipe) | Anthony Green, Red Hat and others | MIT, runtime/LICENSE.txt | Windows ctypes pixel APIs | No |
| SQLite | 3.50.4.0 (CPython pinned build recipe) | SQLite authors | Upstream public-domain dedication | Included in unmodified standard Python runtime | No |
| zlib | 1.3.1 (CPython pinned build recipe) | Jean-loup Gailly, Mark Adler | zlib license | CTB and standard Python compression | No |
| Windows UCRT / Win32 | OS-provided | Microsoft | OS component terms | C runtime and screen-pixel APIs | No: not separately bundled |

## Project URLs

- GNU LibreDWG: https://www.gnu.org/software/libredwg/ ; official mirror https://github.com/LibreDWG/libredwg
- CPython: https://www.python.org/ ; https://github.com/python/cpython
- Noto: https://github.com/google/fonts/tree/main/ofl/notosansjp
- pdf-lib: https://github.com/Hopding/pdf-lib
- fontkit: https://github.com/Hopding/fontkit
- ezdxf: https://github.com/mozman/ezdxf

これらは出典情報であり、アプリが起動時にアクセスするURLではありません。実行ファイル・フォント・ライブラリ・Python全ファイルのSHA-256はBUILD-INFO.jsonとconfig内の固定情報にあります。

## Source and changes

GNU LibreDWGの完全な固定ソース、Unicode修正パッチ、ビルド手順・設定は、同一版のLibreDWG-source-for-2D-Drawing-Plotter ZIPで提供します。実行ZIPと同じ場所から同等の条件・追加料金なしで取得できるようにしてください。元ソースの個別copyrightはアーカイブに保持しています。

Pythonは公式embeddableパッケージを改変せず同梱し、その原LICENSE.txtを保持します。pipパッケージは導入しません。標準実行環境の構成は全体を保持し、アプリ独自の未使用SDK等を追加しません。OpenSSL/libffi/SQLite/zlibの版は固定CPythonソースのPCbuild/python.propsに基づく値です。Microsoft再配布コードの追加条件はruntime/LICENSE.txtと本体利用条件に保持します。依存更新ではアーカイブを差替えるだけでなく版・ハッシュ・受入を更新します。

pdf-lib/fontkitに内包された部品の原通知とApache-2.0本文をlicenses/pdf-bundlesに保持します。fontkit npmアーカイブは単独LICENSEファイルを含まないため、package/READMEのMIT宣言と原バンドル通知を保存しています。

商用・許諾不明のSHX、利用者図面は同梱しません。利用者がフォントを読み込む場合、その利用・PDF出力の権利条件を確認してください。

## Development tools (not in runtime)

esbuild 0.25.12 (MIT, Evan Wallace 2020; https://github.com/evanw/esbuild)は非公開ビルドでのみ使用します。フォント正規化はfonttools 4.61.1を使用した既存の固定成果物を保持します。開発工具・合成テスト図面は実行版へ入れません。

English: Original component terms and copyright notices govern each dependency. Application terms do not override them. LibreDWG's complete matching source, Unicode patch and build recipe are provided separately with equivalent access. Python is the unmodified official embeddable package, retaining original notices and containing no added pip packages. PDF bundles retain embedded component notices. No commercial SHX or private drawings are bundled. Build tooling is private and not part of the runtime.
