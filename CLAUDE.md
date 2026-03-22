# 開発ガイドライン

このリポジトリは shnaki の個人用 Claude Code マーケットプレイス。

## 構造

```
cc-marketplace/
├── .claude-plugin/marketplace.json   # マーケットプレイス定義
├── .claude/skills/                   # メタスキル（マーケットプレイス管理用）
├── dev-tools/                        # メインプラグイン
│   ├── .claude-plugin/plugin.json    # プラグインメタデータ
│   └── skills/                       # スキル定義
├── CLAUDE.md                         # このファイル
└── README.md
```

## スキル追加手順

1. `dev-tools/skills/<skill-name>/` ディレクトリを作成
2. `SKILL.md` を YAML frontmatter + Markdown 形式で作成
3. 必要に応じて `template-*.md` や `examples.md` を追加
4. `README.md` のスキル一覧を更新
5. `dev-tools/.claude-plugin/plugin.json` の version をインクリメント

## SKILL.md の形式

```yaml
---
name: skill-name
description: "スキルの説明（自動呼び出し判定に使われる）"
user-invocable: true
argument-hint: "[引数の説明]"
---
```

frontmatter の後に Markdown で指示を記述する。

## 命名規約

- スキル名: kebab-case（例: `init-go-project`）
- エージェント名: kebab-case（例: `code-reviewer`）
- description は日本語で記述

## コミット・PR規約

- `co-authored-by` や類似表現は絶対に記載しないこと。特に、コミットメッセージや PR の作成に使ったツールには言及しないこと。

### コミット規約

- **Conventional Commits** 形式: `<type>: <説明>`（日本語で記述）
- プリフィックス: feat, fix, docs, style, refactor, perf, test, build, ci, chore, revert
