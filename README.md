# pubsite

VM（vnic-01）で作ったアプリのうち、選んだものを GitHub Pages で公開するためのリポジトリ。

- `site/` の中身はすべてパスワードで暗号化済み（AES-256-GCM、鍵は PBKDF2-SHA256 60万回）。元のソースはこのリポジトリに含めない
- `site/` は VM の `publish-site` コマンドが作る。手で編集しない
- push すると GitHub Actions（`.github/workflows/pages.yml`）が Pages に公開する

## 設定（VM 側）

- `~/.config/pubsite/apps.txt` … 公開するアプリのスラッグを1行に1つ（`~/web_server/public/projects/<slug>/poc` が対象）
- `~/.config/pubsite/password` … パスワード（`chmod 600`。リポジトリには入れない）

## 更新の流れ

    publish-site                 # site/ を作り直す
    cd ~/pubsite && git add -A && git commit -m "update" && git push
