---
name: create-skill
description: "dev-tools プラグインに新しいスキルを追加する"
user-invocable: true
argument-hint: "<スキル名> [スキルの説明]"
---

# 新スキル作成

# 指示

`dev-tools/skills/` 配下に新しいスキルのテンプレートを生成する。

## 手順

1. `$ARGUMENTS` からスキル名（kebab-case）と説明を取得する
2. `dev-tools/skills/<スキル名>/` ディレクトリを作成する
3. 以下の内容で `SKILL.md` を生成する:

```markdown
---
name: <スキル名>
description: "<スキルの説明>"
user-invocable: true
argument-hint: "[引数の説明]"
---

# <スキル名>

# 指示

TODO: スキルの指示をここに記述する
```

4. `README.md` のスキル一覧テーブルに新しいスキルを追加する
5. 作成したファイルの場所をユーザーに報告し、指示の記述を促す
