# React - props のまとめノート
📅 日付：2025/04/11

---

## ✅ propsとは？

**props（プロップス）とは「親コンポーネントから子コンポーネントへ渡す情報」**のこと。

> HTMLでいう「タグの属性」みたいなもので、Reactでは親から子へ「値」や「関数」を渡すために使う。

---

## ✅ propsの役割まとめ

| 役割 | 説明 |
|------|------|
| 📦 データの受け渡し | 親 → 子 に値を渡すために使う |
| 🔁 イベントの伝達 | 子から親へイベントを伝える（関数を props として渡す） |
| 🧩 UI部品の再利用 | 子コンポーネントをパラメータ化して再利用できる |

---

## ✅ 基本の書き方

### ① 親 → 子 に値を渡す

```jsx
function App() {
  return <Welcome name="ゆうくん" />;
}

function Welcome({ name }) {
  return <h1>こんにちは、{name}さん！</h1>;
}
```

---

### ② 親 → 子 に関数を渡す（イベント伝達）

```jsx
function App() {
  const handleClick = () => {
    alert("クリックされた！");
  };

  return <ChildButton onClick={handleClick} />;
}

function ChildButton({ onClick }) {
  return <button onClick={onClick}>押してね</button>;
}
```

---

### ③ props drilling（孫コンポーネントまで渡す）

```jsx
<App>
  <Parent>
    <Child onClick={handleClick} />
  </Parent>
</App>
```

→ `props` を「中継」して孫まで渡すことを props drilling という。

---

## ✅ props の受け取り方（NGとOK）

### ❌ NG：オブジェクトで全部受け取ってしまう

```js
function Comp(props) {
  return <p>{props.text}</p>;
}
```

### ✅ OK：分割代入して必要なものだけ取り出す

```js
function Comp({ text }) {
  return <p>{text}</p>;
}
```

---

## ✅ よくあるpropsエラー防止ポイント

| 書き方 | 内容 |
|--------|------|
| `onClick={handleClick}` | ✅ 関数そのものを渡す |
| `onClick={handleClick()}` | ❌ すぐ実行されてしまう |
| `function Comp({ text })` | ✅ 分割代入が基本 |
| `function Comp(props)` → `props.text` | ❌ 直接書くより分割代入が読みやすい |

---

これで props の基礎はバッチリ！  
親 → 子 → 孫 の流れや、関数を渡す構造がわかっていれば React の基礎は完成や💪
