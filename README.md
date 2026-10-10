# .github

このリポジトリは `maerchen-cloud` 組織の共通の設定やドキュメントを管理する。

## コミュニティヘルスファイル

コミュニティヘルスファイルとは、GitHub が定めているテンプレートや規約などの特定のファイルを指す。
コミュニティヘルスファイルは、各リポジトリに同名のファイルが存在しない場合、このリポジトリのファイルの内容が各リポジトリに適用される。
適用されるのはこのリポジトリが public の場合に限られるため、現時点では適用されない。

| ファイル | 内容 |
| --- | --- |
| `.github/ISSUE_TEMPLATE/` | Issue のテンプレート |
| `.github/PULL_REQUEST_TEMPLATE.md` | プルリクエスト本文のテンプレート |
| `.github/CONTRIBUTING.md` | 組織共通の開発規約 |

## Reusable Workflow

| ファイル | 検証する対象 |
| --- | --- |
| `reusable-lint.yml` | コードの整形と Lint |
| `reusable-secret-scan.yml` | シークレットの混入 |
| `reusable-pull-request-title.yml` | プルリクエストタイトル |

各リポジトリは次のように Reusable Workflow を呼び出す。

```yaml
jobs:
  lint:
    uses: maerchen-cloud/.github/.github/workflows/reusable-lint.yml@main
```

## Renovate

`default.json` では Renovate の共通設定を定義する。
各リポジトリは `renovate.json` の `extends` で次のように Renovate の共通設定を参照する。

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["local>maerchen-cloud/.github"]
}
```

このリポジトリ自身の `renovate.json` も、他のリポジトリと同じ書き方で `default.json` を参照している。

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
| [コントリビューションガイド](.github/CONTRIBUTING.md) | 組織共通の開発規約 |
