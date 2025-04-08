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

# React学習ノート（STEP 2） useStateの基本理解

## 学習内容
- ReactのuseStateフックを使った状態管理の仕組みを学習
- JSXでstateを表示し、ボタン操作でstateを変更する挙動を実装

---

## useStateとは？
Reactの関数コンポーネント内で「状態（変化するデータ）」を持つためのフック。  
書き方：

```js
const [state, setState] = useState(初期値);」

#実際のコード
import { useState } from 'react';

function App() {
  const [count, setCount] = useState(0);

  return (
    <div style={{ textAlign: 'center', marginTop: '50px' }}>
      <h1>カウント：{count}</h1>
      <button onClick={() => setCount(count + 1)}>増やす</button>
      <button onClick={() => setCount(count - 1)}>減らす</button>
      <button onClick={() => setCount(0)}>リセット</button>
    </div>
  );
}

#各構文の意味
・useState(0)：初期値０で状態作成
・const：現在の状態（表示される値）
・setCount：状態を更新する関数
・{count}：JSX内で現在の状態を表示
・onClick={・・・}：イベント発火でstateを変更

#回答まとめ（自分で答えた内容）
	1.	useStateの役割 → 数字などの変化する状態を管理するため
	2.	setCountの役割 → 状態（count）を更新する
	3.	{count}の意味 → JSX内で状態を画面に表示している
	4.	setCount(count - 1)の結果 → 現在の数字が1減る
