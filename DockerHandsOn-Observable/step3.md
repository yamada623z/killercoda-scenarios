# prometheusのスタート#1

prometheusは、ポート9090で使用可能なUIを備えたdockerコンテナとして実行できます。prometheusは、ダッシュボード、グラフ化、アラートを可能にするAPIを介して使用できるようにします。その前に、構成を使用してターゲットから周期的にメトリックを収集して保存します。  

\# `docker run -d --net=host -v /root/prometheus.yml:/etc/prometheus/prometheus.yml --name prometheus-server prom/prometheus`{{execute}}  

- コマンドは、prometheusを設定の通りにコンテナを起動します。「-v」（ファイルのマウント）ではStep2で作成したprometheusのコンフィグファイルを指定しています。  

- 「--net」では、コンテナがどのNetwork を使用するかを指定しています。

- prometheusを起動すると、ダッシュボードはポート9090で表示できます。  

> **KillercodaのWebアクセス方法：**  
> ①ターミナルペインの「**Tab1**」「**＋**」のタグの並びの一番右にある「**三**」をクリックする。  
> ②表示されるドロップリストから「**Traffic / Ports**」をクリックする。
> ③新しいブラウザタブ「**Traffic Port Accessor**」が表示されたら、「**Custom Ports**」の下のボックスに「**9090**」を入力し、「**Access**」をクリックします。  

（表示例）  
![Prometheus Start](https://github.com/yamada623z/scenario-image/raw/main/ObservableHandsOn/Prometeus-Start.jpg)  
