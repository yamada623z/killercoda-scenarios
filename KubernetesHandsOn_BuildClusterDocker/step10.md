# ダッシュボードの実装

## 【masterノード（controlplane）で実施】  

①下記の手順でダッシュボードへのアクセスの為の証明書を作成します。  

$ `mkdir $HOME/certs`{{execute}}  

$ `cd $HOME/certs`{{execute}}  

$ `openssl genrsa 2048 > dashboard.key`{{execute}}  

$ `openssl req -new -key dashboard.key > dashboard.csr`{{execute}}  
（「Country Name」のみ「JP」を入力し、その後はEnterキーで何も入れません。）

$ `openssl x509 -days 3650 -req -signkey dashboard.key < dashboard.csr > dashboard.crt`{{execute}}  

②作成した証明書からsecretを作ります。  

$ `kubectl create secret generic kubernetes-dashboardcerts --from-file=$HOME/certs -n kube-system`{{execute}}  

（表示例）

```text
secret/kubernetes-dashboard-certs created
```  

③ダッシュボードをPodとして、クラスターにインストールします。  
今回は、ダッシュボードのマニフェストファイルをホームディレクトリに配置済みなのでホームディレクトリに移動します。  
$ `cd`{{execute}}  

④マニフェストファイルを指定してダッシュボードをインストールします。  
$ `kubectl apply -f recommended.yaml`{{execute}}  

*※本来は下記の通り、直接ダッシュボードをインストールする為のマニフェストファイルを指定しますが、このレッスンではカレントに用意したマニフェストファイルでダッシュボードをインストールします。*  

$ `kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.6.0/aio/deploy/recommended.yaml`  

⑤クラスターの状況を確認します。  

$ `kubectl cluster-info`{{execute}}  

（表示）

```text
Kubernetes controlplane is running at https://xxx.xxx.xxx.xxx:6443
CoreDNS is running at
https://xxx.xxx.xxx.xxx:6443/api/v1/namespaces/kubesystem/services/kube-dns:dns/proxy
```  
