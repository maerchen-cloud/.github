# コントリビューションガイド

`maerchen-cloud` 組織のすべてのリポジトリに適用する規約を定める。

## type

type は変更の種類を表す。
ブランチ名とコミットメッセージ、プルリクエストのタイトルで使用する。

<!-- type の一覧は .github/workflows/reusable-pull-request-title.yml と一致させる -->

- `feat`: 新機能
- `fix`: バグ修正
- `docs`: ドキュメント
- `style`: コードスタイル。フォーマットやセミコロンなど、動作に影響しない変更
- `refactor`: リファクタリング
- `perf`: パフォーマンス改善
- `test`: テストの追加と修正
- `build`: ビルドシステムと依存関係の変更
- `ci`: 継続的インテグレーションと継続的デリバリーに関する変更
- `chore`: その他の雑多な変更。設定など機能に直接関係しない変更
- `revert`: 過去のコミットの取り消し

## Issue

Issue は次のテンプレートに沿って作成する。

- バグ報告は `.github/ISSUE_TEMPLATE/bug_report.md` を使う
- 機能要望は `.github/ISSUE_TEMPLATE/feature_request.md` を使う
- テンプレートリポジトリへの反映は `.github/ISSUE_TEMPLATE/template_reflection.md` を使う

## ブランチ

`main` ブランチには直接プッシュしない。
作業ブランチを作成する。

作業ブランチ名は次の形式にする。

```text
<type>/<topic>
```

| 要素 | 内容 |
| --- | --- |
| `type` | [type](#type) のいずれか |
| `topic` | 変更内容が読み取れる短い名前 |

例を次に示す。

- `fix/broken-reusable-workflow-path`
- `docs/add-setup-guide`

## コミットメッセージ

[Conventional Commits](https://www.conventionalcommits.org/ja/v1.0.0/) に準拠する。
コミットメッセージは日本語で書く。

### フォーマット

```text
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

| 要素 | 内容 | 要否 |
| --- | --- | --- |
| `type` | [type](#type) のいずれか | 必須 |
| `scope` | 変更の影響範囲 | 任意 |
| `description` | 変更内容の簡潔な説明 | 必須 |
| `body` | 変更の詳細な説明 | 任意 |
| `footer` | 補足情報 | 任意 |

### 破壊的変更

破壊的変更は次のいずれかの方法で示す。

- `:` の直前に `!` を付与する。`feat!: Node 6 のサポートを終了する` のように書く
- `footer` に `BREAKING CHANGE:` と説明を記述する

## プルリクエスト

プルリクエストを作成して `main` ブランチにマージする。

### タイトル

`<type>[optional scope]: <description>` の形式にする。
各要素は[コミットメッセージのフォーマット](#フォーマット)に従う。

### 本文

`.github/PULL_REQUEST_TEMPLATE.md` に沿って記述する。

## テンプレートリポジトリへの反映

テンプレートリポジトリにも存在するファイルを変更した場合は、テンプレートリポジトリに Issue を作成して反映を依頼する。
