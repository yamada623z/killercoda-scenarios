# kubeadmのインストール（workerノード）

**※このステップは本レッスンでは必要ありません。**

## 【workerノードで実施】  

⑥apt-transport-httpsのインストールは念のため実施します。  

\# `apt update && apt install -y apt-transport-https`  

⑦kubernetes のキーとリポジトリを登録します。  

\# `curl -s https://packages.cloud.google.com/apt/doc/aptkey.gpg | apt-key add -`{{copy}}  

\# `apt-add-repository “deb http://apt.kubernetes.io/kubernetes-xenial main"`  

⑧スワップをオフにします。  
*※恒久的にswapoffにする必要があります。（/etc/fstabのswap行をコメントアウトします）*  

\# `swapoff -a`  

⑨**kubeadm**をインストールします。  

\# `apt update`  
\# `apt install -y kubeadm`  
