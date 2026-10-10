# template-base

<!-- テンプレートから作成した場合は、この README をプロジェクトの内容に書き換える -->

このリポジトリは小規模プロジェクトやドキュメント管理を行うリポジトリのテンプレートとして使用する。

## セットアップ

1. 次をインストールする

   - [mise](https://mise.jdx.dev/getting-started.html)
   - [GitHub CLI](https://cli.github.com/)
   - [Claude Code](https://code.claude.com/docs/en/overview)

2. 設定ファイルを信頼する

   ```bash
   mise trust
   ```

3. 開発環境を構築する

   ```bash
   mise run setup
   ```

4. GitHub CLI と Claude Code を認証する

   ```bash
   gh auth login
   claude auth login
   ```

5. dotfiles を配置する

   ```bash
   chezmoi init --apply maerchen-cloud/dotfiles
   ```

### Dev Container

Dev Container を用いて開発することもできる。
VS Code と Dev Containers 拡張機能が必要である。

コンテナの作成時に手順 1 から 3 が自動で実行される。
手順 4 と 5 はコンテナ内のターミナルで手動で実行する。

次の名前付きボリュームは、同じマシン内の他コンテナと共有される。
そのため、2 つ目以降のコンテナでは手順 4 と 5 を実行しなくてよい。

| ボリューム | 内容 | マウント先 |
| --- | --- | --- |
| `claude-code-config` | Claude Code の設定と認証情報 | `~/.claude/` |
| `gh-config` | GitHub CLI の設定と認証情報 | `~/.config/gh/` |
| `chezmoi-source` | dotfiles の元ファイル | `~/.local/share/chezmoi/` |

## 開発

### コミット

コミットメッセージは Conventional Commits に準拠する。
lefthook の `commit-msg` フックが検証するため、準拠しない場合はコミットできない。

### 静的解析

lefthook の `pre-commit` フックが静的解析を実行し、整形した内容をステージする。
手動で静的解析を実行する場合は次のコマンドを用いる。

```bash
lefthook run pre-commit --all-files
```

## ドキュメント

| ドキュメント | 内容 |
| --- | --- |
| [コントリビューションガイド](https://github.com/maerchen-cloud/.github/blob/main/.github/CONTRIBUTING.md) | 組織共通の開発規約 |
