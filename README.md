# 給食成分表 (Diet Calc) — PWA 一式

## 配置（リポジトリ直下にそのまま置く）

```
/
├── index.html          ← 差し替え（<head> と </body> 直前に追記済み）
├── manifest.json       ← 新規
├── sw.js               ← 新規
├── favicon.ico         ← 新規
└── icons/
    ├── icon-192.png
    ├── icon-512.png
    ├── icon-maskable-192.png
    ├── icon-maskable-512.png
    ├── apple-touch-icon.png
    ├── favicon-32x32.png
    └── favicon-16x16.png
```

パスはすべて相対（`./`）なので、`user.github.io/リポジトリ名/` 配下でも動きます。

## index.html への変更点（2か所のみ）

1. `<head>` に manifest / アイコン / theme-color / description を追加
2. `</body>` 直前に Service Worker 登録スクリプトを追加

アプリ本体のコードには一切手を触れていません。

## アプリを更新したときの手順（重要）

`index.html` を書き換えたら、**必ず `sw.js` の `CACHE` の版数も上げる**。

```js
const CACHE = 'kyushoku-v1.4.2';   →   'kyushoku-v1.4.3'
```

これを忘れると、古いキャッシュが残ったままの端末が出ます。
index.html 自体は network-first なのでオンラインなら最新が出ますが、
アイコン等の静的ファイルは cache-first のため版数更新が必要です。

## キャッシュ戦略

- HTML（navigate）: network first → 失敗時 cache（オフラインでも起動する）
- 静的アセット: cache first → なければ取得してキャッシュ

## 色

| 用途 | 値 |
|---|---|
| アイコン背景 | `#1A5FA8`（TNM アプリと共通） |
| シンボル | `#A5D6A7` |
| 下段テキスト | `#BBD4F0` |
| theme-color | `#FFFFFF`（ヘッダーが白のため） |
| スプラッシュ背景 | `#F7F9FC` |
