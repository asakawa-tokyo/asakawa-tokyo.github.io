# Contributing Guide

このドキュメントでは、Issue・PR の命名規則と運用ガイドラインを定めます。

## Issue の命名規則

### 形式

```
[Type] 概要を一文で書く
```

### Type 一覧

| Type | 用途 |
|---|---|
| `[Bug]` | 不具合・予期しない動作の報告 |
| `[Feature]` | 新機能の提案・要望 |
| `[Docs]` | ドキュメントの追加・修正 |
| `[Refactor]` | 機能変更を伴わないコード整理 |
| `[Chore]` | 依存パッケージ・CI・ビルド設定の変更 |
| `[Question]` | 質問・相談 |

### 例

```
[Bug] ログイン後にセッションが切れる
[Feature] ダークモード対応を追加する
[Docs] README のセットアップ手順を更新する
[Refactor] 認証モジュールのディレクトリ構成を整理する
[Chore] 依存パッケージを最新化する
```

### ルール

- タイトルは **「何が起きているか／何をしたいか」** を一文で書く
- 動詞で締める（「〜できない」「〜を追加する」など）
- 50文字以内を目安にする
- 詳細は本文に書く（タイトルに詰め込まない）

## PR の命名規則

[Conventional Commits](https://www.conventionalcommits.org/ja/) 形式を採用します。

### 形式

```
<type>(<scope>): <summary>
```

破壊的変更（Breaking Change）を含む場合は `!` を付けます。

```
<type>(<scope>)!: <summary>
```

- `scope` は省略可能。影響範囲が明確なときのみ記載する
- `summary` は英語・日本語どちらでも可（チーム内で統一すること）
- 破壊的変更とは、既存の API・インターフェース・動作との後方互換性が失われる変更のこと

### Type 一覧

| Type | 用途 |
|---|---|
| `feat` | 新機能の追加 |
| `fix` | バグ修正 |
| `docs` | ドキュメントのみの変更 |
| `refactor` | 機能変更を伴わないコード整理 |
| `test` | テストの追加・修正 |
| `chore` | ビルド・依存関係・CI など |
| `perf` | パフォーマンス改善 |
| `revert` | 以前のコミットを元に戻す |

### 例

```
feat(auth): Google OAuthログインを追加
fix(api): レート制限超過時に500でなく429を返す
docs(readme): ローカル環境構築手順を追記
refactor(db): N+1クエリを解消
test(user): ユーザー削除のエッジケースを追加
chore(deps): lodash を 4.17.21 に更新
```

破壊的変更の例：

```
feat(api)!: レスポンスのフィールド名をスネークケースに変更
refactor(auth)!: JWTからセッション認証に移行
```

> 破壊的変更の PR は、本文の `BREAKING CHANGE:` セクションに影響範囲と移行方法を記載してください。
>
> ```
> BREAKING CHANGE: /users エンドポイントのレスポンスが変更されました。
> `userName` → `user_name`、`createdAt` → `created_at` に変更してください。
> ```


## Issue と PR の紐付け

PR タイトルまたは本文に Issue 番号を記載してください。

```
fix(auth): セッション切れのバグを修正 (#123)
```

PR 本文に以下のキーワードを含めると、マージ時に Issue が**自動クローズ**されます。

```
Closes #123
Fixes #123
Resolves #123
```
