# 理工の補講 — Webサイト

静的HTMLとCSSのGitHub Pagesサイト。Node.jsやビルド処理は不要です。
動画制作プロジェクトでは `website/` サブモジュールとして利用します。

## 編集とプレビュー

- `public/index.html`：トップページ
- `public/assets/style.css`：共通スタイル
- `public/`：公開するHTML・画像・CSSなど
- `.github/workflows/pages.yml`：GitHub Pages公開設定

このリポジトリのルートで実行します。

```bash
python3 -m http.server 8000 --bind 127.0.0.1 --directory public
```

http://127.0.0.1:8000/ を開きます。終了は Ctrl+C。
HTMLは直接編集し、ページを増やすときは `public/` に追加します。
リンクと画像のパスは相対パスにして、リポジトリ名を含むPagesのURLでも動くようにします。

## GitHub Pagesの初回設定

1. このリポジトリをGitHubへpushします。公開ブランチは `main` です。
2. GitHubの **Settings → Pages → Build and deployment → Source** を **GitHub Actions** にします。
3. **Actions → Deploy static site to GitHub Pages → Run workflow** で `main` を選んで実行します。
4. 成功した実行の `github-pages` 環境に表示される公開URLを確認します。

以降は `main` の `public/` または公開ワークフローを変更してpushすると自動公開します。
公開対象は `public/` だけです。READMEや制作プロジェクトのファイルは配信しません。
公開設定を変えただけではワークフローは実行されないため、初回は手動実行してください。
利用プランによってはPages用リポジトリをpublicにする必要があります。

## 制作プロジェクトからの更新

制作プロジェクトのルートで、サイトの変更を先にcommit・pushします。

```bash
git -C website switch main
git -C website add public
git -C website commit -m "Update website"
git -C website push origin main
git add website
git commit -m "Update website submodule"
```

ワークフローを変更した場合は、サイト側で `.github/workflows/pages.yml` もaddします。
親リポジトリのcommitだけでは、サイトの変更はpush・公開されません。
親が記録するサイトのcommitは、先にサイト用リモートへpushしてください。

仕様確認：2026-09-26、[GitHub公式のPagesワークフロー手順](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages)。
