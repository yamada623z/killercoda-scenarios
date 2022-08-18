# クラスターの生成（kubeadm init）（masterノード（controlplane））  

**※このステップは本レッスンでは必要ありません。**  

①kubernetesの構築を行います。
（使用するCNIによって「--pod-network-cidr」の指定が必要です。）  

$ `kubeadm init`  

（以下はkubeadm init実行後の表示例）

```text
Your Kubernetes master has initialized successfully!
```

「Kubernetesマスターが正常に初期化されました！」  

```text
 To start using your cluster, you need to run the following as a regular user:
 ```

「クラスターの使用を開始するには、通常のユーザーとして次を実行する必要があります。」  
*※ 下記のコマンドを表示通りに実行します。（②で実施します。）*

```text
    mkdir -p $HOME/.kube
    sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
    sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
  
```text
 You should now deploy a pod network to the cluster.↲
 Run "kubectl apply -f [podnetwork].yaml" with one of the options listed
    https://kubernetes.io/docs/concepts/clusteradministration/addons/
```

「ここで、ポッドネットワークをクラスターにデプロイする必要があります」  
*※ CNI（Contena Network Intarface）のインストールします（Step4で実施します。）*

```text
You can now join any number of machines by running the following on each node
as root:
```

「各ノードで次を実行することで、任意の数のマシンに参加できるようになりました。」「ルートで：」  
*※workerノードを追加する際には、下記の**kubeadm join**を実施します。（Step7で実施します。）*  

```text
kubeadm join xxx.xxx.xxx.xxx:6443 --token
xxxxxx.xxxxxxxxxxxxx --discovery-token-ca-cert-hash sha256:xxxxxxx
```  

②「kubeadm init」コマンドの出力で実施を促された部分を実施します。  

$ `mkdir -p $HOME/.kube`  

$ `sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config`{{copy}}  

$ `sudo chown $(id -u):$(id -g) $HOME/.kube/config`  
