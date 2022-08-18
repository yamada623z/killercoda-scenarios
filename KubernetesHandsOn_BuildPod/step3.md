# プライベートレジストリのWeb-UIの構築

プライベートレジストリで管理されているコンテナイメージの参照・削除などはWeb-UIを構築することで可能となります。  

**【registryノードで実施】※本レッスンではmasterノード（controlplane:Tab1）で実施します。**  

①プライベートレジストリのWeb-UIのコンテナイメージをパブリックレジストリからpullします。  
$ `docker pull hyper/docker-registry-web`{{execute}}  

②パラメータを指定して、Web-UIのコンテナイメージを起動します。（「xxx.xxx.xxx.xxx」はregistryノードのIPアドレスを指定します。*※但し、本レッスンではmasterノードのIPアドレス（172.30.1.2）を指定してください。*）  

$ `docker run -d -p 8080:8080 -e REGISTRY_URL=http://xxx.xxx.xxx.xxx:5000/v2 -e REGISTRY_NAME=xxx.xxx.xxx.xxx:5000 -e REGISTRY_READONLY=false hyper/docker-registry-web:latest`  

③ブラウザからアクセスする場合のURLは下記の通りです。  

`http://xxx.xxx.xxx.xxx:8080`  

> **KillercodaのWebアクセス方法：**  
> ①ターミナルペインの「**Tab1**」「**Tab2**」「**＋**」のタグの並びの一番右にある「**三**」をクリックする。  
> ②表示されるドロップリストから「**Traffic / Ports**」をクリックする。
> ③新しいブラウザタブ「**Traffic Port Accessor**」が表示されたら、「**Host 1**」「**Common Ports**」の下の「**8080**」をクリックします。  

（表示例）
![Registry Image](https://github.com/yamada623z/scenario-image/raw/main/KubernetesHandsOn_BuildPod/Registry.jpg)  
