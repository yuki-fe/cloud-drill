# CLAUDE.md

このファイルは、このリポジトリで作業する Claude Code 向けのガイドです。人向けの説明は `README.md` にある。

## プロジェクト概要

AWS 認定クラウドプラクティショナー（CLF-C02）の学習サイト **「クラウド用語ドリル」**。運営者は Yuki-fe（個人・副業）。姉妹サイト「ITパスポート用語ドリル」（デスクトップの `ip-drill`）の build.py をもとに作った。FE用語ドリル（`claude FE対策サイト`）も同じ運営者。

- **サイト**: https://cloud.yogo-drill.com/ （予定。GitHub Pages。リポジトリ `yuki-fe/cloud-drill` の `main` ブランチの `/docs`）
- 用語の単語帳（カード・4択・書いて答える・復習・一覧）、用語ごとの解説ページ、分野別ミニテスト（`test.html`、4分野から20問）、略語クイズと早見表（`abbr.html`）
- 用語は `data/make_terms.py` に書き、実行して `data/terms.json` を作る。出題範囲は AWS の試験ガイド CLF-C02（2026年10月12日版）の4分野と「In-Scope AWS Services」に合わせた
- お問い合わせは FE と同じ Google フォーム https://forms.gle/s4yB1xMbcoRqZps2A

## よく使うコマンド

```powershell
python data/make_terms.py               # 用語を直したら
python build.py                         # docs/ を作り直す（エラー・注意が出たら直す）
python -m http.server 8000 -d docs      # http://localhost:8000 で確認
```

- Windows のコンソールは cp932 なので、日本語を出力するスクリプトは `PYTHONIOENCODING=utf-8` を付けて動かす
- build.py は Python の標準ライブラリだけで動く

## 公開までの流れ

1. 編集する
2. `python build.py`
3. 運営者が **GitHub Desktop** で commit → push する（運営者はコマンドの git に慣れていない。手順は GitHub Desktop の画面で説明する）
4. 数分で公開サイトに反映される

## 決まりごと

- **レイアウト**（2026-10-23 に入れた）: 見た目の土台は `static/assets/style.css`、その上に全サイト共通の `static/assets/layout.css`（FE用語ドリルのものと同じファイル。直すときは FE で直して、各サイトにコピーする）。トップは「見出し・説明・数字・あなたの進み具合」→「学習する」（学び方はタブ）→「できること」のカード→説明。用語ページは本文と右の「この用語を練習する」「同じ分野の用語」の2列（スマホは1列）。学習の画面（app.js）が使う `#modes`・`#fields`・`#toolbar`・`#panel`・`#reset` は消さない
- ユーザーへの回答は **日本語**。運営者は初心者寄りなので、手順は画面のボタン名まで具体的に書く
- `docs/` は生成物。直接編集しない（ただし GitHub Pages が使うので commit はする）
- 公開後は用語の id（並び順）を変えない。新しい用語は `TERMS` の最後に足す
- localStorage の名前は `cloud-drill-` で始める（FE・ITパスポートと同じオリジンなので、名前が同じだと進み具合が混ざる）
- **AWS の商標**: サイト名・ドメインに「AWS」を入れない（URL のパスは可）。AWS のロゴを使わない。「AWS 認定クラウドプラクティショナーの用語」と事実として文字で書くだけにする。AWS と関係がある・認められていると取られる書き方（「公式」など）をしない。フッターの商標の注意書きを消さない
- サービスの名前・機能・料金・サポートプランは変わる（例: 2025年12月にサポートプランが Business Support+・Enterprise Support・Unified Operations に再編、Developer・Business・Enterprise On-Ramp は 2027年1月1日に終了）。料金の金額など変わりやすい数字は書かない。試験ガイドが改訂されたら用語を見直す
- 「必ず合格」など確かめられない言い切りは使わない。広告は「PR」の表示を消さない（ステルスマーケティング規制）
- 用語の説明は AI の支援で作ったもの。足すときは AWS のドキュメントで確かめる
- トークン・合言葉・個人情報はリポジトリに入れない。リポジトリは **公開**
- 手順書・計画などの資料は FE 側の `notes/`（公開しない）で作る
