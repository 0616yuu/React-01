# 🧹 Props Drilling の理解メモ  
🗕 2025年4月14日  

---

## 🌟 目的

React における「親→子→孫」へのデータ伝達（**props drilling**）を体験し、データの受け渡しが複雑になった際の課題を実感する。その後の **Context API** の必要性を理解するための土台を作る。

---

## 🔁 実装構成

```
App.jsx
 └── Parent.jsx
       └── Child.jsx
```

- App：状態（state）を管理する親コンポーネント
- Parent：propsで受け取った値をさらにChildへ渡す
- Child：最終的に受け取ったデータを表示するだけ

---

## 💻 コード例

### `App.jsx`

```jsx
import Parent from "./Parent";
import { useState } from "react";

function App() {
  const [message, setMessage] = useState("ようこそ、Reactの世界へ");

  return (
    <>
      <h1>Appコンポーネント</h1>
      <Parent message={message} />
    </>
  );
}

export default App;
```

---

### `Parent.jsx`

```jsx
import Child from "./Child";

function Parent({ message }) {
  return (
    <div style={{ border: "1px solid gray", padding: "10px" }}>
      <h2>Parentコンポーネント</h2>
      <Child message={message} />
    </div>
  );
}

export default Parent;
```

---

### `Child.jsx`

```jsx
function Child({ message }) {
  return (
    <div style={{ border: "1px dashed gray", padding: "10px" }}>
      <h3>Childコンポーネント</h3>
      <p>受け取ったメッセージ：{message}</p>
    </div>
  );
}

export default Child;
```

---

## 📉 Props Drilling の課題点

- 子→孫→その先...と**どんどん props を渡す必要**が出てくる
- 本当に使いたいのは末端のコンポーネントだけなのに、**中間のコンポーネントでも受け取って渡す処理が必要**
- **状態管理が複雑になる**
- **再利用性が低下**になる

---

## 🌀 Context API の必要性

Context API を使えば...

- ✅ グローバルな state を作れる　（複数コンポーネントで共有可）
- ✅ 中間コンポーネントを介さずに、**必要な子コンポーネントだけ**で値を使える
- ✅ props drilling を回避できる

️ → 「小さなアプリ」なら気にならないが、「中→大規模アプリ」では必須の考え方！

