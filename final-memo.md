    # ✅ Reactメモアプリまとめ（チェック・削除・編集機能付き）

---

## 🗓️ 作成日

2025 年 4 月 14 日

## 🧠 概要

- React を使って「チェック・削除・編集」機能付きのメモアプリを実装。
- useState、map、filter などの基本構文や、イベント処理・親子コンポーネントの props 渡しを練習。
- UI はシンプルなリスト形式で、ToDo アプリのような操作ができる。

---

## 📁 実装ファイル一覧

```
/src
├── App.jsx
├── components/
│   ├── MemoList.jsx
│   └── MemoItem.jsx
```

---

## 💡 各機能の説明

### 1. メモの追加

```js
const [input, setInput] = useState("");
const [memos, setMemos] = useState([]);

const handleAdd = () => {
  if (input.trim() === "") return;
  setMemos([...memos, { text: input, isDone: false, isEditing: false }]);
  setInput("");
};
```

- `input`: テキストボックスの入力内容
- `memos`: メモ一覧（配列）
- `setMemos([...memos, 新しいメモ])`: 既存メモに追加
- `.trim()` で空白だけのメモを除外

---

### 2. メモの削除

```js
const handleDelete = (indexToRemove) => {
  setMemos(memos.filter((_, index) => index !== indexToRemove));
};
```

- `.filter()` で削除対象以外の要素だけ残す
- `_` は使わない引数（今回はメモ本体）

---

### 3. チェック（完了状態の切り替え）

```js
const handleToggle = (indexToToggle) => {
  const newMemos = [...memos];
  newMemos[indexToToggle].isDone = !newMemos[indexToToggle].isDone;
  setMemos(newMemos);
};
```

- チェック状態を true/false 切り替え
- `textDecoration: 'line-through'` で見た目に反映

---

### 4. 編集モードの切り替えと保存・キャンセル

```js
const handleEdit = (index) => {
  const newMemos = [...memos];
  newMemos[index].isEditing = true;
  setMemos(newMemos);
};

const handleUpdate = (index, newText) => {
  const newMemos = [...memos];
  newMemos[index].text = newText;
  newMemos[index].isEditing = false;
  setMemos(newMemos);
};

const handleCancelEdit = (index) => {
  const newMemos = [...memos];
  newMemos[index].isEditing = false;
  setMemos(newMemos);
};
```

- 編集ボタンで `isEditing` を true に
- Enter で `handleUpdate()`、Escape で `handleCancelEdit()` を呼ぶ

---

## 🔗 コンポーネントの分割と流れ

### App.jsx

- 状態管理（input, memos）を行う
- 子コンポーネント（MemoList）に props を渡す

### MemoList.jsx

- `.map()` を使って MemoItem を並べる
- 子コンポーネントに 1 件分のメモ情報と操作関数を渡す

### MemoItem.jsx

- 1 件分のメモの表示・編集・チェック・削除
- `isEditing` によって表示を `<span>` と `<input>` に切り替える

---

## 📘 学びポイント・注意点

- `useState` で「状態の保存と更新」ができる
- `map` の中には必ず `key` をつける（index 可、できればユニーク ID）
- `filter` を使えば配列から条件付きで削除できる
- `props` を使って親 → 子、イベント関数で子 → 親のやりとりが可能
- `Reactは状態に応じてUIが再描画される`のが基本ルール
- `条件分岐 (三項演算子)` を使えば表示の切り替えができる
- 編集時には `編集モード用state（isEditing）` を持たせておく

---

## ✅ 最終状態でできること

- メモの追加
- チェック（完了）状態の切り替え
- メモの削除
- メモの編集とキャンセル

---

次は Step2：props に進んで「親 → 子」「子 → 親」のやり取りに強くなっていこう！
