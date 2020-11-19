
# ABOUT python

## Install python

``` Dockerfile
FROM alpine:latest
WORKDIR /src
RUN apk add python3
```

Dockerfileは設計図。環境の内容が記載されている。

FROMはベースとなるイメージを指定する。このイメージはDocker Hubにあるので余裕が出来たらいつか見てみて。

WORKDIRはコマンドを実行するディレクトリを指定する。コンテナに入った時はここに入った状態でスタートする。

<hr>

``` command line
docker build -t python .
```

実行する際はDockerfileがあるディレクトリで行う。

buildはDockerfileからイメージを作成する際に使われるコマンド。

-tオプションは生成するイメージに名前をつけている。

最後のドットはDockerfileがあるディレクトリの場所を指している。

<hr>

``` command line
docker run --name py -v (pythonのソースを置くディレクトリ):/src -it python
```

実行はどこのディレクトリでもいい。

runはイメージからコンテナを生成する際に使われるコマンド。

--name はコンテナに名前をつけるコマンド。pyとつけている。

-v はメインOSのディレクトリとコンテナのディレクトリをマウントしている。平たく言うと紐づけ。中身を同じにするって認識でいい。コロンを境に左がメインOSのディレクトリ。右がコンテナのディレクトリ。どちらも絶対パスで書かなきゃいけないっぽい。

-it はイメージを指定している。さっき生成したpythonイメージを使用している。

<hr>

これでコンテナに入っているはず。

コンテナから抜け出すときはexitを入力。

<hr>

runコマンドはコンテナを生成するコマンド。

では生成したコンテナにはどうやって入るか？

``` command line
docker start py
docker exec -it py /bin/sh
```

で入る。コンテナに入る前に起動してあげなければならない。それがstartコマンド。

exec を使うとコンテナの中で指定したコマンドを実行する。

-it は使用するコンテナ。

最後の/bin/shは実行するコマンド。ここではシェルを起動している。

<hr>

## 基本コマンド

```
docker stop [container] # 指定した起動しているコンテナを停止する。
docker ps               # 起動しているコンテナをリストアップ
docker ps -a            # コンテナすべてをリストアップ
docker images           # イメージすべてをリストアップ
docker rm [container]   # 指定したコンテナを削除。起動中だと消せない。
docker rmi [image]      # 指定したイメージを削除する。
```

ここのcontainerやimageはそれの名前でもIDでも指定できる。
たまにイメージはIDしか受け付けない時がある。
というかFROMで引っ張ってきたベースのやつがそう。

**余談**

コンテナの使い方として、コンテナを残さずに、使用する度新しいコンテナを作成するのを推奨している人たちもいる。
が、別に好みの問題だと思ってる。