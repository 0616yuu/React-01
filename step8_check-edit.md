# ✅ チェック・編集機能付きメモアプリまとめ（2025/04/11）

---

## 1. タイトル＋日付

**チェック機能 & 編集機能付き メモアプリ（STEP2）**  
📅 作成日：2025年4月11日（金）

---

## 2. 概要（どんな機能まで作ったか）

ReactのuseStateとmapをベースに、以下の機能を備えたメモアプリを作成：

- メモの追加
- メモの削除
- チェック機能（完了状態の切り替え）
- 編集モードへの切り替え
- 編集内容の保存 / キャンセル
- チェック済みは取り消し線表示
- ファイル分割による機能の整理

---

## 3. 実装したReactファイルの一覧

| ファイル名         | 役割                          |
|-------------------|-------------------------------|
| App.jsx           | 画面にMemo_step02を表示するメインコンポーネント |
| Memo_step02.jsx   | メモ機能の本体（状態管理＋関数群） |
| MemoList.jsx      | メモリストを`<ul>`で表示する中間コンポーネント |
| MemoItem.jsx      | 1件ずつのメモを表示・操作する最小単位 |

---

## 4. 各機能の説明

### 🔧 useState
```js
const [input, setInput] = useState("");
const [memos, setMemos] = useState([]);
```
- `input`：入力欄の文字
- `memos`：メモ一覧（配列）

### ➕ メモ追加（handleAdd）
```js
setMemos([...memos, { text: input, isDone: false, isEditing: false }]);
```
- 入力された文字を `text` としてオブジェクトに保存

### ❌ 削除（handleDelete）
```js
setMemos(memos.filter((_, index) => index !== indexToRemove));
```
- 該当のindexだけ除外して、再構築された配列を保存

### ✅ チェック切替（handleToggle）
```js
newMemos[index].isDone = !newMemos[index].isDone;
```
- チェックをトグル（true/false 切替）

### ✏ 編集モードON（handleEdit）
```js
newMemos[index].isEditing = true;
```

### 💾 編集確定（handleUpdate）
```js
newMemos[index].text = newText;
newMemos[index].isEditing = false;
```

### 🚫 編集キャンセル（handleCancelEdit）
```js
newMemos[index].isEditing = false;
```

---

## 5. コンポーネント分割の流れ

```
Memo_step02.jsx
├─ MemoList.jsx（<ul>の中身）
│   └─ MemoItem.jsx（1件分の<li>）
```

- 分割によって役割が明確になり、コードの見通しが良くなる
- propsを通して関数や状態を子コンポーネントに渡す練習にもなった

---

## 6. 学びポイント・注意点

- `props` の渡し忘れ → `onEdit` や `onCancel` などを忘れると `undefined` になる
- `memo` はオブジェクトなので直接表示できない → `memo.text` として表示する必要あり
- `index` を子に渡すのを忘れると何も動かなくなる
- `useState(memo.text)` の初期値ミス → `[]` や `{}` を入れたら爆発する
- 編集のときは `editText` で一時的に管理してから保存する流れが重要
- JSXの条件分岐は `(条件 ? A : B)` で切り替えを明確に

---

✔ これでチェック＆編集付きのメモアプリは完成！！
次のステップは `localStorage` で保存する応用とか、UIの強化🔥

