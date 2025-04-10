# 🧠 React関数のよく使うテンプレート集

> イベントの中で「何するか」は自分で考える必要があるけど、
> Reactではよくある "定番の書き方" が存在する！

---

## ✅ 1. 追加処理（配列の末尾に追加）

```js
const handleAdd = () => {
  if (input.trim() === "") return;
  setList([...list, { text: input, done: false }]);
  setInput("");
};
```

| ポイント | 説明 |
|----------|------|
| `...list` | 今の配列をコピー（展開）
| `input`   | 入力欄から取ったテキスト
| `done: false` | チェック機能付き用（初期状態）

---

## ✅ 2. 削除処理（クリックした要素だけ除外）

```js
const handleDelete = (indexToRemove) => {
  setList(list.filter((_, index) => index !== indexToRemove));
};
```

| パーツ      | 意味                       |
|-------------|----------------------------|
| `filter()`   | 条件を満たすものだけ残す   |
| `_`         | 使わない引数（中身）       |
| `index !== indexToRemove` | 押されたやつ以外を残す！ |

---

## ✅ 3. チェック切り替え（true ↔ false）

```js
const handleToggle = (indexToToggle) => {
  const newList = [...list];
  newList[indexToToggle].done = !newList[indexToToggle].done;
  setList(newList);
};
```

| 処理内容 | 説明 |
|----------|------|
| `...list` | コピー（直接編集NG）
| `.done = !done` | true ⇄ false を切り替える
| `setList()` | 状態更新

---

## ✅ 4. 編集処理（中身を書き換える）

```js
const handleEdit = (indexToEdit, newText) => {
  const updatedList = list.map((item, index) =>
    index === indexToEdit ? { ...item, text: newText } : item
  );
  setList(updatedList);
};
```

| 処理内容 | 説明 |
|----------|------|
| `map()`  | 全部見る → 条件で書き換え |
| `...item` | 他の情報を保持（textだけ変更） |

---

## ✅ 5. 全クリア

```js
const handleClear = () => {
  setList([]);
};
```

---

## ✅ よく使う関数パターンまとめ

| 処理        | メソッド       | 一言まとめ                      |
|-------------|----------------|---------------------------------|
| 追加        | `...list, 新`  | スプレッド構文で追加           |
| 削除        | `.filter()`    | 条件に合わないやつだけ残す     |
| チェック切替| `!値`          | true/false を反転               |
| 編集        | `.map()`       | 条件に合うやつだけ書き換える   |
| 全削除      | `[]`           | 配列を空にするだけ              |

---

Reactは「中身の関数は自分で考える」けど、
**このテンプレ集をベースにすればだいたい何でも作れる！**

必要に応じてカスタムして使おう💪
