# npm-work

このリポジトリは、npm workspace + TypeScript + ESM構成で、パッケージ間の依存・型安全な呼び出しを実現するサンプルです。

## ディレクトリ構成

```
.
├── package.json           # ルート: npm workspace定義
├── tsconfig.base.json     # ルート: TypeScript共通設定
├── packages/
│   ├── package-a/         # 提供パッケージ
│   │   ├── src/index.ts   # helloA関数をexport
│   │   └── ...
│   └── package-b/         # 利用パッケージ
│       ├── src/index.ts   # package-aのhelloAをimportして利用
│       └── ...
```

## セットアップ手順

1. 依存パッケージのインストール

```sh
npm install
```

2. 各パッケージのビルド

```sh
# package-aを先にビルド
cd packages/package-a && npm run build

# package-bをビルド
cd ../package-b && npm run build
```

3. package-bの実行

```sh
npm start
```

## サンプルコード

### package-a/src/index.ts
```ts
/**
 * package-aのサンプル関数
 * @returns {string}
 */
export function helloA(): string {
  return "Hello from package-a!";
}
```

### package-b/src/index.ts
```ts
import { helloA } from "package-a";

console.log(helloA());
```

## サンプル出力

```
Hello from package-a!
```

## 技術ポイント
- npm workspaceによるパッケージ間依存管理
- TypeScript + ESM構成
- プロジェクト参照（references）による型安全な依存
- tsconfigのpaths/moduleResolution設定によるパス解決

## 注意事項
- package-aを先にビルドしてください（型定義・依存解決のため）
- ESM構成のため、Node.js v16以降推奨
- npm がv7以降であること
