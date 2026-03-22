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
```

- ステージ済みの変更がある場合: そのままステップ 2 へ
- ステージ済みの変更がない場合: `git diff` で未ステージの変更を確認し、ユーザーに何をステージするか確認してから `git add` する

## ステップ 2: コミットメッセージの作成

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

## ステップ 3: コミットの実行

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

## ステップ 4: 確認

```bash
git log -1 --stat
```

コミットが正しく作成されたことを確認して結果を報告する。
