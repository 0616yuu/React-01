# React 学習ノート（STEP 3）

## 🎯 今回のテーマ：useState（+α：フォーム・チェックボックス操作）

Reactで「状態」を扱うときに使うのが `useState` フック。
これを理解しないと、Reactはただの見た目だけのマシーンになる。

---

## ✅ useStateとは？

- Reactの「関数コンポーネント内で状態（state）を持てるようにする」ためのフック
- 状態＝ユーザーの操作で変わる値（カウント、入力内容、ON/OFFなど）

### 例：カウンター（数字をカウントアップ）

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>現在のカウント: {count}</p>
      <button onClick={() => setCount(count + 1)}>+1</button>
    </div>
  );
}
```

### 🧠 解説
- `useState(0)` → 初期値0のstateを定義
- `count` → 今の状態
- `setCount` → 状態を更新する関数
- `setCount(count + 1)` → `count`を+1して再描画

---

## 🔁 状態が変わると何が起きる？

1. `setCount` が呼ばれる
2. `count` の値が変わる
3. コンポーネントが再描画（再レンダリング）される

→ だから、画面上の値も更新される！

---

## 🧪 練習①：増やす・減らす・リセットボタン

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <h2>現在のカウント：{count}</h2>
      <button onClick={() => setCount(count + 1)}>+1</button>
      <button onClick={() => setCount(count > 0 ? count - 1 : 0)}>-1</button>
      <button onClick={() => setCount(0)}>リセット</button>
    </>
  );
}
```

---

## 🧪 練習②：文字入力（テキストボックス）

```jsx
function TextInput() {
  const [text, setText] = useState("");

  return (
    <>
      <input
        type="text"
        value={text}
        onChange={(e) => setText(e.target.value)}
        placeholder="文字を入力してみ？"
      />
      <p>今の入力：{text}</p>
    </>
  );
}
```

### 💡 補足：
- `e` はイベントオブジェクト（イベントの全情報）
- `e.target` は「イベントが起きたHTML要素」
- `e.target.value` は「その要素の中に今ある値（入力文字）」

---

## 🧪 練習③：チェックボックスの状態管理

```jsx
function Checkbox() {
  const [isChecked, setIsChecked] = useState(false);

  return (
    <>
      <label>
        <input
          type="checkbox"
          checked={isChecked}
          onChange={(e) => setIsChecked(e.target.checked)}
        />
        バナナ好き？
      </label>
      <p>{isChecked ? "バナナおいしい" : "バナナくれ"}</p>
    </>
  );
}
```

### 💡 補足：
- `checked={isChecked}` でON/OFF状態を反映
- `e.target.checked` でtrue/falseを取得

---

## 🔚 まとめ

- `useState` は状態を使うための基本フック
- `数値・文字列・真偽値` どれでもOK
- JSXのフォーム部品と連携させることで、双方向のUIが作れる
- `onChange` / `onClick` と `useState` の組み合わせが基本

---

次のステップ候補：
- `useEffect` による副作用処理
- 複数の入力フィールド管理
- 簡易バリデーションや送信処理

GitHubへのpush・管理も完了済。

