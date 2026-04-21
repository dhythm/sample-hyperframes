# sample-hyperframes

[HyperFrames](https://github.com/heygen-com/hyperframes) を使ったサンプルリポジトリです。HTML と GSAP だけで動画コンポジションを記述し、MP4 にレンダリングする仕組みを体験できます。

## HyperFrames とは

HyperFrames は、HTML/CSS/JavaScript（GSAP）で書かれたコンポジションを動画として書き出せるフレームワークです。`data-*` 属性でタイミングを宣言し、ブラウザでプレビューしながら制作できます。

- 公式リポジトリ: <https://github.com/heygen-com/hyperframes>
- ドキュメント: <https://hyperframes.heygen.com/introduction>
- LLM 向けインデックス: <https://hyperframes.heygen.com/llms.txt>

## 必要要件

- Node.js 18 以上
- npm（または pnpm / yarn）

## セットアップ

```bash
git clone <this-repo-url>
cd sample-hyperframes
```

依存関係のインストールは不要で、`npx` から CLI を直接実行できます。

## よく使うコマンド

```bash
npx hyperframes preview          # ブラウザでプレビュー（スタジオエディタ）
npx hyperframes render           # MP4 にレンダリング
npx hyperframes lint             # コンポジションを検証（errors + warnings）
npx hyperframes lint --verbose   # info レベルの結果も表示
npx hyperframes lint --json      # CI 向けの機械可読出力
npx hyperframes docs <topic>     # ターミナルからリファレンス参照
```

`docs` で参照可能なトピック: `data-attributes`, `gsap`, `compositions`, `rendering`, `examples`, `troubleshooting`

## プロジェクト構造

```
.
├── index.html          # ルートタイムライン（メインコンポジション）
├── hyperframes.json    # レジストリ / パス設定
├── meta.json           # プロジェクトメタデータ（id, name）
├── compositions/       # サブコンポジション（data-composition-src で参照）
└── assets/             # メディアファイル（動画, 音声, 画像）
```

## コンポジションの基本ルール

1. タイミングを持つ要素には `data-start`, `data-duration`, `data-track-index` を必ず付与する
2. 可視要素には `class="clip"` を付与する（フレームワークが表示制御に使用）
3. GSAP タイムラインは `paused: true` で作成し、`window.__timelines` に登録する

   ```js
   window.__timelines = window.__timelines || {};
   window.__timelines["composition-id"] = gsap.timeline({ paused: true });
   ```

4. 動画は `muted` にし、音声は別の `<audio>` 要素として扱う
5. サブコンポジションは `data-composition-src="compositions/file.html"` で参照する
6. 非決定的な処理（`Date.now()`, `Math.random()`, ネットワーク取得）は使用しない

## 編集後は必ず lint

HTML コンポジションを編集したら、完了前に必ずリンタを実行します。

```bash
npx hyperframes lint
```

エラーは修正してください。warnings は情報提供で、通常は無視して問題ありません。

## AI エージェント向け

本リポジトリには Claude Code 等の AI エージェント向けガイド（[CLAUDE.md](CLAUDE.md) / [AGENTS.md](AGENTS.md)）を同梱しています。エージェントで作業する場合は、フレームワーク固有のパターン（`window.__timelines` 登録や `data-*` 属性の意味など）を記述した公式 Skill の利用を推奨します。

```bash
npx skills add heygen-com/hyperframes
```

## ライセンス

本サンプルの取り扱いは、利用者の判断に委ねます。HyperFrames 本体のライセンスは[公式リポジトリ](https://github.com/heygen-com/hyperframes)を参照してください。
