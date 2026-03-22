---
name: bump-version
description: "dev-tools プラグインのバージョンをインクリメントする"
user-invocable: true
argument-hint: "[major|minor|patch]"
---

# バージョンアップ

# 指示

`dev-tools/.claude-plugin/plugin.json` のバージョンをインクリメントする。

## 手順

1. `dev-tools/.claude-plugin/plugin.json` を読み込む
2. 現在の `version` フィールドを取得する（セマンティックバージョニング: X.Y.Z）
3. `$ARGUMENTS` に基づいてバージョンをインクリメントする:
   - `major`: X+1.0.0
   - `minor`: X.Y+1.0
   - `patch`（デフォルト）: X.Y.Z+1
4. plugin.json を更新する
5. 変更をコミットする: `chore: バージョンを X.Y.Z に更新`
