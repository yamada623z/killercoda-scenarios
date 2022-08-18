# 観測値の表示#1

コンテナが起動すると、prometheusは構成の内部に基づいてデータを取得し、格納します。  

- ダッシュボードのグラフページにアクセスしてください。  
`https://localhost:9090`

> **KillercodaのWebアクセス方法：**  
> ①ターミナルペインの「**Tab1**」「**＋**」のタグの並びの一番右にある「**三**」をクリックする。  
> ②表示されるドロップリストから「**Traffic / Ports**」をクリックする。
> ③新しいブラウザタブ「**Traffic Port Accessor**」が表示されたら、「**Custom Ports**」の下のボックスに「**9090**」を入力し、「**Access**」をクリックします。  

**（表示例）**  
![Step5-1](https://github.com/yamada623z/scenario-image/raw/main/ObservableHandsOn/Step5-1.jpg)  

基になるメトリックをクエリ（補足：クエリ＝要求）してグラフを作成するには、ダッシュボードのグラフページにアクセスしてください。ここから、名前に基づいてさまざまなメトリックを照会できます。  

たとえば、「node_network_receive_bytes」をクエリすると、ディスクIOがどの程度アクティブであるかがわかります。 「node_cpu」を使用してクエリを実行すると、Docker Hosts CPU情報が出力されます。  

- クエリ（虫眼鏡マーク）に該当の言葉（「node_network_receive_bytes」等）を入力し、「Execute」→下部のタグ「Graph」をクリックする。

**（表示例）**  
node_network_receive_bytes  
![Step5-2](https://github.com/yamada623z/scenario-image/raw/main/ObservableHandsOn/Step5-2.jpg)  

node_cpu  
![Step5-3](https://github.com/yamada623z/scenario-image/raw/main/ObservableHandsOn/Step5-3.jpg)  
