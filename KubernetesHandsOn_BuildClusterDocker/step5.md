# 環境設定とdockerのインストール（workerノード）  

**※このステップは本レッスンでは必要ありません。**  

本レッスンでは必要ありませんが、Kubernetesクラスター環境を動作させる実workerノードでは下記の手順（①~⑤）で**docker**をインストール必要があります。

## 【workerノードで実施】  

①ホスト名の変更します。*（※”_”,”-”はホスト名に使えないので注意です。）*  

$ `sudo hostnamectl set-hostname node01`  

②/etc/hostsファイルの変更します。

$ `sudo vi /etc/hosts`  

```text
127.0.0.1   localhost   node01
```

③rootにユーザを切り替えます。  

\# `sudo -s`  

④dockerをインストールします。（ubuntuのリポジトリのものを使用します。）  

\# `apt install docker.io`  

⑤システム起動時に起動するように設定します。  

\# `systemctl enable docker`  
