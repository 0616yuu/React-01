# Git / GitHub環境構築メモ

## SSH鍵の生成
```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```
- ファイル保存場所はそのままEnter（デフォルト）
- パスフレーズは空でもOK（Enter2回）

## 公開鍵の確認とコピー
```bash
cat ~/.ssh/id_ed25519.pub
```
- 表示された1行をすべてコピー（先頭が `ssh-ed25519` で始まる）

## GitHubに鍵を登録
1. GitHubにログイン
2. [SSHキー設定ページ](https://github.com/settings/keys) にアクセス
3. "New SSH key" を選択し、タイトルとコピーしたキーを貼り付け
4. "Add SSH key" を押す

## GitHubリモートをSSH接続に変更
```bash
git remote set-url origin git@github.com:0616yuu/React-01.git
```

## pushが通るか確認
```bash
git push origin main
```
- 初回接続時は「Are you sure you want to continue connecting?」と聞かれる → `yes` と入力
- その後 "Everything up-to-date" が出れば成功！

---

## `git push` とは何か

- ローカルのリポジトリ（自分のPC）で作った変更を、リモートのリポジトリ（GitHub）にアップロードするコマンド。
- 簡単に言うと「**手元のメモをGitHubというクラウドに提出する命令**」。

### わかりやすい流れ：

1. `git add` → 提出したいファイルを選ぶ
2. `git commit` → 内容を「封筒に詰める」（スナップショット）
3. `git push` → GitHubのポストに入れて提出！

### なぜ重要？
- クラウドに保存できる → バックアップになる
- 自分の勉強ログを残せる → 振り返り＆証明
- チーム開発では進捗共有ツールになる
- ポートフォリオとして使える

### よく使う関連コマンド
| コマンド | 意味 |
|----------|------|
| `git add .` | すべての変更を追加対象にする |
| `git commit -m "コメント"` | コメント付きで変更を保存する |
| `git push origin main` | mainブランチに変更をアップする |
| `git pull` | GitHubから変更を取得する（他人と協業する場合） |

---

pushが「成功」してるということは、

> ✅ GitHubに安全に接続できていて、
> ✅ 変更が反映されていて、
> ✅ ローカルとクラウドの状態が一致している

という最高の状態ってこと！

