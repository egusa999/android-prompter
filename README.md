## Usage

1. Open `prompter.html` in Chrome on your tablet → under **① Script**, select a `.md`/`.txt` file (or paste text directly), then set the speed and font size under **② Speed & Appearance**.
2. Tap **"Start Fullscreen"** → after a 3-second countdown, the script auto-scrolls at a constant speed (px/sec).
3. When the end of the script is reached, scrolling stops automatically and shows "Reached the end" — it won't scroll past that point.

## During playback

- **Swipe up/down**: manual scroll (release to resume auto-scrolling at the set speed)
- **Tap**: pause / resume
- **Top-right controls**: speed ±5, jump to start, exit

You can also set a target **read time (minutes)** and tap **"Fit to this time"** to auto-calculate the scroll speed — the estimated duration updates live. **Mirror mode** (for teleprompter beam-splitter rigs) and a **center guideline** can be toggled from the setup screen. The screen is kept awake during scrolling so it won't dim mid-take.

# プロンプター（PWA）

Androidタブレット向けのプロンプター。`.md` / `.txt` の原稿を全画面で等速スクロール表示します。

- 原稿ファイルを選択（または直接貼り付け）＋スクロール速度を指定
- 全画面で指定した速さ（px/秒）で自動スクロール
- 上下スワイプで手動スクロール、タップで一時停止／再開
- 原稿の最後まで到達したら自動停止

## 公開手順（GitHub Pages）

PWAとしてインストールするには **https での公開が必須**です（`file://` で直接開いた場合、インストールはできませんが動作自体はします）。

```bash
# このフォルダで（git init / 初回コミットは実施済み）
git remote add origin https://github.com/<ユーザー名>/<リポジトリ名>.git
git branch -M main
git push -u origin main
```

そのあと GitHub のリポジトリで:

1. **Settings** → 左メニュー **Pages**
2. **Source** を `Deploy from a branch`、**Branch** を `main` / `/ (root)` にして **Save**
3. 1〜2分で `https://<ユーザー名>.github.io/<リポジトリ名>/` が公開されます

## タブレットへのインストール

1. Android の Chrome で公開URLを開く
2. 右上メニュー → **アプリをインストール**（または「ホーム画面に追加」）
3. ホーム画面のアイコンから起動すると、アドレスバーなしの全画面で開きます

> インストール後もページを開くたびに更新チェックが走ります（ネットワーク優先）。
> 一度開けば電波がなくても起動できます。

## 更新の反映

`index.html` などを変更して push したあと、確実に反映させたい場合は `sw.js` の

```js
const CACHE = 'prompter-v1';
```

の数字を上げてからコミットしてください。古いキャッシュが破棄されます。

## 操作一覧

| 操作 | 動作 |
| --- | --- |
| タップ | 一時停止／再開 |
| 上下スワイプ | 手動スクロール（離すと自動スクロール再開） |
| 右上 − / ＋ | 速度を 5 px/秒ずつ調整 |
| 右上 ↺ | 先頭に戻る |
| 右上 ✕ | 終了して設定画面へ |
| スペースキー | 一時停止／再開（PC） |
| ↑ / ↓ キー | 手動スクロール（PC） |
| Esc | 終了（PC） |

## ファイル構成

```
index.html               アプリ本体（HTML/CSS/JS すべて内包）
manifest.webmanifest     PWAマニフェスト（アイコン・全画面表示の設定）
sw.js                    Service Worker（インストール可能化＋オフライン起動）
icons/                   アイコン一式（192 / 512 / maskable / apple-touch）
.nojekyll                GitHub Pages で Jekyll 処理を無効化
```
