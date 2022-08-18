# Dockerfile利用ビルド（FROM）

今回、ベースイメージは「nginx」というウェブサーバーのアプリケーションです。  

まず、コンテナにコピーされる「index.html」ファイルを作成します。（説明は次項参照）  

$ `vi index.html`{{execute}}  

`
<h1>Hello World</h1>
`

次に、Dockerfileを作成します。「Dockerfile」ファイルは、プログラムのビルドでよく利用されるmakeツールの「Makefile」ファイルと同様に、Dockerコンテナーの構成内容をまとめて記述するシンプルなテキスト形式のファイルです。1行につき1つの操作を **｛命令｝** と **｛引数｝** でスペース区切りで記述します。  

$ `vi Dockerfile`{{execute}}  

`
FROM nginx:alpine
COPY ./index.html /usr/share/nginx/html
`

**FROM**命令は、ビルドするDockerイメージに対しての ベースイメージ を指定するものです。  
