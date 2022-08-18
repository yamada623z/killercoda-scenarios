# Dockerfile利用ビルド（コンテナイメージ生成）

Dockerイメージを作成する「**docker build**」コマンドは、「Dockerfile」ファイルの上から順番に処理が実行されます。  

（書式）  
**docker build** *[-t ｛イメージ名｝[:｛タグ名｝]]｛Dockerfileのあるディレクトリ｝*  

「Dockerfile」ファイルが作成できたら、「**docker build**」コマンドでDockerコンテナーの起動、構成、Dockerイメージの作成まで一気に実行します。  
「*-t*」オプションは作成するDockerイメージのイメージ名およびタグ名を指定します。  

$ `docker build -t webserver-image:v1 .`{{execute}}  

カレントディレクトリに「Dockerfile」が存在するため、Dockerfileのあるディレクトリは「*.*」を指定しています。  

（表示例）  

```text
Sending build context to Docker daemon  3.072kB
Step 1/2 : FROM nginx:alpine
alpine: Pulling from library/nginx
df20fa9351a1: Pull complete
091a6e3499e9: Pull complete
b4bea01b9731: Pull complete
62c992d61d2c: Pull complete
b675ffa804eb: Pull complete
Digest: sha256:5fcbe9a6b09b6525651d1e5d5a2df373eec1a13c75f0eaa724a369f43ce589f4
Status: Downloaded newer image for nginx:alpine ---> bd53a8aa5ac9
Step 2/2 : COPY ./index.html /usr/share/nginx/html ---> 0ba8ead98d17
Successfully built 0ba8ead98d17
Successfully tagged webserver-image:v1
```
