# CLAUDE.md — lindh.github.io 管理ガイド

このリポジトリは林冬惠（Donghui Lin）の個人ホームページ。
**Jekyll + GitHub Pages**。`master` ブランチに push すると GitHub Pages が
自動でビルド・公開する（`https://lindh.github.io/`）。ローカルでの手動デプロイは不要。

## 大原則

- 編集対象は基本的に **コンテンツの `.md` ファイルのみ**。
- 構造・デザインに関わる `_layouts/` `_sass/` `_config.yml` `assets/css/` は
  **勝手に変更せず、必ず確認を取ってから**触る。
- 変更は「編集 → diff を見せる → 承認 → commit → push」の順で、段階的に進める。
- commit メッセージは簡潔に（例: `Update publication list (Jun 2026)`）。

## ファイル構成と役割

| ファイル | 役割 | 主な更新タイミング |
| --- | --- | --- |
| `index.md` | トップ。プロフィール・所属・連絡先・各種リンク | 異動・肩書き変更時 |
| `research.md` | 研究紹介（Research Topics / Projects） | 新規プロジェクト採択時 |
| `publication.md` | 業績リスト（最重要・更新頻度高） | 論文採録のたび |
| `students.md` | 指導学生リスト | 年度替わり・修了時 |
| `teaching.md` | 担当講義一覧 | 年度替わり |
| `_config.yml` | サイト設定（title / theme / analytics） | ほぼ触らない |
| `_layouts/` `_sass/` `assets/css/` | テーマ・デザイン | 触らない（要確認） |
| `files/` | 配布PDF（論文等） | 論文PDF追加時 |
| `images/` | 画像（プロフィール写真等） | 随時 |

## 全ページ共通の規約

- フロントマターは必ず以下で開始する。消さない・変えない:
  ```
  ---
  layout: default
  ---
  ```
- フロントマター直後に**共通ナビ行**を置く（全ページで同一に保つ）:
  ```
  [Home](https://lindh.github.io/)&emsp; [Teaching](./teaching.html) &emsp; [Research](./research.html) &emsp; [Publications](./publication.html) &emsp; [Supervised Students](./students.html)
  ```
- リンクはページ間が `.html`（`./teaching.html` 等。`.md` ではない）。
- 和文の句読点は「、」「。」に統一。英文と和文が混在するページでも和文部分はこれに従う。

## ファイル別の編集規約

### publication.md（最重要）
- セクション: Books / Guest Editorial / Journal Papers / Journals in Japanese /
  Book Chapters / International Conference Papers。冒頭のアンカー目次と対応させる。
- 各エントリは1行。著者→`"タイトル,"`→`_誌名/会議名_`(イタリック)→巻号頁→年→`[[DOI](URL)]`。
  既存行の形式を必ず真似る。著者名のうち `Donghui Lin` は本人。
- 新しい論文は各セクションの**先頭（新しい順）**に追加する。
- 編集したら冒頭の `(Last updated: ...)` を当月に更新する。
- PDF を配布する場合は `files/` に置き、`[[PDF](./files/xxx.pdf)]` でリンク。

### students.md
- `### Master Students` と `### Undergraduate Students` に分類。
- 在学中は `- 名前 (Ongoing)`、修了・卒業は `- 名前 (Bachelor degree, Mar. YYYY)` /
  `(Master degree, Mar. YYYY)` の形式。

### teaching.md
- 和文中心。`講義名/英名，学期，言語，所属，年度` の区切りは全角カンマ「，」。
- 編集したら `(Last updated: ...)` を更新。

### research.md
- Research Topics（3本柱）と Research Projects のリスト構成を維持。
- Project は `- タイトル, **役割**, 助成種別(番号), 期間` の形式。

### index.md
- プロフィール本文と Researcher Database Links（DBLP/KAKEN/ORCID 等）を維持。
- 連絡先のメールは spam 回避で `lindh at okayama-u.ac.jp` 表記（`@` を書かない）。

## ローカルプレビュー（任意）

push 前に見た目を確認する場合（Ruby + Bundler 必要）:
```bash
bundle install
bundle exec jekyll serve   # → http://localhost:4000
```
うまく動かない場合は標準 Ruby が原因のことが多い。rbenv 等の導入を検討。

## 公開までの流れ

```bash
git pull            # 作業開始時。3台のMac間はこれで同期
# （Claude Code が .md を編集）
git diff            # 変更確認
git add -A && git commit -m "..."
git push            # 数分で本番反映
```

## やってはいけないこと

- `_config.yml` の `theme` / `title` / `google_analytics` を無断変更しない。
- `_layouts/` `_sass/` を無断で書き換えない（サイト全体が崩れる）。
- ナビ行・フロントマターを削除しない。
- メールアドレスを `@` 付きの生テキストにしない。
