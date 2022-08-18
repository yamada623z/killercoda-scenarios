# manifestファイル（yaml）作成

## 【masterノードで実施（controlplane:Tab1）】  

Podを作成するためにmanifestファイル（nginxphp_pod.yaml）を作成し、Podを作成します。

①manifestファイル（nginxphp_pod.yaml）のコンテナイメージ名（二箇所）を編集します。（「xxx.xxx.xxx.xxx」はregistryノードのIPアドレスを指定します。*但し、本レッスンではmasterノードのIPアドレス（172.30.1.2）を指定します。*）  

$ `cd`{{execute}}  

$ `vi nginxphp_pod.yaml`{{execute}}  

```yaml  
apiVersion: v1
kind: Service           #サービスを定義
metadata:
  name: nginx-service   #Serviceリソース名
  labels:
    app: nginx          #対象のアプリケーション名
spec:
  type: NodePort        #ノードのポートでアクセスを受付け
  ports:
  - port: 80            #クラスタ内仮想IPのポート番号
    targetPort: 80      #コンテナのポート番号
    nodePort: 31001     #受付けノードのポート番号
    protocol: TCP       #TCPプロトコル
  selector:
    app: nginx          #割当てポートのアプリケーション名
---
apiVersion: apps/v1
kind: Deployment        #実行方法を定義
metadata:
  name: nginx           #Deploymentリソース名
spec:
  replicas: 2           #生成するPod数
  selector:
    matchLabels:
      app: nginx        #Deploymentリソースで管理するPodのラベル
  template:
    metadata:
      labels:
        app: nginx      #アプリケーション名
    spec:               #Podに用いるコンテナの定義
      containers:
      - name: nginx     #コンテナ名
        image: xxx.xxx.xxx.xxx:5000/mynginx:1.0
        ports:
        - containerPort: 80     #コンテナにアクセスされるポート番号
      - name: phpfpm    #コンテナ名
        image: xxx.xxx.xxx.xxx:5000/myphpfpm:1.0
        ports:
        - containerPort: 9000   #コンテナにアクセスされるポート番号
```  
