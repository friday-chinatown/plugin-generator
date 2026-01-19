---
name: create-plugin
description: 新しいClaude Codeプラグインの雛形を生成する
argument-hint: <plugin-name>
allowed-tools:
  - Bash
  - Write
  - Read
  - Glob
---

# Create Plugin Command

ユーザーが `/create-plugin <plugin-name>` コマンドを実行した際、以下の手順でプラグイン雛形を生成してください。

## 引数の処理

- `<plugin-name>` が指定されている場合: その名前を使用
- 引数がない場合: `my-awesome-plugin` をデフォルト名として使用

## バリデーション

プラグイン名は以下のルールに従う必要があります：
- 英小文字で始まること
- 英小文字、数字、ハイフンのみ使用可能
- 3文字以上50文字以下

無効な名前の場合はエラーメッセージを表示してください。

## ディレクトリ作成

現在の作業ディレクトリにプラグインのディレクトリ構造を作成します。

既存のディレクトリがある場合は警告を表示し、上書きしないでください。

## 生成するファイル構成

```
<plugin-name>/
├── .claude-plugin/
│   └── plugin.json
├── commands/
│   └── hello.md
├── README.md
└── .gitignore
```

### plugin.json の内容

```json
{
  "name": "<plugin-name>",
  "description": "<plugin-name> - Claude Code plugin",
  "version": "1.0.0",
  "author": {
    "name": "Your Name"
  },
  "capabilities": [
    "slashCommands"
  ]
}
```

### hello.md の内容

```markdown
---
name: hello
description: ユーザーに友好的なメッセージで挨拶する
---

# Hello Command

ユーザーに温かく挨拶し、今日はどのような手助けができるか尋ねてください。
```

### README.md の内容

```markdown
# <plugin-name>

## 概要

<plugin-name> プラグインの説明をここに記述してください。

## インストール

Claude Codeでプラグインを有効化：

1. このディレクトリをクローンまたはコピー
2. Claude Codeの設定でプラグインディレクトリを指定

## 使い方

### 利用可能なコマンド

- `/<plugin-name>:hello` - 挨拶メッセージを表示

## 開発

### 新しいコマンドを追加

1. `commands/` ディレクトリに新しい `.md` ファイルを作成
2. ファイル名がコマンド名になります（例: `goodbye.md` → `/<plugin-name>:goodbye`）

### コマンドファイルの形式

\`\`\`markdown
---
name: command-name
description: コマンドの説明
---

# Command Name

コマンドの動作を記述してください。
\`\`\`
```

### .gitignore の内容

```
# Dependencies
node_modules/

# IDE
.vscode/
.idea/

# OS
.DS_Store
Thumbs.db

# Logs
*.log
npm-debug.log*
```

## 完了報告

全てのファイルが生成されたら、以下の形式でユーザーに報告：

```
プラグイン雛形が生成されました

ディレクトリ: <plugin-name>/

生成されたファイル:
- .claude-plugin/plugin.json (マニフェスト)
- commands/hello.md (サンプルコマンド)
- README.md (ドキュメント)
- .gitignore (Git除外設定)

次のステップ:
1. cd <plugin-name>
2. plugin.json を編集してプラグイン情報をカスタマイズ
3. commands/ に新しいコマンドを追加
4. プラグインをClaude Codeに登録してテスト

ヒント:
- commands/ディレクトリに .md ファイルを追加するだけで新しいコマンドが作成できます
- ファイル名がコマンド名になります
```

## エラーハンドリング

- 既存のディレクトリがある場合: 「ディレクトリ '<plugin-name>' は既に存在します。別の名前を指定するか、既存のディレクトリを削除してください。」
- 無効なプラグイン名: 「プラグイン名 '<plugin-name>' は無効です。英小文字で始まり、英小文字、数字、ハイフンのみ使用可能です（3-50文字）。」
- ファイル作成エラー: エラーの詳細を表示し、部分的に作成されたファイルの状況を報告
