# DWA防災情報センター（台風25号 災害後方支援モジュール 組み込み版）

地震速報LIVE・災害情報をまとめた「防災情報センター」の単一ページサイトに、
**台風25号 災害後方支援モジュール**を組み込んだものです。

## 追加した機能

「🔴 最新情報」ティッカー（バナー）の**すぐ下**に、台風25号向けのバナーを追加しました。

- **バナー**：`🌀 台風25号 災害後方支援` — タップでパネルが開きます。
- **市区町村検索**：名前を入力（漢字・ひらがな両対応。例「市原市」「いちはら」）すると、
  その自治体の**避難所開設・避難情報ページ**（Yahoo!天気・災害／Lアラート等の公式情報）を直接開けます。
- **都県別一覧**：関東7都県・**全316市区町村**をアコーディオン表示。各県の公式防災ポータルも併記。
- **広域・リアルタイム情報**：気象庁キキクル／河川／停電／道路など。
- **後方支援・生活再建**：災害ボランティア・安否確認・被災者支援の窓口。
- **共有ボタン（URL生成）**：パネル右上の「🔗 共有」で共有用URLを生成します。
  - 端末が対応していれば OS の共有シートを開き、非対応でもクリップボードにコピーできます。
  - 生成URLには `#saigai25` が付き、開いた相手は**パネルが自動で開いた状態**になります。
  - 検索欄に入力がある状態で共有すると `#saigai25=市原市` のようにキーワードも引き継がれ、
    相手側で**その市区町村を表示した状態**で開きます。

- **こころのチェック（心診断）**：ハンバーガーメニュー内「// こころのケア」に追加。災害後の心の状態を自分で振り返る自己チェック（`kokoro.html`）。文中の「地震」は「災害／自然災害」に変更済み。

組み込みは既存コードを壊さないよう、すべて `t25-` / `saigai25` の接頭辞で分離しています。

## ローカルで開く

`index.html` をブラウザで開くだけで動作します（外部依存は Google Fonts と各リンク先のみ）。

```bash
# 簡易サーバーで確認する場合
python3 -m http.server 8000
# → http://localhost:8000/
```

## GitHub リポジトリとして push する

このフォルダは git 初期化済み（初回コミット入り）です。自分のリポジトリを作成して push してください。

```bash
cd dwa-bousai-center
git remote add origin https://github.com/<あなたのユーザー名>/<リポジトリ名>.git
git branch -M main
git push -u origin main
```

新規に作り直したい場合：

```bash
rm -rf .git
git init && git add . && git commit -m "init"
```

## GitHub Pages で公開する

1. GitHub でリポジトリを開き **Settings → Pages**。
2. **Build and deployment** の **Source** を「Deploy from a branch」に。
3. **Branch** を `main`／フォルダ `/ (root)` に設定して **Save**。
4. 数十秒後、`https://<ユーザー名>.github.io/<リポジトリ名>/` で公開されます。

（`.nojekyll` を同梱しているため、`.webp` 等がそのまま配信されます。）

## 同梱ファイル

| ファイル | 内容 |
|---|---|
| `index.html` | 本体（台風25号モジュール組み込み済み） |
| `kokoro.html` | こころのチェック（災害後の心の自己チェック。メニューから開く） |
| `README.md` | このファイル |
| `.gitignore` | OS/エディタの一時ファイル除外 |
| `.nojekyll` | GitHub Pages の Jekyll 処理を無効化 |

## 別途用意が必要なファイル（今回のアップロードに含まれていません）

`index.html` は元プロジェクトの以下のファイルを参照します。無くてもページ自体は表示されますが、
アイコン・背景画像・サブページのリンクが欠けます。元プロジェクトから同じ階層にコピーしてください。

- サブページ：`Manual.html` `guide.html` `saiken-guide.html` `quiz.html` `drill.html` `earthquake_globe_2026.html`
- アイコン／PWA：`manifest.json` `favicon-32.png` `apple-touch-icon.png` `reload-icon.png`
- 画像（.webp / .png）：`dwa-header-bg-v2.webp` `dwa-header-panel-v2.webp`
  `dwa-plate-manual-v2.webp` `dwa-plate-diagnosis-v2.webp`
  `dwa-splash-l-v2.webp` `dwa-splash-r-v2.webp`
  `dwa-sw-flare.webp` `dwa-sw-geomag.webp` `dwa-sw-radio.webp`
  `dwa-instagram-qr.webp` `dwa-stamp-mask-1-v2.png` `dwa-stamp-mask-2-v2.png`

## データ出典・免責

- 市区町村ごとの避難所開設・避難情報：**Yahoo!天気・災害**（自治体が L アラート等で発表する情報にもとづく）へ直接リンク。
- 各県の公式防災ポータル：国土交通省 関東地方整備局の公式リンク集にもとづく。
- 市区町村コード：総務省「全国地方公共団体コード」。

避難所情報はリンク先で随時更新されます。表示が実際と異なる場合は、必ず**お住まいの自治体の公式発表**を優先してください。
避難の判断は最新の公式情報と現地の状況にもとづいて行ってください。

本サイトは災害対応の後方支援を目的とした非公式の情報整理ページであり、Anthropic の公式サービスではありません。
