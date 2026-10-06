# Coding conventions

- 実装は `projects/<プロジェクト名>/` に閉じる。プロジェクトごとに独立した `requirements.txt`（Node なら `package.json`）を持ち、他プロジェクトのコードを直接 import しない。複数プロジェクトで同じ処理が3回目に必要になったら、共通化（`shared/` の新設など）を検討し、`変更履歴.md` に記録する。
- プロジェクト名は英小文字のスネークケース（例: `meeting_digest`）。`README.md` の冒頭に紐づく `IDEA-XXXX`／`SPEC-XXX` を書く。
- テストはプロジェクト直下の `tests/` に置く。CI（`.github/workflows/ci.yml`）は `projects/*/tests/` があるプロジェクトを自動で見つけて pytest を実行するので、実通信（外部 API・Google 等）を伴わないテストにする。
- パス解決は `Path(__file__).resolve().parents[N]` でプロジェクトルートを求める（SES_sales の `src/core/config.py` と同じパターン）。カレントディレクトリに依存しない。
- 秘密情報（APIキー・トークン・サービスアカウント鍵・Webhook URL）は `.env` または `config/*.json`（`.gitignore` 済み）にのみ置く。テンプレートは `.env.example`／`*.example.json` として追跡する。プロジェクト固有の環境変数も `.env.example` に追記し、用途をコメントで書く。
- モジュール冒頭の日本語docstringには「何をするか」ではなく「なぜそうしているか」（前提・注意点・既知の制約）を書く。
- 試作は小さく始める。まず動く最小構成（1ファイル＋テスト）を作り、アイデアの仮説が検証できてから構造を整える。
- 既存データを一括で直す一時スクリプトは、DryRun → 本実行の2段階にし、人が直した値は上書きせず、終わったら削除する（SES_sales `.claude/rules/coding.md` と同じ型）。
