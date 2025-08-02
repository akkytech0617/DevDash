# DevDash プロジェクトルール

このドキュメントは、DevDashプロジェクトで開発を行う際に従うべきルールと慣習を定義しています。

## コミットメッセージルール

### フォーマット
```
<type>(<scope>): <subject>

<body>

<footer>
```

### 基本ルール
- **言語**: 英語
- **件名の長さ**: 50文字以内
- **本文の行長**: 72文字以内
- **件名の最初は大文字**、末尾にピリオド不要
- **命令形を使用**: "Fix bug" ✅ / "Fixed bug" ❌

### Type（必須）
| Type | 説明 | 例 |
|------|------|-----|
| `feat` | 新機能追加 | `feat: add user authentication` |
| `fix` | バグ修正 | `fix: resolve login validation error` |
| `docs` | ドキュメント変更 | `docs: update API documentation` |
| `style` | コード整形（機能に影響なし） | `style: format code with prettier` |
| `refactor` | リファクタリング | `refactor: simplify user service logic` |
| `test` | テスト追加・修正 | `test: add unit tests for auth module` |
| `chore` | ビルド・補助ツール等 | `chore: update dependencies` |
| `perf` | パフォーマンス改善 | `perf: optimize database queries` |
| `ci` | CI/CD関連 | `ci: add GitHub Actions workflow` |
| `build` | ビルドシステム変更 | `build: update webpack configuration` |
| `revert` | コミット取り消し | `revert: revert feat: add feature X` |

### Scope（オプション）
プロジェクトの影響範囲を示します：

| Scope | 説明 |
|-------|------|
| `frontend` | フロントエンド（Svelte） |
| `backend` | バックエンド（Rust） |
| `api` | API関連 |
| `ui` | UI/UXコンポーネント |
| `config` | 設定ファイル |
| `deps` | 依存関係 |
| `docs` | ドキュメント |

### 例

#### 良い例
```
feat(frontend): add dashboard navigation component

- Add responsive navigation bar
- Implement route highlighting
- Support for mobile menu toggle

Closes #123
```

```
fix(backend): resolve database connection timeout

The connection pool was not properly configured for production
environment. Updated pool settings to handle concurrent requests.

Fixes #456
```

```
docs: add Tauri setup guide

Create comprehensive setup documentation for new developers
including troubleshooting section and reference links.
```

#### 悪い例
```
update stuff
```

```
fixed a bug
```

```
feat: Added new feature for users to login and logout and also fixed some styling issues
```

## ブランチ命名規則

### フォーマット
```
<type>/<ticket-number>-<short-description>
```

### 例
- `feat/123-user-authentication`
- `fix/456-login-validation`
- `docs/789-api-documentation`
- `refactor/101-user-service`

## プルリクエストルール

### タイトル
- コミットメッセージと同じフォーマット
- 概要が分かりやすい内容

### 説明（テンプレート）
```markdown
## 概要
<!-- 変更内容の簡潔な説明 -->

## 変更内容
- [ ] 機能A の追加
- [ ] バグB の修正
- [ ] ドキュメントC の更新

## テスト方法
<!-- 動作確認の手順 -->

## 関連Issue
Closes #123

## 追加情報
<!-- 必要に応じて -->
```

## コードレビューガイドライン

### レビュアーの視点
- [ ] **機能性**: 要件を満たしているか
- [ ] **可読性**: コードが理解しやすいか
- [ ] **保守性**: 将来の変更に対応しやすいか
- [ ] **セキュリティ**: 脆弱性はないか
- [ ] **パフォーマンス**: 性能に問題はないか
- [ ] **テスト**: 適切にテストされているか

### レビューコメント例
```
# 改善提案
suggestion: この部分はより効率的に書けます
```

```
# 必須修正
必須: セキュリティ上の懸念があります
```

```
# 質問
question: この処理の意図を教えてください
```

## ファイル・ディレクトリ構成ルール

### 基本構成
```
DevDash/
├── src/                    # フロントエンド
│   ├── components/         # 再利用可能コンポーネント
│   ├── pages/             # ページコンポーネント
│   ├── stores/            # 状態管理
│   ├── utils/             # ユーティリティ関数
│   └── types/             # TypeScript型定義
├── src-tauri/             # バックエンド
│   ├── src/
│   │   ├── commands/      # Tauriコマンド
│   │   ├── models/        # データモデル
│   │   └── utils/         # ユーティリティ
├── docs/
│   ├── dev/               # 開発者向けドキュメント
│   └── user/              # ユーザー向けドキュメント
└── tests/                 # テストファイル
```

### 命名規則
- **ファイル**: `kebab-case.ext`
- **ディレクトリ**: `kebab-case`
- **コンポーネント**: `PascalCase.svelte`
- **Rust**: `snake_case.rs`

## 開発ワークフロー

### 1. 新機能開発
1. Issueの作成・確認
2. ブランチ作成 (`feat/xxx-feature-name`)
3. 開発・テスト
4. コミット（ルール遵守）
5. プルリクエスト作成
6. コードレビュー
7. マージ

### 2. バグ修正
1. バグ報告Issue確認
2. ブランチ作成 (`fix/xxx-bug-name`)
3. 修正・テスト
4. コミット
5. プルリクエスト
6. 緊急度に応じて迅速レビュー・マージ

### 3. ドキュメント更新
1. 必要性の確認
2. `docs/xxx-update-name` ブランチ作成
3. ドキュメント作成・更新
4. レビュー・マージ

## 品質基準

### コード品質
- **TypeScript**: 型エラーゼロ
- **Rust**: `cargo clippy` 警告ゼロ
- **フォーマット**: `prettier` / `cargo fmt` 適用済み
- **テスト**: 新機能には必須、バグ修正時は推奨

### ドキュメント品質
- **最新性**: コードと同期している
- **完全性**: セットアップから実行まで完結
- **明確性**: 初心者でも理解可能
- **参考リンク**: 公式ドキュメント等へのリンク

## ツール設定

### 推奨エディタ設定
```json
// .vscode/settings.json
{
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll": true
  },
  "rust-analyzer.checkOnSave.command": "clippy"
}
```

### Git Hooks（推奨）
```bash
# pre-commit: フォーマット・Lint確認
#!/bin/sh
npm run check
cargo fmt --check
cargo clippy -- -D warnings
```

## 参考リンク

### コミットメッセージ
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Angular Commit Message Guidelines](https://github.com/angular/angular/blob/main/CONTRIBUTING.md#commit)

### コードレビュー
- [Google Code Review Guidelines](https://google.github.io/eng-practices/review/)
- [GitHub Pull Request Best Practices](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests)

### プロジェクト管理
- [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow)
- [Semantic Versioning](https://semver.org/)