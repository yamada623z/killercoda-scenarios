# prometheusのスタート#2  

prometheusは、ポート9090で使用可能なUIを備えたdockerコンテナとして実行できます。prometheusは、ダッシュボード、グラフ化、アラートを可能にするAPIを介して使用できるようにします。その前に、構成を使用してターゲットから周期的にメトリックを収集して保存します。  

Step3で起動したprometheusを削除し、Step4で起動したPrometheus Node Exporterを再起動します。  

\# `docker rm prometheus-server`{{execute}}  

\# `docker restart prometheus`{{execute}}  

コマンドは、prometheusを設定の通りにコンテナを起動します。  

\# `docker run -d --net=host -v /root/prometheus.yml:/etc/prometheus/prometheus.yml --name prometheus-server prom/prometheus`{{execute}}  
