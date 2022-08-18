# コンテナ状態の確認（docker ps）

「**docker ps**」コマンドは、実行中のすべてのコンテナ、コンテナの開始に使用されたイメージ、および稼働時間を一覧表示します。このコマンドは、個々のコンテナに関する情報を見つけるために使用できる *コンテナID（container-id）* と *フレンドリ名（friendly-name）* も表示します。  

$ `docker ps`{{execute}}  

（表示例）  

```text  
CONTAINER ID  IMAGE  COMMAND  CREATED  STATUS  PORTS  NAMES  
d6ae8a871e8f  nginx  "/docker-entrypoint.…"  3 minutes ago  Up 3 minutes  80/tcp  elegant_thompson
```  

（説明）  

「 *d6ae8a871e8f* は コンテナID（container-id） です。  
「 *elegant_thompson* 」は フレンドリ名（friendly-name） です。  
