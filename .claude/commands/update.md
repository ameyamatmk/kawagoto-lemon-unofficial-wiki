# Wiki プッシュ・PR作成コマンド

wiki の変更をリモートにプッシュし、PR を作成する。

## 作業手順

### 1. 現在の状態確認

- `git status` で変更ファイルを確認
- `git branch --show-current` で現在のブランチを確認

### 2. 差分の確認

`origin/main` からの差分を確認して、changelog に記載する更新内容を把握する。

```
git diff origin/main --stat
git diff origin/main --name-only
```

### 3. changelog 更新内容のレビュー

差分から更新内容を要約し、**ユーザーにレビューを依頼する**。

AskUserQuestion ツールを使って以下を確認:
- 提案した更新内容でよいか
- 修正が必要か
- **サイレント修正**（changelog に追加しない）かどうか

### 4. changelog.md と index.md の更新

**通常の更新の場合:**

1. `docs/changelog.md` のテーブルに新しい行を追加
   - 日付: 今日の日付（YYYY/MM/DD形式）
   - 内容: レビュー済みの更新内容
   - **重要**: 新しいエントリはテーブルの**一番下**に追加する（古い順）

2. `docs/index.md` の最終更新日を今日の日付に更新
   ```html
   <small style="display: block; text-align: right;">最終更新: YYYY/MM/DD</small>
   ```

**サイレント修正の場合:**

- changelog.md への追加をスキップ
- index.md の最終更新日も変更しない
- そのままプッシュへ進む

### 5. ブランチ準備

現在のブランチが `main` の場合:
- 新しい feature ブランチを作成する
- ブランチ名: `update/YYYYMMDD` または変更内容に応じた名前

```
git checkout -b update/YYYYMMDD
```

### 6. コミット

```
git add .
git commit -m "docs: 更新内容の要約"
```

### 7. プッシュ

ブランチをリモートにプッシュする。

```
git push -u origin <ブランチ名>
```

### 8. PR 作成

`gh` コマンドで PR を作成する。

```
gh pr create --title "更新内容の要約" --body "## 変更内容
- 変更点1
- 変更点2
"
```

作成した PR の URL をユーザーに伝え、**マージの指示を待つ**。

### 9. ローカルの main を最新化

ユーザーがマージしたら、ローカルの main ブランチを origin/main に合わせる。

**重要**: `git pull` ではなく `git reset --hard` を使う（マージコミットを作らないため）

```
git checkout main
git fetch origin --prune
git reset --hard origin/main
```

マージ済みのブランチを削除する。

```
git branch -d <ブランチ名>
```

## 注意事項

- コミットメッセージは日本語で、Conventional Commits 形式（`docs:`, `feat:` など）
- PR タイトルも日本語でわかりやすく
- 変更がない場合は何もせず終了
