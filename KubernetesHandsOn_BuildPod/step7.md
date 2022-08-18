# kubernetesクラスターへのpodの作成

Step6で作成したmanifestファイルで、kubernetesクラスターへPodを作成します。  

## 【masterノードで実施（controlplane:Tab1）】  

①下記のコマンドでkubernetesクラスターへPodを作成します。  

$ `kubectl apply -f nginxphp_pod.yaml`{{execute}}  

②Podの起動状況を確認します。  
（Podの状態（STATUS）が、下記の様に実行中（Running）となるまで、下記のコマンドを数回繰り返してください。）

$ `kubectl get pods`{{execute}}  

（表示例）  

```text  
$ kubectl get pods
NAME                     READY   STATUS    RESTARTS   AGE
nginx-74885b6fdd-4p8ql   2/2     Running   0          13s
nginx-74885b6fdd-mftm9   2/2     Running   0          13s
```  
