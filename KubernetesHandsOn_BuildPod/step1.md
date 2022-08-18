# 準備

このステップは、Killercodaでkubernetesのクラスターを構築・利用するための手順です。実ノードでは、kubernetesのクラスターをあらかじめ構築しておく必要があります。  

※手順を進める前に、新たにターミナル「**Tab2**」を生成して workerノード（node01）のターミナルを準備します。  
> **Killercodaのターミナルの生成方法：**  
> ①ターミナルペインの「**Tab1**」「**＋**」のタグの「**＋**」をクリックします。  
> ②しばらくするとターミナルペインの「**Tab1**」「**＋**」のタグの並びに「**Tab2**」が出現するので、それをクリックします。  

新たにターミナル「Tab2」から下記のコマンドで workerノード（node01）にログインしておきます。

$ `ssh 172.30.2.2`{{execute}}  

## 【masterノードで実施（controlplane:Tab1）①】  

①rootにユーザを切り替えます。  

$ `sudo -s`{{execute}}  

③dockerでプライベートレジストリを利用できるようにするため、「/etc/docker/daemon.json」に「"insecure-registries"」の行を追加します。（「xxx.xxx.xxx.xxx」はregistryノードのIPアドレスを指定します。*※但し、本レッスンではmasterノードのIPアドレス（172.30.1.2）を指定してください。* ）  

\# `vi /etc/docker/daemon.json`{{execute}}  

```json
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "storage-driver": "overlay2",
  "registry-mirrors": ["https://mirror.gcr.io","https://docker-mirror.killer.sh"],
  "insecure-registries": ["http://xxx.xxx.xxx.xxx:5000"],
  "mtu": 1454
}
```  

⑤dockerを再起動します。（「daemon.json」ファイルの反映）  

\# `systemctl restart docker`{{execute}}  

（一般ユーザに戻します）  

\# `exit`{{execute}}  

⑥ノード状態を確認し、クラスターの正常性を確認します。  

$ `kubectl get nodes`{{execute}}  

（表示例）  

```text  
$ kubectl get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   89d   v1.24.0
node01         Ready    <none>          89d   v1.24.0
```

⑦ハンズオンに必要なファイルはカレントのフォルダにあります。確認してください。  

## 【masterノードで実施（controlplane:Tab1）②】  

$ `ls -la`{{execute}}  

（表示例）  

```text  
-rw-r--r--  1 root root  1135 Apr 27 02:09 default.conf
-rw-r--r--  1 root root    32 Apr 27 02:09 index.php
-rw-r--r--  1 root root   655 Apr 27 02:09 nginxphp_pod.yaml
-rw-r--r--  1 root root    95 Apr 27 02:09 php-fpm.conf
-rw-r--r--  1 root root 72763 Apr 27 02:09 php.ini
-rw-r--r--  1 root root    37 Apr 27 02:09 test.php
-rw-r--r--  1 root root   217 Apr 27 02:09 www.conf
```

（ファイルの説明）  
*default.conf：*  
nginxの設定ファイルです。httpの待ち受けポートやphpとのインタフェース、始めに検出するファイルの位置などが設定されています。  

*index.php：*  
phpファイルです。phpの情報を表示させます。  

*nginxphp_pod.yaml：*  
nginx＋phpを連携するようにPodを作成するためのmanifestファイルです。（Step6で説明します）  

*php-fpm.conf・php.ini・www.conf：*  
phpの動作に必要な設定ファイルです。  

*test.php：*  
phpファイルです。現在、アクセス中のプロセス（Pod）の名前を表示させます。  
