# STEP4: useReducer 構成理解メモ（2025/04/14）

## 🎯 目的

useReducer を使った状態管理とコンポーネント分割による効率的なアプリ構築を理解する。

---

## 📁 フォルダ / ファイル構成

```
src/
├─ App.jsx              ← 親コンポーネント：状態管理とdispatch
├─ components/
│   ├─ MemoList.jsx     ← 子：一覧表示用
│   └─ MemoItem.jsx     ← 孫：1件表示と操作（削除・チェックなど）
```

---

## 🔧 各ファイルの役割

### App.jsx

- `useReducer()` で状態管理（memos）と更新命令（dispatch）を実装
- reducer 関数内で "ADD", "DELETE", "TOGGLE" などのロジックを処理
- `<MemoList memos={memos} dispatch={dispatch} />` によって props 渡し

### MemoList.jsx

- `memos.map()` を使ってリスト表示
- 各要素に `<MemoItem memo={memo} index={index} dispatch={dispatch} />` を渡す

### MemoItem.jsx

- 1 つのメモに関する表示や操作（削除・チェック）を担当
- チェックボックス・削除ボタンに `dispatch()` を使って命令を送る

```jsx
<input type="checkbox" onChange={() => dispatch({ type: "TOGGLE", index })} />
<button onClick={() => dispatch({ type: "DELETE", index })}>削除</button>
```

---

## 🔁 データの流れ（props の階層伝達）

```
App.jsx
  └─ MemoList.jsx
        └─ MemoItem.jsx
```

- 状態と関数を親 → 子 → 孫へと段階的に渡していく = props drilling

---

## 🧠 学びポイント

- useReducer は状態の種類が多くなっても管理がしやすくなる
- props drilling は構成が深くなると管理が大変になる → Context API へ繋がる
- 配列操作や dispatch パターンは今後の React 開発で頻出！

---

## ✅ 使用した主な React 機能

| 機能                 | 内容                           |
| -------------------- | ------------------------------ |
| useReducer           | 複雑な状態管理                 |
| dispatch             | 更新命令の送信                 |
| props                | 親 → 子 → 孫へのデータ受け渡し |
| .map()               | 配列表示                       |
| 条件付きレンダリング | チェック状態で線を引くなど     |

---

次ステップ → Context API による共通状態管理へ進む！
