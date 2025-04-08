# React学習ノート（STEP 1）

## 1. 学習期間
2025年4月8日（火）

## 2. 学習内容の概要
- JSXの基本的な構文
- 関数コンポーネントの作成方法
- propsを用いたデータの受け渡し

## 3. 学習の目的
フロントエンド開発業務において、Reactを使用したUI構築の基礎を理解し、今後の実務に対応できるようにするため。

## 4. 学習内容の詳細

### 4.1 JSXとは
- JavaScriptでHTMLのようなUI構文を記述できる記法。
- 見た目はHTMLに近いが、実際はJavaScriptの構文の中に記述する。
- `class`ではなく`className`、`for`ではなく`htmlFor`を使う必要がある。
```jsx
const element = <h1>Hello, world!</h1>;
