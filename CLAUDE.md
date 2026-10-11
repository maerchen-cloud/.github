# CLAUDE.md

## 規約

コントリビューションの規約は @.github/CONTRIBUTING.md に従う。

## 留意点

### Reusable Workflow

Reusable Workflow を変更すると、参照しているほかのリポジトリの CI に影響するため、後方互換性に注意する。

### Renovate

`renovate.json` は `default.json` を参照しているだけのため、Renovate の設定を変更するときは `default.json` を修正する。
