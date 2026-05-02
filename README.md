# beLab-edu — R コード生成アシスタント

オンデマンド講義「社会統計」向けの R 入門 GUI．  
ブラウザだけで動く（インストール不要）shinylive アプリ．

## 学生向け：使い方

1. このリポジトリの GitHub Pages URL（Pages 設定後に表示）にアクセス
2. 初回は webR を読み込むため 30 秒〜1 分待つ
3. ① データタブでデータを選ぶ（組込み or CSV アップロード）
4. 各タブで操作 → 右上の「📋 コピー」で R コードをコピー
5. Google Colab に貼り付けて実行

## 構成

| ファイル/ディレクトリ | 役割 |
|---|---|
| `index.html` | エントリポイント |
| `app.json` | アプリ本体（app.R + README.md を内包） |
| `shinylive/` | webR + 必要パッケージの WASM バンドル |
| `shinylive-sw.js` | COOP/COEP ヘッダ用の Service Worker |
| `edit/` | shinylive エディタ（学生がコードを直接編集できる版） |

## 再ビルド

ソース（`inst/edu/app.R`）を編集したら，beLab 開発リポジトリで以下を実行：

```r
shinylive::export(
  appdir  = "inst/edu",
  destdir = "docs/edu"
)
```

そして `docs/edu/` の中身をこのリポジトリにコピーして commit & push．

## 含まれる機能

- ① データ：組込みデータ／CSV アップロード／URL／Drive
- ② 整形：dplyr テンプレ
- ③ 記述統計：群別 mean / SD / median / quartile
- ④ 可視化：ggplot2 ビルダ（17 種の geom + facet + パレット + ラベル）
- ⑤ クロス集計：addmargins + prop.table + chisq.test + クラメール V
- ⑥ 相関：cor.test + 散布図
- ⑦ 回帰分析：lm + 残差プロット
- ⑧ t 検定：独立 / 対応のある / 1 標本 + Cohen's d + Wilcoxon
- 🎓 チュートリアル：intro.js でステップ案内（クロス集計）
