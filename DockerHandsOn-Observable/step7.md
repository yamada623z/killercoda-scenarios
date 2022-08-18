# prometheusのコンフィグ設定#2

prometheusは、ポート9090で使用可能なUIを備えたdockerコンテナとして実行されます。prometheusは設定を使用してターゲットをスクレイプし、メトリクスを収集して保存した後、ダッシュボード、グラフ化、アラートを可能にするAPIを介して利用できるようにします。（「targets:」に「, '127.0.0.1:9323'」を追加してください。）  

\# `vi prometheus.yml`{{execute}}

```yaml
global:
scrape_interval:     15s
evaluation_interval: 15s

scrape_configs:
  - job_name: 'prometheus’
    static_configs:
      - targets: ['127.0.0.1:9090', '127.0.0.1:9100', '127.0.0.1:9323']
        labels:
          group: 'prometheus'
```

- 9090ポートはprometheusそのものです。 prometheusは、内部の指標とパフォーマンスに関連する情報を公開しています。  

- 9100ポートは、Node Exporter Prometheusプロセスです。 これにより、ディスクスペース、メモリ、CPU使用率などのノードに関する情報が公開されます。  

- 9323ポートは、公開されたばかりのDocker Metricsポートです。  
