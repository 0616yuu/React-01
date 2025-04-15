# STEP4: Context APIで状態を共有する（2025/04/14）

## 1. タイトル＋日付
**Context APIで状態を共有する学習（2025年4月14日）**

---

## 2. 目的
**props drilling を回避して、どの階層からでも状態を使えるようにするための Context API を理解し、実装できるようになる。**

---

## 3. フォルダ構成（全体像）

```
src/
├── App.jsx                  // アプリのエントリーポイント
├── components/
│   ├── Parent.jsx          // 中間コンポーネント
│   └── Child.jsx           // 状態の表示と更新をする
└── context/
    └── MessageContext.jsx  // Context定義とProvider
```

---

## 4. 各ファイルのコードと説明

### MessageContext.jsx（Contextの定義とProvider）
```jsx
import { createContext, useState } from "react";

export const MessageContext = createContext();

export function MessageProvider({ children }) {
  const [message, setMessage] = useState("ようこそ");

  return (
    <MessageContext.Provider value={{ message, setMessage }}>
      {children}
    </MessageContext.Provider>
  );
}
```

- `createContext()`：共有する箱を作る
- `MessageProvider`：全体を囲んで中の子供に `value` を渡す
- `value` の中に `message`（状態）と `setMessage`（更新関数）を入れている

---

### App.jsx（Providerで全体を囲む）
```jsx
import { MessageProvider } from "./context/MessageContext";
import Parent from "./components/Parent";

function App() {
  return (
    <MessageProvider>
      <Parent />
    </MessageProvider>
  );
}

export default App;
```

- `MessageProvider` で `Parent` を囲むことで、その中のどこでも Context が使えるようになる

---

### Parent.jsx（中間のコンポーネント）
```jsx
import Child from "./Child";

function Parent() {
  return (
    <div>
      <h2>👪 Parentコンポーネント</h2>
      <Child />
    </div>
  );
}

export default Parent;
```

- ここでは特に props を受け渡ししない（Contextがあるから！）

---

### Child.jsx（実際に状態を使うコンポーネント）
```jsx
import { useContext } from "react";
import { MessageContext } from "../context/MessageContext";

function Child() {
  const { message, setMessage } = useContext(MessageContext);

  return (
    <div>
      <h3>👶 Childコンポーネント</h3>
      <p>📩 メッセージ：{message}</p>
      <button onClick={() => setMessage("こんにちは、世界！")}>更新</button>
    </div>
  );
}

export default Child;
```

- `useContext()` を使って、props なしでデータを取得＆更新できる

---

## 5. Context APIを使う流れ

| ステップ | 内容 |
|--------|------|
| 1. | `createContext()` で箱を作る |
| 2. | Provider を作って囲む（`children` を中に） |
| 3. | value に状態と関数を渡す |
| 4. | `useContext()` で取り出す（どの階層でもOK） |

---

## 6. props drilling の問題点と Context のメリット

### ❌ props drilling とは？
- 深い階層まで「props を手渡ししないといけない」状態。
- 親 → 子 → 孫 → ひ孫・・・と渡すのがめんどくさいし、バグの原因になる。

### ✅ Context API のメリット
- 親や中間を通さず、どの階層からでもデータを「直接」読める
- コードがシンプルで読みやすくなる
- 状態の管理場所を1ヶ所にまとめられる

---

## 7. 学びポイント
- `useContext()`はどのコンポーネントでも使える（Providerの中なら）
- `props` を使わないで済むから、開発効率が上がる
- 設計の段階で「共通の状態をContextにまとめる」発想が大事

---

次のステップ：`useReducer` に進む！
