# コンテナの起動（ポート割付）

「**docker run**」コマンドは、DockerイメージからDockerコンテナを作成・実行します。  

（書式）  
**docker run** *[オプション] ｛イメージ名｝[:｛タグ名｝]*  

「*-d*」は、バックグラウンドでコンテナを実行するオプションです。  
*「-p ｛ホストのポート番号｝:｛コンテナーのポート番号｝」*のオプション指定で、Dockerホストマシンとポートマッピングを構成します。  
「nginx」は*80*番ポートを常時Listenするコンテナです。Dockerホストマシンとポートマッピングすることにより、Dockerホストマシンの*80*番ポートで入力を受け付けます。  

*｛イメージ名｝[:｛タグ名｝]* には、Step14で作成したコンテナイメージを指定します。  

$ `docker run -d -p 80:80 webserver-image:v1`{{execute}}  

（表示例）  

```text
67bcb99e625ac1b2f7193a27901b2ae61481ee9470bdea0a9c957d6ca8a39e08  
```
