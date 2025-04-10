# 🔥 Reactでよく使うイベント関数（イベントハンドラ）まとめ

Reactでは、ユーザーの操作（クリック、入力、送信など）に反応して処理を実行する「**イベント関数**」が超重要！
ここではよく使うものをまとめたぞ！

---

## ✅ 1. `onChange`：入力内容が変わったとき

```jsx
<input
  type="text"
  value={text}
  onChange={(e) => setText(e.target.value)}
/>
```

- 入力された文字を `text` という state に保存
- `e.target.value` で入力欄の値を取得！

---

## ✅ 2. `onClick`：クリックされたとき

```jsx
<button onClick={handleAdd}>追加</button>
```

```js
const handleAdd = () => {
  // クリック時の処理を書く
};
```

- ボタンなどがクリックされた瞬間に実行される！

---

## ✅ 3. `onSubmit`：フォームが送信されたとき

```jsx
<form onSubmit={handleSubmit}>
  <input ... />
  <button type="submit">送信</button>
</form>
```

```js
const handleSubmit = (e) => {
  e.preventDefault(); // ページリロードを防ぐ
  // 送信処理を書く
};
```

- `<form>`タグの送信をキャッチ！
- `e.preventDefault()` がポイント！

---

## ✅ 4. `onKeyDown`：キーボードが押されたとき

```jsx
<input onKeyDown={(e) => {
  if (e.key === 'Enter') {
    console.log("Enter押された！")
  }
}} />
```

- キーボードの入力を拾える！
- `e.key === 'Enter'` などで判定可能！

---

## ✅ 5. `onChange`（チェックボックス）

```jsx
<input
  type="checkbox"
  checked={isChecked}
  onChange={(e) => setIsChecked(e.target.checked)}
/>
```

- `e.target.checked` で「ONかOFFか」がわかる！

---

## ✅ まとめ表

| イベント関数  | トリガー（きっかけ）           | よく使う場面                     |
|----------------|----------------------------|------------------------------|
| `onChange`     | 入力欄が変化したとき         | 入力フォーム・チェックボックス |
| `onClick`      | ボタンなどがクリックされたとき | 追加・削除・送信ボタン         |
| `onSubmit`     | フォームが送信されたとき       | 検索、ログインなど             |
| `onKeyDown`    | キーが押されたとき             | Enterキー処理など             |

---

📌 **Reactは"状態（state）とイベント関数の連携"が超大事！**
これをマスターすればどんなUIも自由自在💪
