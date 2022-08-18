# Node Exporterの実行#2

Docker Metricsエンドポイントは、dockerに関連する情報を返します。dockerホストでメトリックを収集するには、Prometheus Node Exporterを実行する必要があります。prometheusには、PostgresやMySQLなどの特定のシステムのメトリックを出力するように設計された多くのエクスポーターがあります。  

Node Exporterコンテナを起動します。 ホストの/procおよび/sysディレクトリをマウントすることにより、コンテナはレポートに必要な情報にアクセスできるようになります。  

生のメトリックを表示することに興味がある場合は、下記のコマンドで表示できます。  

\# `curl localhost:9100/metrics`{{execute}}
