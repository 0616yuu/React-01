# 🧠 React開発スタート完全メモ【Vite展開＋ターミナル操作】

---

## ✅ プロジェクトを新規作成してReactで始めるまでの流れ

---

### ▶ 1. ターミナルを開く（Mac）

```bash
cd ~/Desktop
```

→ デスクトップに移動

---

### ▶ 2. プロジェクト用フォルダ作成

```bash
mkdir memo-app
cd memo-app
```

---

### ▶ 3. ViteでReactテンプレートを作成

```bash
npm create vite@latest . -- --template react
```

- `.` → 今いるディレクトリに生成
- `--template react` → React構成で作る

Enterでいくつか質問に答えて進む（基本は全部EnterでOK）

---

### ▶ 4. パッケージをインストール

```bash
npm install
```

---

### ▶ 5. 開発サーバーを起動

```bash
npm run dev
```

---

### ▶ 6. ブラウザで表示を確認

ターミナルに出る👇を開く：

```
http://localhost:5173/
```

---

## 🗒 プロジェクト構成（主なファイル）

```plaintext
memo-app/
├— index.html ← ベースHTML
├— vite.config.js ← 設定ファイル
└— src/
    ├— main.jsx ← アプリ起動ポイント
    └— App.jsx ← 自分のコードを書く場所
```

---

## ✨ 次にやるべきこと

- `App.jsx`を自分のコードで上書きする
- コンポーネント分けたいなら、`src/`に`.jsx`ファイル追加して`import`

---

