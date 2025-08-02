# DevDash プロジェクト開発ガイド

このファイルはClaude Codeがプロジェクトの慣習とルールを理解するためのガイドです。

## プロジェクト概要
- **プロジェクト名**: DevDash
- **技術スタック**: Tauri + Svelte + TypeScript
- **対象プラットフォーム**: Windows, macOS
- **開発環境**: GitHub Codespace

## ドキュメント作成ルール

### 開発者向けドキュメント
- **保存場所**: `docs/dev/` 配下に作成すること
- **形式**: Markdown形式（`.md`拡張子）
- **言語**: 日本語
- **必須要素**:
  - 手順の詳細説明
  - 関連する公式ドキュメントのURL
  - トラブルシューティング情報
  - 実行可能なコマンド例

### ドキュメント命名規則
- ケバブケース（`kebab-case`）を使用
- 内容が分かりやすい名前をつける
- 例: `tauri-setup.md`, `deployment-guide.md`, `api-reference.md`

## コーディング規則

### ファイル構成
```
src/                    # フロントエンド (Svelte + TypeScript)
src-tauri/             # バックエンド (Rust)
docs/
  ├── dev/             # 開発者向けドキュメント
  └── user/            # ユーザー向けドキュメント（将来用）
```

### TypeScript/Svelte
- 厳密な型チェックを有効にする
- コンポーネントは`src/components/`に配置
- ユーティリティ関数は`src/utils/`に配置

### Rust
- `cargo fmt`でフォーマット
- `cargo clippy`で静的解析
- エラーハンドリングを適切に行う

## 開発ワークフロー

### 新機能開発時
1. 関連するドキュメントが存在するか確認
2. 存在しない場合は`docs/dev/`にドキュメントを作成
3. 実装前にドキュメントをレビュー
4. 実装後にドキュメントを更新

### ドキュメント更新タイミング
- 新しいセットアップ手順が追加された時
- API仕様が変更された時
- 新しいツールや依存関係が追加された時
- トラブルシューティング情報が更新された時

## コマンド参考

### よく使用するコマンド
```bash
# 開発サーバー起動
npm run dev

# デスクトップアプリ開発
npm run tauri:dev

# 型チェック
npm run check

# 本番ビルド
npm run tauri:build
```

### Rust関連
```bash
# フォーマット
cargo fmt

# 静的解析
cargo clippy

# テスト実行
cargo test
```

## Claude Codeへの指示

### ドキュメント作成時の必須事項
- 開発者向けドキュメントは必ず`docs/dev/`配下に作成
- 公式リファレンスURLを含める
- 実際に動作するコマンド例を記載
- トラブルシューティング情報を含める

### 実装時の注意点
- 既存のコード規約に従う
- セキュリティベストプラクティスを遵守
- 適切なエラーハンドリングを実装
- 必要に応じてドキュメントも同時更新

## 参考リンク
- [Tauri公式ドキュメント](https://tauri.app/)
- [Svelte公式ドキュメント](https://svelte.dev/)
- [Claude Code公式ドキュメント](https://docs.anthropic.com/en/docs/claude-code)