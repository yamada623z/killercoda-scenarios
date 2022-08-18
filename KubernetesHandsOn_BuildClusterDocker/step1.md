# 環境設定とdockerのインストール（masterノード）

**※このステップは本レッスンでは必要ありません。**

本レッスンでは必要ありませんが、Kubernetesクラスター環境を動作させる実masterノード（controlplane）では下記の手順（①~⑤）で**docker**をインストール必要があります。  

## 【masterノード（controlplane）で実施】  

**kubeadm**はKubernetesクラスター環境を高速に作成する方法として**kubeadm init**と**kubeadm join**というコマンドを提供するツールです。Kubernetesのクラスターを立ち上げ、稼働させる上で最低限必要なものを提供します。  

①ホスト名の変更します。  

$ `sudo hostnamectl set-hostname controlplane`  

②/etc/hostsファイルの変更します。

$ `sudo vi /etc/hosts`  

```text
127.0.0.1   localhost   controlplane
```

③rootにユーザを切り替えます。  

\# `sudo -s`  

④dockerをインストールします。（ubuntuのリポジトリのものを使用。）  

\# `apt install docker.io`  

⑤システム起動時に起動するように設定します。  

\# `systemctl enable docker`  
