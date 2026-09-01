Markdown
# qitta-content

Qiita CLI を活用して、Qiita（キータ）の記事を GitHub 上でバージョン管理・自動投稿するためのリポジトリです。

---
## 📁 記事公開方法
4. 記事の作成・編集（front-matter の設定）
投稿・更新対象の Markdown ファイルは public/ ディレクトリ内に配置し、ファイル先頭に front-matter（ヘッダー情報）を記述します。

📄 新規投稿の場合
id を null に設定します。投稿成功時に自動的に ID が付与されます。

Markdown
---
title: 記事のタイトル
tags:
  - Qiita
  - GitHub
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

ここから本文を開始します...
🔄 既存記事を更新・上書きする場合
id に Qiita 上の既存記事の ID を直接指定します。
（例: https://qiita.com/username/items/123456789abcdef01234 の場合は 123456789abcdef01234）

Markdown
---
title: 更新後の記事タイトル
tags:
  - Qiita
  - GitHub
private: false
updated_at: ''
id: '123456789abcdef01234'
organization_url_name: null
slide: false
ignorePublish: false
---

ここから更新後の本文を記述します...
5. 記事の投稿・更新（Publish）
編集が完了したら、以下のコマンドで Qiita へ反映させます。

Bash
npx qiita publish
id: null のファイル ➔ 新規記事として投稿

id: 'xxxx' のファイル ➔ 対象の既存記事を更新

## 📁 記事更新方法

編集が完了したら、以下のコマンドで Qiita へ反映させます。

Bash
npx qiita publish
id: null のファイル ➔ 新規記事として投稿

id: 'xxxx' のファイル ➔ 対象の既存記事を更新

## 📁 フォルダ構成

```text
qitta-content/
├── .github/
│   └── workflows/
│       └── publish.yml      # GitHub Actions 自動投稿ワークフロー
├── public/                  # Qiita 記事格納用ディレクトリ (.md)
├── .env                     # Qiita トークン設定 (ローカル用)
├── package.json
└── README.md
🚀 使い方
1. 記事の新規作成
以下のコマンドで public/ ディレクトリ配下に新しい記事ファイルを作成します。

Bash
npx @qiita/qiita-cli new "記事のタイトル"
2. ローカルでのプレビュー確認
ローカルサーバーを起動し、ブラウザ上で記事の表示を確認できます。

Bash
npx @qiita/qiita-cli preview
実行後、ブラウザで http://localhost:4000 にアクセスしてください。

3. ローカルからの投稿・同期
Qiita にログイン後、ローカルから記事を投稿・更新します。

Bash
# ログイン（初回のみ）
npx @qiita/qiita-cli login

# 記事の投稿・更新
npx @qiita/qiita-cli publish
🔄 GitHub Actions による自動投稿の流れ
作業ブランチで記事の作成・修正を行います。

GitHub 上で main ブランチへ Pull Request を作成します。

PR を Merge すると、GitHub Actions が自動起動し、Qiita へ記事が公開・更新されます。

📝 Frontmatter（記事ヘッダー）の指定
public/ 配下の各 Markdown 記事の先頭には、以下のメタ情報を記述します。

YAML
---
title: エンジニア未経験でもわかる要件定義の基礎知識
tags:
  - 要件定義
  - 初心者
private: false
updated_at: ''
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
id: 新規投稿時は null に指定します。投稿成功後に自動で記事 ID が付与されます。

private: false で全体公開、true で限定共有記事になります。

ignorePublish: true にすると投稿対象から除外されます。


---

### 作成手順（ターミナルからの追加方法）

ローカル環境のプロジェクトルートで以下を実行し、GitHub へプッシュします。

```bash
cd /Users/kazuya.nakazawa/projects-personal/qitta-content

# README.md の新規作成・保存（上記内容をファイルに書き込んだ後）
git add README.md
git commit -m "docs: README.md を作成"
git push origin kazoo0908-patch-2
