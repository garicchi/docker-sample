FROM python:3.5.6-alpine

WORKDIR /

# 依存パッケージを記述したファイルを最初にコピーする
COPY ./requirements.txt /py/requirements.txt

# 依存パッケージをインストール
RUN pip install -r /py/requirements.txt

ENV PYTHONPATH /py

# ソースコードをコピー
# ソスコードを編集してもパッケージ再インストールは走らない
COPY ./app /py/app

WORKDIR /py

ENTRYPOINT python /py/app/main.py
