# 環境設定とcontainerdのインストール（masterノード）  

**※このステップは本レッスンでは必要ありません。**  

本レッスンでは必要ありませんが、Kubernetesクラスター環境を動作させる実masterノード（controlplane）では下記の手順（①~⑧）で**containerd**をインストール必要があります。  

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

④「br_netfilter」モジュールがロードされていることを確認します。  

$ `lsmod | grep br_netfilter`

**（表示例）**  

```text
br_netfilter           28672  0
bridge                176128  1 br_netfilter
```

※明示的にロードするには「modprobe br_netfilter」を実行します。  

⑤iptablesがブリッジを通過するトラフィックを処理できるように net.bridge.bridge-nf-call-iptablesをsysctlの設定ファイルで1に設定します。  

$ `cat <<EOF > /etc/sysctl.d/k8s.conf`

```text
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
```

$ `sysctl --system`  

⑥システムのiptablesツールがnftablesバックエンドを使用している場合、iptablesツールをレガシーモードに切り替える必要があります。  

- レガシーバイナリがインストールされていることを確認します。  
  $ `sudo apt-get install -y iptables arptables ebtables`  
- レガシーバージョンに切り替えます。  
  $ `sudo update-alternatives --set iptables /usr/sbin/iptables-legacy`  
  $ `sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy`  
  $ `sudo update-alternatives --set arptables /usr/sbin/arptables-legacy`  
  $ `sudo update-alternatives --set ebtables /usr/sbin/ebtables-legacy`  

⑦containerdをインストールするために必要な設定を追加します。  
$ `cat > /etc/modules-load.d/containerd.conf <<EOF`

```text
overlay
br_netfilter
EOF
```  

$ `modprobe overlay`  

$ `modprobe br_netfilter`  

必要なカーネルパラメータの設定をします。これらの設定値は再起動後も永続化されます。  
$ `cat > /etc/sysctl.d/99-kubernetes-cri.conf <<EOF`

```text
net.bridge.bridge-nf-call-iptables  = 1
net.ipv4.ip_forward                 = 1
net.bridge.bridge-nf-call-ip6tables = 1
EOF
```  

$ `sysctl --system`  

⑧containerdをインストールします。  

- HTTPS越しのリポジトリの使用をaptに許可するために、パッケージをインストールします。  
  $ `apt-get update && apt-get install -y apt-transport-https ca-certificates curl software-properties-common`{{copy}}  

- Docker公式のGPG鍵を追加します。  
  $ `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -`{{copy}}  

- Dockerのaptリポジトリの追加します。  

  $ `add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"`{{copy}}  

- containerdのインストールします。  
  $ `apt-get update && apt-get install -y containerd.io`  
  ※「*** config.toml (Y/I/N/O/D/Z) [default=N] ? 」はdefaultを選択します。  

- containerdの設定します。  
  $ `mkdir -p /etc/containerd`  

- containerdの再起動します。  
  $ `systemctl restart containerd`  
