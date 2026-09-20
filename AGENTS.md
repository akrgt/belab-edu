# AGENTS.md

## Cursor Cloud specific instructions

このリポジトリは **shinylive** で書き出した静的バンドルである．R Shiny アプリ（`app.json` に `app.R` を内包）を WebAssembly（webR）へコンパイル済みであり，ブラウザだけで完結する．サーバ側に R や Node の依存は存在しない．

### サービスと実行方法

- 実体は静的サイトである．ビルド工程はない．依存インストールも不要である（webR とパッケージは `shinylive/` 配下の WASM にバンドル済み）．
- 開発時はリポジトリ直下を HTTP で配信し，`http://127.0.0.1:<port>/index.html` を開く．Service Worker（`shinylive-sw.js`）が COOP/COEP ヘッダを付与する関係で，`localhost`/`127.0.0.1` か https 以外では起動しない（`shinylive/load-shinylive-sw.js` 参照）．
- 配信例（標準ライブラリのみで完結）：`python3 -m http.server 8000 --bind 127.0.0.1`
- 編集可能なエディタ版は `edit/index.html`（`index.html` のエディタモードへリダイレクトする）．

### 起動時の注意点（非自明）

- 初回アクセスでは webR の初期化に概ね 20 秒〜1 分かかる．UI（① データ 〜 ⑧ 検定 などのタブ）が描画されるまで待つこと．
- 可視化タブでプロット種別を「散布図（geom_point）」にして X 軸変数のみ指定すると，Y 軸未指定のためプレビューに `Error: [object Object]` が出る．これはアプリの入力依存挙動であり，環境不具合ではない．Y 軸も指定するか，ヒストグラム等に戻すと解消する．

### lint / test / build

- 本リポジトリには lint・テスト・ビルドのツール設定は存在しない（静的成果物のみ）．
- アプリ本体の編集と再ビルドは別の開発リポジトリ側で行う（ソースは `inst/edu/app.R`，`shinylive::export("inst/edu", ...)` で書き出し）．詳細は `README.md` の「再ビルド」節を参照．
