# Machine / environment facts

- 通常の開発機は Windows（SES_sales と同じ機体を想定）。シェルは PowerShell、Python は `py` ランチャー経由、仮想環境は `.venv\Scripts\python.exe`（未作成のことがあるため都度確認する）。作業ディレクトリの実体パスは未確認なので、判明したらここに追記する。
- Claude Code on the web・リモート実行環境では Linux コンテナ上で動作し、上記の Windows 固有パスは無関係になる。作業を始める前に、どちらの環境で動いているか（platform / シェル）を確認してからパス操作を行う。
- Linux 環境ではシステムの Python に依存せず、プロジェクトごとに `python -m venv .venv && .venv/bin/pip install -r projects/<名前>/requirements.txt pytest` で仮想環境を用意する（SES_sales でシステムの `cryptography` が壊れていたことがあるため）。
