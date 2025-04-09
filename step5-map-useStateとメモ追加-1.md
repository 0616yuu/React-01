# step3-map：useStateとメモ追加（前半）

## ✅ 今回の目標
- 入力欄に文字を入力できるようにする
- 「追加」ボタンを押すと、配列にメモを追加する
- 入力欄は空になる
- 今の配列の中身を画面に表示して確認

---

## ① useState で状態を2つ管理
```js
const [input, setInput] = useState("");      // 今の入力文字を保存する箱
const [memos, setMemos] = useState([]);       // メモの一覧を保存する配列
```

---

## ② 入力欄に文字を打てるようにする
```jsx
<input
  type="text"
  value={input}
  onChange={(e) => setInput(e.target.value)}
  placeholder="メモを入力"
/>
```
- 入力するたびに `setInput()` が呼ばれて、状態が更新される
- `value={input}` で、Reactの状態と入力欄がリンク

---

## ③ 「追加」ボタンでメモを配列に追加する
```js
const handleAdd = () => {
  if (input.trim() === "") return; // 空欄や空白だけの入力を無視
  setMemos([...memos, input]);     // 今ある配列に新しいメモを追加
  setInput("");                    // 入力欄をリセット（空文字に）
};
```

- `input.trim()` は空白だけの入力を防ぐおまじない
- `[...memos, input]` で、配列の末尾に新しいメモを追加

---

## ④ memos 配列の中身を画面に出してみる
```jsx
<pre>{JSON.stringify(memos, null, 2)}</pre>
```
- JSON.stringify() は「配列やオブジェクトを文字列にして表示する」関数
- `<pre>` で整形表示（インデントあり）

---

## ⑤ 今のメモ数を数えてみる
```jsx
<p>現在のメモ数：{memos.length}</p>
```
- `.length` は「要素の数」
- 配列に何個入ってるかを表示（※文字数ではない！）

---

## ✅ 次にやること
- `.map()` を使って配列の中身を画面にリストで表示する
- 削除ボタンをつける

---

ゆうくん、ここまでOKなら `.map()` 編いくぞ！

