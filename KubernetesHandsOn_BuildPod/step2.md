# プライベートレジストリの構築

プライベートレジストリ（ノンセキュア※）を構築します。自己で作成したコンテナイメージを格納し、Podをビルドする際に使用します。これを構築しないと、Podをスケールした際に新しいPodがイメージの無いノードでビルドされません。  
※外部公開をしないデバッグ環境での利用の為、セキュリティ無しで構築します。  

**【registryノードで実施】**  
*※本レッスンではmasterノード（controlplane:Tab1）で実施します。*  

①rootにユーザを切り替えます。  

$ `sudo -s`{{execute}}  

②dockerをインストールします。（ubuntuのリポジトリのものを使用します。）  
*（本レッスンでは不要です。）*  

\# `apt install docker.io`  

③システム起動時に起動するように設定します。  
*（本レッスンでは不要です。）*  

\# `systemctl enable docker`  

④registryノードのdockerでプライベートレジストリを利用できるようにするため、「/etc/docker/daemon.json」に「"insecure-registries"」の行を追加します。（「xxx.xxx.xxx.xxx」はregistryノードのIPアドレスを指定します。）  
*※但し、本レッスンではmasterノードでの構築のため、手順は不要です。（④～⑤は、Step1で実施済み）*  

\# `vi /etc/docker/daemon.json`  

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
*（本レッスンでは不要です。）*  

\# `systemctl restart docker`  

⑥docker上で動作させる「registry」の最新のコンテナイメージをpullする。

\# `docker pull registry`{{execute}}  

⑦「registry」のコンテナイメージをポート5000を指定して起動します。

\# `docker run -dit -p 5000:5000 --name registry -e REGISTRY_STORAGE_DELETE_ENABLED=true registry`{{execute}}  

## 【付録：プライベートレジストリの利用方法】

*（Step5で実際に利用します。ここでは、利用方法を覚えてください。）*  
※例として、作成するコンテナイメージを「mynginx:1.0」、registryノードのIPアドレスを「xxx.xxx.xxx.xxx」とします。

①コンテナイメージを作成します。  
$ `docker build --no-cache mynginx:1.0 .`  

②コンテナイメージの名前を変更します。  
$ `docker tag mynginx:1.0 xxx.xxx.xxx.xxx:5000/mynginx:1.0`  

③コンテナイメージをレジストリにpushします。  
$ `docker push xxx.xxx.xxx.xxx:5000/mynginx:1.0`  

- docker pushまたはpullコマンドで、イメージ名が指定された形式と一致しない場合はプライベートレジストリからではなく、パブリックレジストリからコンテナイメージをpushまたはpullしようとします。  
- 一度、Dockerイメージをpushすると、同じイメージ名でも上書きができません。（イメージ生成時にリビジョンを変更をするなどが必要。）  
- プライベートレジストリで管理されているコンテナイメージの参照・削除などはWeb-UIを構築することで可能となります。  
（プライベートレジストリのWeb-UIの構築方法はstep3で説明します。）  

## 【プライベートレジストリを利用するためのkubernetesの設定】

### 【master（controlplane:Tab1）/workerノード（node01:Tab2）で実施】  

①rootにユーザを切り替えます。  

$ `sudo -s`{{execute}}  

②kubernetesでプライベートレジストリを利用できるようにするため、「/etc/containerd/config.toml」に記述を追加します。

\# `vi /etc/containerd/config.toml`{{execute}}  

【追加イメージ】

```yaml
{
      # ～省略～
      [plugins."io.containerd.grpc.v1.cri".registry.mirrors]
        [plugins."io.containerd.grpc.v1.cri".registry.mirrors."docker.io"]
          endpoint = ["https://mirror.gcr.io", "https://docker-mirror.killer.sh", "https://registry-1.docker.io"]
        [plugins."io.containerd.grpc.v1.cri".registry.mirrors."xxx.xxx.xxx.xxx:5000"]
          endpoint = ["http://xxx.xxx.xxx.xxx:5000"]
      # ～省略～
}
```

【追加方法】  
1）まず、 [plugins."io.containerd.grpc.v1.cri".registry.mirrors] を検索します。  
2）その下の2行（下記）を追加してください。  

```yaml
[plugins."io.containerd.grpc.v1.cri".registry.mirrors."xxx.xxx.xxx.xxx:5000"]  
  endpoint = ["http://xxx.xxx.xxx.xxx:5000"]  
```

3）「xxx.xxx.xxx.xxx」はregistryノードのIPアドレスを指定します。  
*※但し、本レッスンではmasterノードのIPアドレス（172.30.1.2）を指定してください。*  

※追加位置がわからない場合は、カレントに「config.toml」の見本があります。参考にしてください。  

③containerdを再起動します。（「config.toml」ファイルの反映）  

\# `systemctl restart containerd`{{execute}}  

（一般ユーザに戻します）  

\# `exit`{{execute}}  

**※workerノード（node01:Tab2）でも忘れずに①~④を実施してください。**
