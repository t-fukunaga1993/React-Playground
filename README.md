# React + TypeScript + Vite

このテンプレートは、ViteでReactを動作させるための最小限のセットアップを提供し、HMRといくつかのESLintルールを含んでいます。

現在、2つの公式プラグインが利用可能です：

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) は [Babel](https://babeljs.io/) を使用してFast Refreshを実現します
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) は [SWC](https://swc.rs/) を使用してFast Refreshを実現します

## 環境構築
[React と TypeScript で簡単 TODO アプリ](https://zenn.dev/sprout2000/articles/40328708afaeb9)を学習するための環境構築を行っています。

### Voltaのインストール (Windows)

Voltaを利用してNode.jsとnpmのバージョンを管理します。

1. [Voltaの公式サイト](https://volta.sh/)にアクセスし、インストールスクリプトをダウンロードします。
2. ダウンロードしたインストールスクリプトを実行します。コマンドプロンプトまたはPowerShellを管理者権限で開き、以下のコマンドを実行します：
   ```sh
   powershell -Command "iwr https://get.volta.sh | Install-Volta"
   ```
3. インストールが完了したら、コマンドプロンプトまたはPowerShellを再起動します。

### Nodeとnpmのインストール (Voltaを使用)

1. Voltaを使用してNode.jsをインストールします。以下のコマンドを実行します：
   ```sh
   volta install node@18.20.4
   ```
2. 次に、npmをインストールします。以下のコマンドを実行します：
   ```sh
   volta install npm@10.7.0
   ```

### プロジェクトのセットアップ

1. プロジェクトのルートディレクトリに移動します。
2. 必要な依存関係をインストールします。以下のコマンドを実行します：
   ```sh
   npm install
   ```

### アプリケーションの実行方法

1. 開発サーバーを起動します。以下のコマンドを実行します：
   ```sh
   npm run dev
   ```
2. ブラウザで `http://localhost:5173/` にアクセスし、アプリケーションが正しく動作していることを確認します。

3. アプリケーションをビルドするには、以下のコマンドを実行します：
   ```sh
   npm run build
   ```

4. ビルドされたアプリケーションをプレビューするには、以下のコマンドを実行します：
   ```sh
   npm run preview
   ```

## ESLint設定の拡張

本番アプリケーションを開発している場合、型を認識するlintルールを有効にするために設定を更新することをお勧めします：

- トップレベルの `parserOptions` プロパティを次のように設定します：
```js
export default tseslint.config({
  languageOptions: {
    // other options...
    parserOptions: {
      project: ['./tsconfig.node.json', './tsconfig.app.json'],
      tsconfigRootDir: import.meta.dirname,
    },
  },
})
```

- `tseslint.configs.recommended` を `tseslint.configs.recommendedTypeChecked` または `tseslint.configs.strictTypeChecked` に置き換えます
- オプションで `...tseslint.configs.stylisticTypeChecked` を追加します
- [eslint-plugin-react](https://github.com/jsx-eslint/eslint-plugin-react) をインストールし、設定を更新します：

```js
// eslint.config.js
import react from 'eslint-plugin-react'

export default tseslint.config({
  // Set the react version
  settings: { react: { version: '18.3' } },
  plugins: {
    // Add the react plugin
    react,
  },
  rules: {
    // other rules...
    // Enable its recommended rules
    ...react.configs.recommended.rules,
    ...react.configs['jsx-runtime'].rules,
  },
})
```