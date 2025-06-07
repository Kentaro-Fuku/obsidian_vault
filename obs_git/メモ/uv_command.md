# uv(Pythonバージョン・パッケージ・仮想環境マネージャ)の使い方

## 概要
uv はPythonのバージョン、ライブラリ(パッケージ)、仮想環境をプロジェクトごとに管理するためのツールです。  
pyenv + virtualenv + poetryみたいな感じ。  
HPは[こちら](https://docs.astral.sh/uv/)

## インストール
公式ドキュメントを見てください。  
スタンドアロン型＋シェル補完だけ記載すると、  
>Windows  
`powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"`  
`Add-Content -Path $PROFILE -Value '(& uv generate-shell-completion powershell) | Out-String | Invoke-Expression'`  

## クイックスタートガイド
Python環境はインストールされておらず、uvがスタンドアロン型でインストールされている状況を想定  

1. Pythonのインストール  
`uv python install 3.X.X`: Pythonの3.Xをuv管理下にインストール。  
1. プロジェクトの作成  
`uv init new_project`: 新規プロジェクト(ディレクトリ)の立ち上げ。既存のものを使いたい場合は、そのディレクトリ内で`uv init`  
`cd ./new_project`: 作成したプロジェクトディレクトリに移動  
1. 仮想環境の作成  
`uv venv env_name --python 3.X`: 新規仮想環境env_nameという名称で作成、名前やバージョン指定は省略可能  
1. パッケージのインストール  
`uv add package`: 必要なパッケージをインストール
1. 仮想環境へのパッケージの移植  (uv addが機能しない場合)
`env_name\Scripts\activate`: 仮想環境をactivate する　デフォルトの名前は.venv  
`uv pip install -r pyproject.toml` : 仮想環境への移植  
`deactivate`: 仮想環境を退出  
  
  
現在のパッケージ情報は、`pyproject.toml`に記載されています。  

## VSCodeへの仮想環境の追加  
VSCodeやCursorで仮想環境を使用するためには、仮想環境内のPythonをインタープリタに設定する必要があります。  
1. `Shift+Ctrl+P`でコマンドパレットを起動   
1. `Pythonインタープリタの選択`を選択  
1. `インタープリタ－パスを入力`を選択
1. 仮想環境内のpython.exeを登録。例：`<project_root_dir>\<project_name>\.venv\Scripts\python.exe`  
  
これで、VSCodeで仮想環境のカーネルを選択可能。  
VSCode内で.ipynbを使用したい場合は以下を実行してください。  
`uv pip install ipython ipykernel jupyter`  
`ipython kernel install`  


## Pythonのバージョン管理関係のコマンド  
`uv python install`: Python バージョンをインストールします。  
`uv python list`: 利用可能な Python バージョンを表示します。  
`uv python find`: インストールされている Python バージョンを見つけます。  
`uv python pin`: 特定の Python バージョンを使用するために現在のプロジェクトを固定します。  
`uv python uninstall`: Python バージョンをアンインストールします。 

## プロジェクト管理コマンド   

* プロジェクトの立ち上げ  
`uv init new_project_name`: 新規プロジェクト作成  
`cd project_folder`: 既存フォルダをuvで管理する場合  
`uv init`  
  
* 各仮想環境で実行するコマンド類  
`uv add`: パッケージの追加  
`uv remove`: パッケージの削除  
`uv run`: .pyファイルの実行  
`uv tree`: パッケージの依存関係表示  
`uv build`: プロジェクトを配布アーカイブにビルド  
`uv publish`: プロジェクトをパッケージ インデックスに公開  
  
**※**`pip install ~~`**も使えますが、addが使用できない場合**に使います。  

## ユーティリティ
`uv cache clean`: キャッシュの削除  
`uv sync --reinstall`: `pyproject.toml`に記載された情報を元に、パッケージ関係の再構築。  
`uv add git+https://github.com/encode/httpx`: githubからパッケージをインストールする方法。`git+`の後にgithubのURL  


