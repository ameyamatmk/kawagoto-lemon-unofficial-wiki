# 河琴れもん 非公式wiki プロジェクト

## プロジェクト概要

個人VTuber「河琴れもん」さんの非公式wikiサイト。
ファン活動として配信情報・びしょげ雑談・歌枠セットリスト・活動履歴などをまとめる。

### 河琴れもんさんについて
- 美少女ゲームとお酒が大好きな一般人VTuber
- YouTube: https://www.youtube.com/@河琴れもん
- X(Twitter): https://x.com/lemonmon017
- 配信タグ: #れもすとりーむ

## 技術スタック

- **SSG**: MkDocs + Material for MkDocs
- **ホスティング**: Cloudflare Pages
- **パッケージ管理**: uv
- **言語**: Python 3.12+

## 参照プロジェクト

基本構成は mashiro wiki を参照:
`E:\10_devel\Cloudflare\wiki\mashiro`

## ディレクトリ構成

```
lemonk/
├── CLAUDE.md           # このファイル
├── mkdocs.yml          # MkDocs設定
├── pyproject.toml      # Python依存関係
├── design/             # 設計ドキュメント
└── docs/               # コンテンツ（Markdown）
    ├── index.md        # トップページ
    ├── stylesheets/    # カスタムCSS
    ├── javascripts/    # カスタムJS
    └── assets/images/  # favicon, OGP
```

## 開発コマンド

```powershell
# 依存関係インストール
uv sync

# 開発サーバー起動（http://127.0.0.1:8000）
uv run mkdocs serve

# 本番ビルド（site/ に出力）
uv run mkdocs build
```

## コンテンツ編集ルール

### 記載OK
- 配信日時、曲名、ゲームタイトル等の事実情報
- YouTube埋め込み/リンク
- 公式発表情報（マイルストーン、衣装発表）
- タイムスタンプ付きリンク

### 記載NG（厳守）
- 歌詞（著作権侵害）
- 配信のスクリーンショット（許可なき画像使用）
- メンバー限定の内容詳細（有料コンテンツの価値毀損）
- 本人が嫌がる情報
- 質問/回答の全文転載

### YouTube埋め込み
- **埋め込み使用**: デビュー配信、記念配信など重要なもののみ（トップページ）
- **リンク使用**: 通常の配信アーカイブ（テーブル形式）

### 日付順の方針
- **全ページ共通**: 古い順（時系列で活動を追う）
- 新規層がwikiを見ることを想定し、最初から順を追って理解できるようにする

## Markdown記法（Material for MkDocs）

### テーブル
```markdown
| 日付 | 内容 | リンク |
|------|------|--------|
| 2025/xx/xx | 内容 | [▶️](URL) |
```

## 参考資料

- 参照プロジェクト: `E:\10_devel\Cloudflare\wiki\mashiro`
- [Material for MkDocs ドキュメント](https://squidfunk.github.io/mkdocs-material/)

## デプロイ

GitHubにpushすると Cloudflare Pages が自動でビルド・デプロイする。

## playwright MCP

必要に応じて playwright MCP を利用してブラウザでの表示を確認する。
このとき、サーバーは起動済みとしてよく、起動コマンドの実行は不要です。
