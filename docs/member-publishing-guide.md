# STUDIO ARTS 作品公開ガイド（メンバー向け）

診断・特設ページなどを、公式ドメインの下で公開するための手順です。
`［ドメイン］` と `［Organization名］` は管理担当から伝えられたものに読み替えてください。

---

## 公開されるURL

| 置き場所（GitHub） | 公開URL |
|---|---|
| `［Organization名］/［Organization名］.github.io` | `https://［ドメイン］/`（トップ。管理担当のみ） |
| `［Organization名］/ryo-shindan` | `https://［ドメイン］/ryo-shindan/` |
| `［Organization名］/作品名` | `https://［ドメイン］/作品名/` |

- 作品名（リポジトリ名）は **半角英小文字・数字・ハイフンだけ** にしてください（例：`ryo-shindan`）。これがそのままURLになります。
- ドメインの設定は不要です。Organization の中に作れば、自動でこのURLになります。

---

## 最初に1回だけやること

1. **GitHub アカウントを作る**（持っていればそのままでOK）
2. **ユーザー名を管理担当に送る** → Organization に招待が届くので承認する
3. **二段階認証をオンにする**
   Settings → Password and authentication → Two-factor authentication
4. **メールアドレスを非公開にする**
   Settings → Emails →「Keep my email addresses private」をオン
   同じ画面に表示される `数字+ユーザー名@users.noreply.github.com` を控えておく
5. **（パソコンから Git でアップロードする人だけ）本名がコミットに残らない設定をする**
   ```
   git config --global user.name "GitHubのユーザー名"
   git config --global user.email "4で控えたnoreplyアドレス"
   ```
   ブラウザからアップロードするだけの人は不要です。

---

## 作品を公開する手順

1. Organization のページで **New repository**
   - Owner：`［Organization名］`
   - Repository name：作品名（例：`ryo-shindan`）
   - **Public** を選ぶ
2. **Add file → Upload files** で、作品のフォルダの中身をまとめてドラッグ＆ドロップ
   - 最初に開くページのファイル名は **`index.html`** にする
   - フォルダ構成（画像フォルダなど）はそのまま保つ
3. 画面下の **Commit changes** を押す
4. リポジトリの **Settings → Pages**
   - Source：**Deploy from a branch**
   - Branch：**main** ／ **/(root)** → **Save**
5. 数分待って `https://［ドメイン］/作品名/` を開いて確認
6. 管理担当に「公開した」と連絡（トップページの NOW PLAYING に載せるか決めます）

### 修正したいとき
同じリポジトリに、直したファイルを同じ名前でアップロード → Commit changes。数分で反映されます。

### 公開をやめたいとき
Settings → Pages で Unpublish、または管理担当に連絡してください。

---

## 公開前チェック（必ず）

公開リポジトリは、サイトだけでなく **中のファイルやアップロード履歴まで誰でも見られます。**
一度公開した内容は、あとで消しても履歴やキャッシュに残ることがあります。

- [ ] ファイル・画像・コメント・メモに、**本名・住所・個人の連絡先** が入っていない
- [ ] **試作ファイル・没データ・使っていない画像** を入れていない
- [ ] **パスワード・APIキー・管理画面のURL** などを入れていない
- [ ] 他作品を参考にした場合、その **作品名や「〇〇風」などの文言** をファイルやコメントに書いていない
- [ ] フォント・画像・音素材は **利用規約上、Web公開してよいもの** だけ
- [ ] Canva などで書き出した画像は、作成者情報が埋め込まれることがある → 気になる場合は管理担当に相談
- [ ] 回答を集計・保存する仕組み（Googleフォーム連携など）がある場合は、**公開前に管理担当に相談**

---

## やらないでほしいこと

- トップページのリポジトリ（`［Organization名］.github.io`）の編集
- リポジトリの **Settings → Pages の Custom domain** 欄の入力（空欄のままでOK）
- Organization の設定変更

困ったら、画面のスクショを付けて管理担当に連絡してください。
