# dockerイメージのプライベートレジストリへの登録

## 【masterノードで実施（controlplane:Tab1）】  

Podの作成に必要なコンテナイメージをプライベートレジストリにpushします。

①プライベートレジストリにpushする為にコンテナイメージの名前を変更します。（「xxx.xxx.xxx.xxx」はregistryノードのIPアドレスを指定します。*但し、本レッスンではmasterノードのIPアドレス（172.30.1.2）を指定します。*）  

$ `docker tag mynginx:1.0 xxx.xxx.xxx.xxx:5000/mynginx:1.0`  

$ `docker tag myphpfpm:1.0 xxx.xxx.xxx.xxx:5000/myphpfpm:1.0`  

②コンテナイメージをレジストリにpushします。  

$ `docker push xxx.xxx.xxx.xxx:5000/mynginx:1.0`  

$ `docker push xxx.xxx.xxx.xxx:5000/myphpfpm:1.0`  

③Step3でアクセスした、プライベートレジストリのWeb-UIをリロードすると、プライベートレジストリにコンテナイメージがpushされたことが確認できます。  

（表示例）  
![Registry Image](https://github.com/yamada623z/scenario-image/raw/main/KubernetesHandsOn_BuildPod/Registry_2.jpg)  
