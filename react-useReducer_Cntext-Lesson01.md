# 【Reactメモアプリ説明書】

## ▶ 作成日
2025/04/16

## ▶ 概要
Reactの`useState` / `useReducer` / `Context API`を駆使したメモアプリ。基本功能(追加 / 削除 / 編集 / チェック)を完備。コンポーネント分割も行い、実務でも使えるスタイルに近づけた構成にしている。

---

## ▶ 構成ファイル

```
/src
  ├アプリ本体(App.jsx)
  ├ components/
  │   ├ MemoList.jsx
  │   └ MemoItem.jsx
  ├ context/
  │   └ MemoContext.jsx
  └ reducer/
      └ memoReducer.js
```

---

## ▶ 実装機能と説明

### （ᵃ＿＿＿）Context API + useReducer の基本構成

- `MemoContext.jsx`
  - createContext() で作成
  - Providerを用意して `state` / `dispatch`を入れる

- `memoReducer.js`
  - メモ構成:
    ```js
    {
      text: "入力されたメモ",
      isDone: false,
      isEditing: false
    }
    ```
  - switch-case で変更管理
    - ADD_MEMO
    - DELETE_MEMO
    - START_EDIT / UPDATE_MEMO / CANCEL_EDIT
    - TOGGLE_DONE

---

### （ᵃ＿＿＿）App.jsx
- Providerでメモアプリ全体を包む
- `MemoList`を表示

---

### （ᵃ＿＿＿）MemoList.jsx

- 入力値(input) とメモ配列(memos)を管理
- dispatch(行動) 一覧
  - `ADD_MEMO`（追加）
  - `DELETE_MEMO`（削除）
  - `START_EDIT`（編集開始）
  - `UPDATE_MEMO`（更新確定）
  - `CANCEL_EDIT`（キャンセル）
  - `TOGGLE_DONE`（チェックON/OFF）

---

### （ᵃ＿＿＿）MemoItem.jsx

- 1件ずつのメモを表示
- 表示切り替え(編集モードのON/OFF)
- チェックボックス、更新、削除、キャンセル
- propsで受け口指定: `memo`, `index`, `onUpdate`, `onCancel`, `onDelete`, `onToggle`

---

## ▶ 実装準を整える方法

1. `useReducer` の利点
    - 複数の変更を一緒のロジックで管理
    - `switch-case` で動作分定

2. `Context` の利点
    - 任意のコンポーネントで `state` / `dispatch`が使える
    - props drilling 解決

3. 分割のポイント
    - `App.jsx`: Providerと入口
    - `MemoList`: 表示管理
    - `MemoItem`: 1個ずつのメモを管理

---

## ▶ 実装中の注意点

- `useContext(MemoContext)`は、必ず`MemoProvider`で包んだ上で実行
- `dispatch({ type: “タイプ”, payload: 値 })`は例外やミスを避ける
- 表示切り替えは`memo.isEditing`で分岐
- `textDecoration: memo.isDone ? "line-through" : "none"`でチェック表示

---

## ▶ 今後のステップ

1. チェック機能 (完了)
2. ローカルストレージ / Firebase保存
3. 説明書(.md)をポートフォリオ用に修正

---

## ▶ まとめ
Reactの基礎、独立した実装力、結合的に使えるメモアプリを作成できたら、ポートフォリオとしても効果突立。

これを元に「チャットアプリ」や「ログイン機能付きToDo」への発展も楽になるぞ！

---

