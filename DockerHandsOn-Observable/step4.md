# Node Exporterの実行#1  

ノードに関連するメトリックを収集するには、Prometheus Node Exporterを実行する必要があります。 prometheusには、PostgresやMySQLなどの特定のシステムのメトリックを出力するように設計された多くのエクスポーターがあります。  

Node Exporterコンテナを起動します。 ホストの/procおよび/sysディレクトリをマウントすることにより、コンテナはレポートに必要な情報にアクセスできるようになります。  

\# `docker run -d -v "/proc:/host/proc" -v "/sys:/host/sys" -v "/:/rootfs" --net="host" --name=prometheus quay.io/prometheus/node-exporter:v0.13.0 -collector.procfs /host/proc -collector.sysfs /host/sys -collector.filesystem.ignored-mount-points "^/(sys|proc|dev|host|etc)($|/)"`{{execute}}  

- 「-collector.xxx」は、それぞれ情報を取得しに行く先のパスを指定します。

- 「-collector.filesystem.ignored-mount-points」は、無視するファイルシステムのマウントポイントを正規表現で指定します。

生のメトリックを表示することに興味がある場合は、下記のコマンドで表示できます。

\# `curl localhost:9100/metrics`{{execute}}  
