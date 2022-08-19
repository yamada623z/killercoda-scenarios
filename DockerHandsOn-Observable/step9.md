# Node Exporterの実行#2

Docker Metricsエンドポイントは、dockerに関連する情報を返します。dockerホストでメトリックを収集するには、Prometheus Node Exporterを実行する必要があります。prometheusには、PostgresやMySQLなどの特定のシステムのメトリックを出力するように設計された多くのエクスポーターがあります。  

\# `docker run -d -v "/proc:/host/proc" -v "/sys:/host/sys" -v "/:/rootfs" --net="host" --name=prometheus quay.io/prometheus/node-exporter:v0.13.0 -collector.procfs /host/proc -collector.sysfs /host/sys -collector.filesystem.ignored-mount-points "^/(sys|proc|dev|host|etc)($|/)"`{{execute}}  

Node Exporterコンテナを起動します。 ホストの/procおよび/sysディレクトリをマウントすることにより、コンテナはレポートに必要な情報にアクセスできるようになります。  

生のメトリックを表示することに興味がある場合は、下記のコマンドで表示できます。  

\# `curl localhost:9100/metrics`{{execute}}
