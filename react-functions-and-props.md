# React - 関数と props の使い方まとめ
📅 日付：2025/04/11

---

## ✅ 1. 関数の書き方と使い方の違い

| 書き方                          | 意味・使い方                                       |
|-------------------------------|--------------------------------------------------|
| `function aaa() { }`        | 通常の関数定義                                   |
| `const aaa = () => { }`     | アロー関数（複数行の処理）                        |
| `const aaa = () => 式`        | アロー関数（1行なら return を省略可能）            |
| `aaa()`                       | 関数を「実行」する                               |
| `aaa`                         | 関数そのものを「渡す・登録する」場合に使う         |

---

## ✅ 2. Reactイベントと関数の扱い方

### ✅ 基本パターン

```jsx
<button onClick={handleClick}>OK</button>    // ✅ 正しい（関数を渡す）
<button onClick={handleClick()}>NG！</button> // ❌ 関数の結果が渡ってしまう（即実行）
```

---

### ✅ 引数を渡したい時はアロー関数でラップ

```jsx
<button onClick={() => handleClick("ゆうくん")}>✅ これが正解！</button>
```

---

## ✅ 3. propsの受け取り方：何が違う？

### ❌ これはNGな例：

```js
function ChildButton(onClick) {
  // 実は onClick には props オブジェクト全体が入る
  console.log(onClick); // → { onClick: function }
}
```

> 呼ぶ時に `onClick.onClick()` みたいになってしまって超ややこしい！

---

### ✅ 正しい受け取り方（分割代入）

```js
function ChildButton({ onClick }) {
  return <button onClick={onClick}>押してね</button>;
}
```

> propsの中身から `onClick` だけをスッキリ抜き出して使える！

---

## ✅ 4. propsの基本まとめ

| 書き方                         | 説明 |
|------------------------------|------|
| `function Comp(props)`       | 全部 props オブジェクトで受け取る |
| `function Comp({ title })` | title だけ抜き出す（分割代入） |
| `function Comp({ onClick, text })` | 複数の値を一気に受け取る時に使う（定番） |

---

これを理解すれば、propsと関数周りでエラー出ることがグッと減るぞ🔥
