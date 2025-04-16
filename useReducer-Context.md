# Step4: useReducer + Context API（状態管理の本格導入）

## 🗓️ 日付

2025/04/14

## 🎯 目的

- 複雑な状態を整理して管理するために、useReducer を導入
- 複数コンポーネント間で状態を共有するために、Context API を併用

---

## 🧩 構成（ファイルと役割）

```
src/
├── App.jsx             // 全体の画面
├── context/
│   └── MemoContext.jsx // 状態管理ロジック（useReducer + Context）
├── components/
│   ├── MemoForm.jsx    // 入力・追加フォーム
│   └── MemoList.jsx    // メモ一覧表示（削除機能も）
```

---

## 🧠 用語と役割の解説

### ✅ useReducer

状態（state）を「どんな操作（action）でどう変えるか？」をまとめて管理するフック。

- `state`: 現在の状態（ここではメモの一覧）
- `dispatch`: 命令を送る関数（操作を実行させる）
- `reducer`: 実際に処理する関数（命令の種類に応じて state を変更）

### ✅ Context API

state と dispatch をアプリ全体で共有できるようにする仕組み。
props drilling を回避して、どこからでも「命令（dispatch）」や「状態（state）」にアクセスできるようにする。

---

## ⚙️ MemoContext.jsx の構造

```jsx
import { createContext, useReducer } from "react";

// ✅ 1. Contextを作成
export const MemoContext = createContext();

// ✅ 2. reducer関数（操作の種類とその処理）
const reducer = (state, action) => {
  switch (action.type) {
    case "ADD_MEMO":
      return { ...state, memos: [...state.memos, action.payload] };
    case "DELETE_MEMO":
      return {
        ...state,
        memos: state.memos.filter((_, index) => index !== action.payload),
      };
    default:
      return state;
  }
};

// ✅ 3. Provider（他のコンポーネントに共有する箱）
export const MemoProvider = ({ children }) => {
  const initialState = { memos: [] };
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <MemoContext.Provider value={{ state, dispatch }}>
      {children}
    </MemoContext.Provider>
  );
};
```

---

## 📦 reducer とは？

```jsx
const reducer = (state, action) => {
  switch (action.type) {
    case "ADD_MEMO":
      return { ...state, memos: [...state.memos, action.payload] };
    // action.payload → 追加するメモ文字列

    case "DELETE_MEMO":
      return {
        ...state,
        memos: state.memos.filter((_, index) => index !== action.payload),
      };
    // action.payload → 削除したいindex番号

    default:
      return state;
  }
};
```

### 🔍 各パーツの意味

- `state`: 現在の状態（{ memos: [...] }）
- `action`: 操作内容を表すオブジェクト（type と payload を含む）
- `switch`: 操作の種類ごとに処理を分ける
- `case "ADD_MEMO"`: 特定の指示に対する処理を分ける
- `...state`: 今の状態を引き継ぎつつ
- `memos: [...]`: memos の部分だけ新しく作り直す

---

## 📣 命令の送り方（dispatch の使い方）

たとえば、メモを追加したい場合：

```jsx
dispatch({ type: "ADD_MEMO", payload: "やること" });
```

- `type`: 処理の種類（reducer の中でどの case に行くか）
- `payload`: 実際に渡す値（この例だと「やること」）

---

## ✅ props drilling との違いとメリット

| 項目             | props drilling     | Context API              |
| ---------------- | ------------------ | ------------------------ |
| データの渡し方   | 親 → 子 → 孫と渡す | 直接アクセスできる       |
| 深い構造になると | 面倒・読みにくい   | どこでも使える           |
| 状態管理         | 親に集中しやすい   | どこでも dispatch できる |
| おすすめ場面     | 小規模 or 単発の値 | グローバルな状態         |

---

## 📝 学びポイント

- `useReducer` は操作ごとの分岐がキレイに書ける
- `Context API` を併用することで、複数コンポーネントから操作できる
- `dispatch({ type: ..., payload: ... })` で命令を飛ばす
- `reducer()` が実際に state を変更する処理担当

---

次は `MemoForm.jsx` と `MemoList.jsx` を Context に対応させていく！
