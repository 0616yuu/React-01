# 🔁 Reactの `.map()` 演習まとめ（ステップ1〜ステップ4）

---

## ✅ 1. `.map()` の基本構文（昨日のステップ）

```js
const fruits = ["りんご", "バナナ", "みかん"];

return (
  <ul>
    {fruits.map((fruit, index) => (
      <li key={index}>{fruit}</li>
    ))}
  </ul>
);
```

### ✔ ポイント
- `.map()` は配列の要素を1個ずつ取り出して、React要素を返す
- `key` を忘れると警告（Reactがどの要素が変わったか追えなくなる）
- `index` を使えば、とりあえず一意な値になる

---

## ✅ 2. メモアプリに `.map()` を使ったリスト表示（今日）

### 📦 元の状態
```js
const [memos, setMemos] = useState([]);
```

### 🧩 `.map()` を使ってリスト表示
```jsx
<ul>
  {memos.map((memo, index) => (
    <li key={index}>{memo}</li>
  ))}
</ul>
```

---

## ✅ 3. 削除ボタンつき `.map()` 応用

```jsx
<ul>
  {memos.map((memo, index) => (
    <li key={index}>
      {memo}
      <button onClick={() => handleDelete(index)}>削除</button>
    </li>
  ))}
</ul>
```

### ✔ ポイント
- `.map()` の中で `button` を配置 → 各行に「削除ボタン」がつく
- `onClick={() => handleDelete(index)}` でその行の index を渡せる
- `handleDelete` 関数は `.filter()` を使って対象以外を残す

```js
const handleDelete = (indexToRemove) => {
  setMemos(memos.filter((_, index) => index !== indexToRemove));
};
```

---

## ✅ 4. `.map()` の中をコンポーネント化（props練習）

### 🧩 `MemoItem.jsx`
```jsx
function MemoItem({ memo, onDelete, index }) {
  return (
    <li>
      {memo}
      <button onClick={() => onDelete(index)}>削除</button>
    </li>
  );
}
export default MemoItem;
```

### 📦 `MemoList.jsx`
```jsx
import MemoItem from "./MemoItem";

function MemoList({ memos, onDelete }) {
  return (
    <ul>
      {memos.map((memo, index) => (
        <MemoItem
          key={index}
          memo={memo}
          index={index}
          onDelete={onDelete}
        />
      ))}
    </ul>
  );
}
export default MemoList;
```

### ✔ ポイント
- `.map()` の中身を1つのコンポーネントに切り出して管理しやすく
- `memo`, `index`, `onDelete` を props として渡す

---

## 🎯 まとめ

| レベル | 内容                         | 学んだこと                             |
|--------|------------------------------|----------------------------------------|
| 基本   | `.map()` で配列 → JSX表示   | `key` の意味、`index` の使い方        |
| 応用① | 削除ボタンをつける           | `onClick` に関数＋引数渡し             |
| 応用② | `.map()` の中身を分割        | propsで受け取り、コンポーネントを使う |

---

✅ `.map()` を使って「複数のUI部品を並べる力」を手に入れた！
次は `.filter()` や `.map()` の組み合わせや、チェック付きリストなどに応用予定！
