# Dockerホストの視覚化  

Weave Scopeコンテナが起動すると、ポート4040でUIにアクセスできます。

`https://localhost:4040`

> **KillercodaのWebアクセス方法：**  
> ①ターミナルペインの「**Tab1**」「**＋**」のタグの並びの一番右にある「**三**」をクリックする。  
> ②表示されるドロップリストから「**Traffic / Ports**」をクリックする。
> ③新しいブラウザタブ「**Traffic Port Accessor**」が表示されたら、「**Custom Ports**」の下のボックスに「**4040**」を入力し、「**Access**」をクリックします。  

（表示例）
![Scope farst](https://github.com/yamada623z/scenario-image/raw/main/ObservableHandsOn/Step13-1.jpg)  

新しいコンテナーが起動されると、Scopeはライブアーキテクチャ（リアルタイムな機能仕様）を反映するように自動的に更新されます。  

\# `docker run -d --link redis:redis katacoda/redis-node-docker-example`{{execute}}  

追加のフロントエンドコンテナを起動して結果を確認してください。  

（表示例）  
![Scope container plus](https://github.com/yamada623z/scenario-image/raw/main/ObservableHandsOn/Step13-2.jpg)  
