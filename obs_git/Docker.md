
|状況|実行するコマンド|
|---|---|
|ライブラリを追加した|`docker compose build`|
|コードを編集した|`docker compose up`|
|イメージごと再構築したい|`docker compose build --no-cache`|
|前回の実行をもう一度|`docker compose up`|


|概念|説明|
|---|---|
|`Dockerfile`|Pythonやライブラリをどう入れるかを定義する|
|`docker compose build`|Dockerfile を元にイメージ（環境）を構築する|
|`.dockerignore`|コピー不要なファイルを除外（`.git`, `__pycache__`など）|



|概念|説明|
|---|---|
|`volumes`|ホスト側（Windows）のフォルダと、Dockerコンテナ内を同期させる|
|`docker-compose.yml` の `- .:/app`|現在のディレクトリ全体を `/app` にマウントする|

📂 たとえば `Docker_test/data/` に CSV を入れれば、コンテナ内から `/app/data/xxx.csv` で読めます。

**追加する知識：**

|概念|説明|
|---|---|
|`jupyterlab`|Docker上でJupyter起動するにはこれが便利|
|`ports`|`-p 8888:8888` でブラウザからアクセス可能にする|
|`.ipynb` ファイルは `volumes` で共有しておけば編集・保存もOK|

`output/` フォルダを作ってそこに保存すれば、ホストから閲覧可能

docker compose run
docker compose run dev python -m ipykernel install --user --name docker-dev --display-name "Python (Docker)"

上記を初回のみ実行




後回し。