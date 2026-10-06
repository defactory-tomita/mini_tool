---
name: start-project
description: docs/ideas のアイデアを実装に着手する。仕様書（docs/spec/）と実装ディレクトリ（projects/<名前>/）の雛形を作り、アイデアのステータスを「実装中」にする。「IDEA-XXXXを作り始めて」「これ実装しよう」「プロトタイプを作って」などで使う。
---

# 実装への着手

## 0. 前提の確認
- 対象の `docs/ideas/IDEA-XXXX_*.md` を読む。アイデアが未登録なら、先に `new-idea` スキルで登録する（実装だけが先行して、なぜ作ったか分からなくなるのを防ぐため）。
- スコープ（最初に作る最小構成と、今回やらないこと）をユーザーと合意する。合意できていなければ、聞いてから進める。

## 1. 仕様書
- `docs/spec/<対象>_spec.md` を作る。フロントマターと章立ては `docs/spec/README.md` に従い、`version: 0.1`・`status: ドラフト` で始める。
- doc_id は `origin/main` 上の最大 SPEC 番号 +1。
- 小さな試作で仕様書が過剰なら、ユーザーに確認したうえで省略してよい（その場合 dev-log の doc_id は IDEA-XXXX を使う）。

## 2. 実装ディレクトリ
`projects/README.md` の標準構成で `projects/<プロジェクト名>/` を作る。
- `README.md`: 冒頭に `IDEA-XXXX` / `SPEC-XXX`、何をするか、使い方、必要な環境変数。
- `requirements.txt`、エントリーポイント、`tests/`（最低1本、実通信なし）。
- 新しい環境変数はルート `.env.example` に用途コメント付きで追記する。
- 規約は `.claude/rules/coding.md`。

## 3. 紐づけ
- アイデアのフロントマター `spec`・`project` を埋め、`ステータス: 実装中`、判断ログに行を足す。
- `docs/ideas/README.md`・`docs/spec/README.md`・`projects/README.md` の一覧表を更新する。

## 4. 検証
- `python -m venv .venv && .venv/bin/pip install -r projects/<名前>/requirements.txt pytest` → `cd projects/<名前> && ../../.venv/bin/python -m pytest -q` が通ることを確認してからコミットする。
- 区切りがついたら `dev-log` スキルで引き継ぎメモを残す。
