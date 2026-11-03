# 公式ドメイン × GitHub Pages 設定手順（管理担当向け）

トップに「準備中」ページ、各作品を `https://studio-arts.jp/作品名/` で公開するための初期設定です。
仮に ドメイン＝`studio-arts.jp`、Organization＝`［Organization名］` と書いています。

```
訪問者 → studio-arts.jp
          │ ① Xserver の DNS が GitHub Pages を指す
          ▼
       GitHub Pages
          │ ② 確認済みドメインとして ［Organization名］ に紐づく
          ▼
  ［Organization名］.github.io     → https://studio-arts.jp/            （準備中ページ → 将来HP）
  ［Organization名］/ryo-shindan   → https://studio-arts.jp/ryo-shindan/
```

---

## 1. Organization を作る
- GitHub 右上の ＋ → **New organization** → **Free**
- Organization 名は URL に出ないので自由（例：`studio-arts-mm`）
- **Settings → Authentication security → Require two-factor authentication** をオン（推奨）
- **People** で自分の表示を **Private** に（個人アカウントをたどられにくくする）
- Owner は自分＋予備1人まで。メンバーは **Member** で招待

## 2. トップ用リポジトリを作る
- Organization 内に **`［Organization名］.github.io`**（この名前ちょうど）の **Public** リポジトリを作る
- 中身は、`studioarts-site` の `org-site/` フォルダの中身（`index.html` / `404.html` / `images/`）
  - Claude に頼めばアップロードまで行います（リポジトリへのアクセス許可が必要）
- **Settings → Pages**：Source を `main` ／ `/(root)` にして Save

## 3. ドメインの所有確認（乗っ取り防止）
- Organization の **Settings → Pages → Add a domain** に `studio-arts.jp` を入力
- 表示される **TXT レコードの名前と値** を控える

## 4. Xserver の DNS 設定
Xserver のドメイン管理画面 → 対象ドメイン → **DNSレコード設定**

| ホスト名 | 種別 | 内容 |
|---|---|---|
| （空欄＝ドメイン直下） | A | 185.199.108.153 |
| （空欄） | A | 185.199.109.153 |
| （空欄） | A | 185.199.110.153 |
| （空欄） | A | 185.199.111.153 |
| www | CNAME | ［Organization名］.github.io |
| 手順3の名前 | TXT | 手順3の値 |

- 初期設定で入っている **ドメイン直下と www の A レコードは削除**
- 「DNSレコード設定」が編集できない場合は、ネームサーバーが Xserver（`ns1.xserver.jp` など）になっているか確認

## 5. GitHub 側で接続
1. 手順3の画面で **Verify**（反映待ちで失敗したら時間をおいて再実行）
2. `［Organization名］.github.io` の **Settings → Pages → Custom domain** に `studio-arts.jp` → Save
3. チェックが通ったら **Enforce HTTPS** をオン（証明書発行に最大1日ほど）

## 6. 確認
- `https://studio-arts.jp/` → 準備中ページ
- `https://studio-arts.jp/存在しないURL` → 404 ページ
- 作品リポジトリで Pages をオン → `https://studio-arts.jp/作品名/`

---

## トップの「NOW PLAYING」に作品を載せる
`［Organization名］.github.io` の `index.html` 内、`const WORKS = [` の中に1行追加：

```js
const WORKS = [
  { title: '寮診断', url: '/ryo-shindan/', note: '診断' },
];
```
空のままなら欄ごと表示されません。

## HP 本体を公開するとき
`［Organization名］.github.io` の中身を、新デザイン（`studioarts-site` の確認用ブランチ）に差し替えるだけ。URL・DNS は変更不要。

## 持ち回らない情報
- Xserver のログイン情報（ドメインの乗っ取り・失効の危険）
- ドメインの更新日・支払い方法（**自動更新オン** と、カード期限を確認）
