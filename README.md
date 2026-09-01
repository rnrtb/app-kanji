# ラボ式・漢字プリントメーカー

漢字練習プリントをブラウザ上で生成し、PDF保存・印刷するための静的1ページサイトです。

## 全体像

サーバー・DB・ビルドツールなし。`index.html` を GitHub に push すると、Vercel が自動公開します。

```
ローカル編集 → git push (GitHub: rnrtb) → Vercel 自動デプロイ → 公開URL
```

## リポジトリ構成

| パス | 内容 |
| --- | --- |
| `index.html` | HTML / CSS / JS を集約 |
| `timer_logo_v2_3.png` | プリント右下のロゴ |
| `reference/` | レイアウト参考用 PDF（公開サイトでは未使用） |

- フレームワークなし（React 等なし）
- `package.json` なし → `npm install` 不要
- ビルド不要 → 編集後 push だけで反映

## 公開の流れ

1. ローカルで `index.html` 等を編集する
2. `git add` → `git commit` → `git push origin main`
3. Vercel が GitHub の `main` を検知して自動デプロイ（数秒〜1分）
4. 発行された `https://xxxx.vercel.app` で確認する

**ローカル確認:** ブラウザで `index.html` を直接開く。

## 保守に使うサイト

| サービス | URL | やること |
| --- | --- | --- |
| GitHub（ソース） | https://github.com/rnrtb/app-kanji | コード管理、push |
| Vercel（ホスティング） | https://vercel.com/dashboard | デプロイ状況、ドメイン |
| 本番サイト | （Vercel の発行 URL） | 公開確認 |

GitHub アカウントは **`rnrtb`** を使います。

## 技術メモ

- **CSS:** Tailwind CSS を CDN（`cdn.tailwindcss.com`）経由で使用
- **フォント:** UDデジタル教科書体。未インストール時は BIZ UDPゴシック等にフォールバック
- **PDF:** ブラウザの印刷（`window.print()`）と `@page` CSS で A4 を指定
- **共有:** タイトル・問題データ等は URL パラメータで復元できる

## よく触る作業

| 作業 | 変更場所 |
| --- | --- |
| 文言・レイアウト | `index.html` |
| ロゴ差し替え | `timer_logo_v2_3.png`（ファイル名を変える場合は HTML の `src` も更新） |
| 独自ドメイン追加 | Vercel + DNS 設定 |
