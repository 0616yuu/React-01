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
- 注意点：`class`ではなく`className`、`for`ではなく`htmlFor`を使用する。

```jsx
const element = <h1>Hello, world!</h1>;
```

### 4.2 関数コンポーネントとは
- ReactでUIを部品化するための基本的な方法。
- JavaScriptの関数として定義し、JSXを返す。

```jsx
function Hello() {
  return <h1>こんにちは！</h1>;
}
```

### 4.3 propsの使用
- 親コンポーネントから子コンポーネントへデータを渡す仕組み。
- `props`はオブジェクトであり、各プロパティにアクセスして値を表示する。

```jsx
function Hello(props) {
  return <h1>こんにちは、{props.name}さん！</h1>;
}

function App() {
  return <Hello name="タカシ" />;
}
```

### 4.4 JSXとJavaScriptの組み合わせ
- JSX内でJavaScriptの変数や式を使うには`{}`で囲む。

```jsx
const name = "アユミ";
return <p>{name}、今日はReactを学びます</p>;
```

### 4.5 ルートコンポーネントの構造
- すべてのReactアプリは1つのルートコンポーネント（通常は`App`）から始まる。
- JSXは1つの親要素で囲む必要がある。

```jsx
function App() {
  return (
    <div>
      <Hello name="カズオ" />
      <Hello name="ユミコ" />
    </div>
  );
}
```

## 5. 振り返り・気づき
- JSXはHTMLに似ているが、細かい構文の違いに注意が必要。
- propsはコンポーネント間のデータ受け渡しにおいて基本となる概念。
- コンポーネントを関数で定義することで、再利用性の高いUI部品を作ることができる。
- データの流れは「親 → 子」の一方通行で設計されており、構造を明確に保てる。

## 6. 次の学習目標
- `useState`を使った状態管理の基礎
- JSXとstateの連動
- イベントハンドリング（クリック、入力など）との組み合わせ

