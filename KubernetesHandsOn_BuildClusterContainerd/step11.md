# ダッシュボードのアクセス方法

## 【masterノード（controlplane）で実施】  

ダッシュボードへのアクセス方法を3つ説明します。１～２は自ノード（localhost）からのアクセス方法、３は外部ノードからのアクセスを可能とする方法です。  
**今回は、１の方法でアクセスを試みます。** ２～３は方法があることを理解しておいてください。  

### **１．kubectl port-forwardコマンドによる方法（localhostからのアクセス）**

①はじめにダッシュボードのPodが正常に動作している（Running）ことを確認します。  
$ `kubectl get pods -n kubernetes-dashboard`{{execute}}  

（表示例）  

```text
NAME                                         READY   STATUS    RESTARTS   AGE
dashboard-metrics-scraper-747c5cf959-h88ms   1/1     Running   0          3m50s
kubernetes-dashboard-6696687cd9-ffstd        1/1     Running   0          3m50s
```

②「**kubectl port-forward**」を起動し、ブラウザでアクセス出来るようにします。  
$ `kubectl port-forward service/kubernetes-dashboard -n kubernetes-dashboard --address 0.0.0.0 9090:9090`{{execute}}  

③ブラウザでは下記のURLを指定します。  
`http://localhost:9090`  

④ページ末に記載されている「 **KillercodaのWebアクセス方法** 」でダッシュボードを表示させてください。  

### **２．kubectl proxyコマンドによる方法（localhostからのアクセス）**  

**（今回は実施しないでください。）**  

①「**kubectl proxy**」を起動し、ブラウザでアクセス出来るようにします。  
$ `kubectl proxy`  

（表示例）  

```text
Starting to serve on 127.0.0.1:8001
```

②ブラウザでは下記のURLを指定します。  
`http://localhost:8001/api/v1/namespaces/kubesystem/
services/https:kubernetes-dashboard:/proxy/`  

### **３．外部ノードからのアクセスを可能とする方法**

**（今回は実施しないでください。）**  

masterノードのポートを使用して、外部ノードからアクセス出来るようにします。  

①Podの状態からダッシュボードのみを表示します。  
$ `kubectl get pods --all-namespaces | grep dashboard`{{copy}}  

②ダッシュボードの定義ファイルを編集します。  
$ `kubectl -n kubernetes-dashboard edit service kubernetes-dashboard`  

```yaml
（省略）
spec:
（省略）
  ports:
  - port: 443
    protocol: TCP
    targetPort: 8443
    nodePort: 9090 <- nodePortを追加します（任意のポートを指定します。 例：9090）
（省略）
  type: ClusterIP <- この行を削除し、下記の行「type: NodePort」を追加します。
  type: NodePort
（省略）
```

③サービスの状態を取得し、確認します。  

$ `kubectl get svc --all-namespaces`  

（表示例）

```text
kubernetes-dashboard  kubernetes-dashboard    NodePort    yyy.yyy.yyy.yyy  <none>      443:9090/TCP   16m
```

④ブラウザでは下記のURLを指定します。  
（例：「xxx.xxx.xxx.xxx」はmasterノードのIPアドレスです。）  
`https://xxx.xxx.xxx.xxx:9090`  

> **KillercodaのWebアクセス方法：**  
> ①ターミナルペインの「**Tab1**」「**＋**」のタグの並びの一番右にある「**三**」をクリックする。  
> ②表示されるドロップリストから「**Traffic / Ports**」をクリックする。
> ③新しいブラウザタブ「**Traffic Port Accessor**」が表示されたら、「**Host 1**」「**Custom Ports**」の下のボックスに「**9090**」を入力し、「**Access**」をクリックします。  

（表示例）  
![DashBoard Image](https://github.com/yamada623z/scenario-image/raw/main/KubernetesHandsOn_BuildCluster/Step11.jpg)  
