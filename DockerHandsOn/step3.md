# コンテナの起動（docker run）

Docker CLIには、Dockerイメージに基づいてコンテナを起動する「**run**」というコマンドがあります。 書式は「**docker run** *options image-name*」です。  

デフォルトでは、Dockerはフォアグラウンドでコマンドを実行します。 バックグラウンドで実行するには、オプション「**-d**」を指定する必要があります。  

$ `docker run -d nginx`{{execute}}  

（表示例）

```text
Unable to find image 'nginx:latest' locally  
latest: Pulling from library/nginx  
d121f8d1c412: Pull complete  
66a200539fd6: Pull complete  
e9738820db15: Pull complete  
d74ea5811e8a: Pull complete  
ffdacbba6928: Pull complete  
Digest: sha256:fc66cdef5ca33809823182c9c5d72ea86fd2cef7713cf3363e1a0b12a5d77500  
Status: Downloaded newer image for nginx:latest  
D6ae8a871e8f6c7f93da21fd9fd79670a82e0a7a6f119ea3e94a29f96ac0439b  
```

デフォルトでは、Dockerは利用可能な最新バージョンを実行します。 特定のバージョンが必要な場合は、タグとして指定できます。たとえば、バージョン1.17.7は「**docker run -d** *nginx:1.17.7*」になります。  
