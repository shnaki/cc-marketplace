---
name: cm
description: "Conventional Commits 形式で git commit を実行する。コード変更のコミット時に使用する。"
user-invocable: true
argument-hint: "[コミットメッセージまたは変更の説明]"
---

# Conventional Commit

# 指示

変更内容を Conventional Commits 形式でコミットする。

## ステップ 1: 変更内容の確認

```bash
git status
git diff --staged
git diff
```

すべての変更（ステージ済み・未ステージ・未追跡）を把握する。

## ステップ 2: 変更の分類とグループ化

変更内容を論理的なテーマごとにグループ化する。

### 分類の基準

- **機能単位**: 同じ機能に関する変更は1つのグループ
- **種類単位**: ドキュメント変更、テスト追加、リファクタリング等は別グループ
- **依存関係**: 他の変更に依存する場合は依存先を先にコミット

### 判定

- 全変更が1つのテーマに収まる → そのままステップ 3 へ（1コミット）
- 複数テーマがある → グループごとにステップ 3〜5 を繰り返す

グループ化の判断をユーザーに提示し、確認を取ってから進める。

## ステップ 3: ステージング

グループに含まれるファイルのみをステージする:

```bash
git add <file1> <file2> ...
```

- `git add -A` や `git add .` は使わない。対象ファイルを明示的に指定する
- 1ファイル内に複数テーマの変更がある場合は `git add -p` でハンク単位でステージする

## ステップ 4: コミットメッセージの作成

### 形式

```
<type>(<scope>)?: <subject>

<body>

<footer>
```

### type（必須）

- `feat`: 新機能
- `fix`: バグ修正
- `docs`: ドキュメント変更
- `refactor`: 振る舞いを変えない内部改善
- `test`: テスト追加・修正
- `chore`: 雑務・メンテナンス
- `ci`: CI 設定変更
- `build`: ビルド/依存関係変更
- `perf`: 性能改善
- `revert`: 変更取り消し

### scope（任意）

変更の影響範囲。不要なら省略する。

### subject（必須）

- 簡潔な日本語で記述
- 文末の句点は付けない

### body（任意）

- 変更の理由と背景を説明
- 何を変更したかではなく、なぜ変更したかを記述

### footer（該当時のみ）

- 破壊的変更: `type(scope)!: ...` 形式、または body に `BREAKING CHANGE:` を記載
- ユーザー報告に基づく変更: `git commit --trailer "Reported-by:<name>"`
- GitHub Issue 関連: `git commit --trailer "Github-Issue:#<number>"`

### 禁止事項

- `co-authored-by` や類似表現は絶対に記載しない
- コミットメッセージや PR の作成に使ったツールには言及しない

## ステップ 5: コミットの実行

`$ARGUMENTS` が指定されている場合はそれをコミットメッセージの参考にする。

```bash
git commit -m "<type>(<scope>): <subject>"
```

body や footer が必要な場合は HEREDOC を使用する:

```bash
git commit -m "$(cat <<'EOF'
<type>(<scope>): <subject>

<body>

<footer>
EOF
)"
```

## ステップ 6: 確認と次のグループ

```bash
git log -1 --stat
```

- 残りのグループがある場合 → ステップ 3 に戻る
- 全グループ完了 → 全コミットのサマリーを報告する
