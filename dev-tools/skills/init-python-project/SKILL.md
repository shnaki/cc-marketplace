---
name: init-python-project
description: "Python プロジェクトの CLAUDE.md を生成する。新しい Python プロジェクトのセットアップ時や、既存プロジェクトに CLAUDE.md を追加する時に使用する。"
user-invocable: true
argument-hint: "[プロジェクトの説明]"
---

# Python プロジェクト CLAUDE.md 生成

# 指示

以下の手順で、現在のプロジェクトに最適化された CLAUDE.md を生成する。

## ステップ 1: プロジェクト構成の調査

以下のファイル・ディレクトリを確認する:

1. `pyproject.toml` — プロジェクト名、Python バージョン、依存パッケージ、ツール設定（ruff, pyright, pytest）
2. `src/` または プロジェクトルート — ソースコードのレイアウト
3. `tests/` — テストの構成
4. `.pre-commit-config.yaml` — pre-commit フック設定
5. `.github/workflows/` — CI 設定
6. `Makefile` — 利用可能なコマンド
7. 既存の `CLAUDE.md` — 上書き前に内容を確認

## ステップ 2: テンプレートの適用

`template-claude-md.md` をベースに、ステップ 1 で得た情報に基づいてカスタマイズする。

### カスタマイズポイント

- **目的**: `$ARGUMENTS` またはプロジェクトの README から目的を記述
- **行の長さ**: pyproject.toml の ruff 設定から実際の値を取得（88文字 or 120文字）
- **テストフレームワーク**: pytest 以外を使用している場合は置き換え
- **非同期テスト**: anyio 以外（asyncio 等）を使用している場合は調整
- **カバレッジ要件**: pyproject.toml の `fail_under` 値を反映
- **追加ツール**: mypy, bandit 等を使用している場合は追加
- **ディレクトリ構成**: 実際のパスに合わせて調整

## ステップ 3: CLAUDE.md の生成

プロジェクトルートに `CLAUDE.md` を生成する。既存ファイルがある場合はユーザーに確認してから上書きする。

## 注意事項

- テンプレートを盲目的にコピーしない。pyproject.toml の設定を正確に反映する
- プロジェクトが使用していないツールのセクションは削除する
- 日本語で記述する
