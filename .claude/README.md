# .claude/ ディレクトリについて

Claude Code 自身の振る舞いに関する設定を置く場所。`docs/` が「アイデア・知見・仕様」を扱うのに対し、こちらは「Claude がこのリポジトリでどう動くか」を扱う別軸のレイヤー。

- `rules/` — トピック別の作業ルール。常に効かせたいものはルート `CLAUDE.md` から `@import` する。1ファイル1トピック。
- `skills/` — 手順書。`/<スキル名>` で明示的に呼べるほか、依頼内容が description に合えば Claude が自動で使う。1スキル＝1ディレクトリ（`skills/<名前>/SKILL.md`）。
  - `new-idea` アイデア登録 ／ `idea-review` アイデア棚卸し・次の一手の提案 ／ `start-project` アイデアを実装に着手する（spec＋projects 雛形） ／ `dev-log` 実装引き継ぎメモ ／ `add-todo` todo 登録
- `knowledge/` — 事業知識（`docs/knowledge/`）ではなく、開発機・実行環境などクロスセッションで再利用したい技術的事実。

## まだ作っていないもの（SES_sales から必要になったら移植する）

先回りして空の仕組みは作らない。同じパターンを複数回繰り返す必要が出てから追加する。

- `agents/` ＋ `skills/autopilot/` ＋ `rules/autonomy.md` — 定期実行（Routine）でサブエージェントを動かし PR にする仕組み。無人で回したい業務（例: アイデアの定期棚卸し）が出たら、SES_sales の同名ファイルを手本に移植する。
- todo の Google Tasks 同期 — SES_sales の `src/sync_todos_to_gtasks.py`。`docs/todo/` のスキーマは互換にしてあるので、必要になればそのまま移植できる。
