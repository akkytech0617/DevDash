# Tauri開発環境セットアップガイド

このドキュメントは、DevDashプロジェクトでTauri + Svelte + TypeScript環境をセットアップするための手順書です。

## 前提条件

### システム要件
- **Node.js** v16以上
- **Rust** 1.77.2以上
- **Git**

### OS別追加要件

#### Windows
- **Microsoft C++ Build Tools** または **Visual Studio**
- **WebView2** (Windows 10/11では通常プリインストール済み)

#### macOS
- **Xcode Command Line Tools**
```bash
xcode-select --install
```

#### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install libwebkit2gtk-4.0-dev \
    build-essential \
    curl \
    wget \
    file \
    libssl-dev \
    libgtk-3-dev \
    libayatana-appindicator3-dev \
    librsvg2-dev
```

## セットアップ手順

### 1. Rustのインストール

```bash
# Rustupを使用してRustをインストール
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# 環境変数を読み込み
source $HOME/.cargo/env

# インストール確認
rustc --version
cargo --version
```

### 2. プロジェクトのクローン

```bash
git clone <repository-url>
cd DevDash
```

### 3. 依存関係のインストール

```bash
# Node.js依存関係をインストール
npm install

# Tauri CLIをグローバルインストール（オプション）
npm install -g @tauri-apps/cli
```

### 4. 開発サーバーの起動

#### Webブラウザでの開発
```bash
npm run dev
```
ブラウザで `http://localhost:1420` にアクセス

#### デスクトップアプリでの開発
```bash
npm run tauri:dev
```

## プロジェクト構造

```
DevDash/
├── src/                    # フロントエンド (Svelte + TypeScript)
│   ├── App.svelte
│   ├── main.ts
│   └── app.css
├── src-tauri/              # バックエンド (Rust)
│   ├── src/
│   │   └── main.rs
│   ├── Cargo.toml
│   ├── tauri.conf.json
│   └── build.rs
├── public/                 # 静的ファイル
├── dist/                   # ビルド出力 (自動生成)
└── package.json
```

## 利用可能なスクリプト

| コマンド | 説明 |
|----------|------|
| `npm run dev` | 開発サーバー起動（Web版） |
| `npm run build` | 本番用ビルド |
| `npm run preview` | ビルド結果のプレビュー |
| `npm run check` | TypeScript型チェック |
| `npm run tauri:dev` | デスクトップアプリ開発モード |
| `npm run tauri:build` | デスクトップアプリビルド |

## 設定ファイル

### `src-tauri/tauri.conf.json`
Tauriアプリケーションの主要設定ファイル
- アプリケーション情報
- ウィンドウ設定
- セキュリティ設定
- バンドル設定

### `vite.config.ts`
Vite（ビルドツール）の設定ファイル
- Svelteプラグイン設定
- 開発サーバー設定
- Tauri用の最適化設定

## トラブルシューティング

### よくある問題

#### 1. Rustコンパイルエラー
```bash
# Rustツールチェーンを最新に更新
rustup update

# キャッシュをクリア
cargo clean
```

#### 2. Node.jsモジュールエラー
```bash
# node_modulesを削除して再インストール
rm -rf node_modules package-lock.json
npm install
```

#### 3. ポート競合エラー
デフォルトポート1420が使用中の場合：
```bash
# 別のポートを指定
npm run dev -- --port 3000
```

#### 4. WebView2エラー (Windows)
Microsoft EdgeのWebView2ランタイムをインストール：
https://developer.microsoft.com/en-us/microsoft-edge/webview2/

## 参考リンク

### 公式ドキュメント
- **Tauri公式ドキュメント**: https://tauri.app/
- **Tauri APIリファレンス**: https://tauri.app/v1/api/js/
- **Svelte公式ドキュメント**: https://svelte.dev/
- **TypeScript公式ドキュメント**: https://www.typescriptlang.org/
- **Vite公式ドキュメント**: https://vitejs.dev/

### セットアップガイド
- **Tauri前提条件**: https://tauri.app/v1/guides/getting-started/prerequisites
- **Rust公式インストールガイド**: https://www.rust-lang.org/tools/install
- **Node.js公式サイト**: https://nodejs.org/

### 開発リソース
- **Tauri Examples**: https://github.com/tauri-apps/tauri/tree/dev/examples
- **Svelte Examples**: https://svelte.dev/examples
- **Tauri Plugin集**: https://github.com/tauri-apps/plugins-workspace

## 追加設定

### VS Code拡張機能（推奨）
- **rust-analyzer**: Rust言語サポート
- **Svelte for VS Code**: Svelte言語サポート
- **Tauri**: Tauri開発サポート
- **TypeScript Importer**: TypeScript自動インポート

### デバッグ設定
`.vscode/launch.json`を作成してデバッグ環境を設定可能：
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "lldb",
      "request": "launch",
      "name": "Tauri Development Debug",
      "cargo": {
        "args": [
          "build",
          "--manifest-path=./src-tauri/Cargo.toml",
          "--no-default-features"
        ]
      },
      "args": [],
      "cwd": "${workspaceFolder}"
    }
  ]
}
```

## 本番ビルド

### デスクトップアプリのビルド
```bash
npm run tauri:build
```

ビルド成果物は以下に出力されます：
- **Windows**: `src-tauri/target/release/bundle/msi/`
- **macOS**: `src-tauri/target/release/bundle/dmg/`
- **Linux**: `src-tauri/target/release/bundle/deb/` または `src-tauri/target/release/bundle/appimage/`

### 配布用パッケージング
アプリケーション署名や配布については、Tauriの公式ガイドを参照：
https://tauri.app/v1/guides/distribution/

---

## サポート

- **GitHub Issues**: プロジェクトの問題報告
- **Tauri Discord**: https://discord.com/invite/SpmNs4S
- **Rust Community**: https://www.rust-lang.org/community