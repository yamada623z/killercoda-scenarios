# アプリケーションのデプロイ  

まず、2つのリンクコンテナを起動して、Webサイト/データベースのアーキテクチャをデモします。  

\# `docker run -d --name redis redis`{{execute}}  
\# `docker run -d --link redis:redis katacoda/redis-node-docker-example`{{execute}}  
