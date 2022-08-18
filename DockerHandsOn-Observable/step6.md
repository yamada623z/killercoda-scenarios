# メトリクス機能を有効にする

最初の作業は、メトリクス機能を有効にする（新しい）experimentalフラグを有効にし、localhost:9323でリッスンするメトリクスアドレスを定義することです。「/etc/docker/daemon.json」に記述し、dockerをリスタートします。  

- daemon.jsonに「"metrics-addr": "127.0.0.1:9323",」「"experimental": true」の行を追加します。  
※JSON記述文の文末に追加しているため、前の行の文末に「,」（下記の「"mtu": 1454,」の部分）を追加することを忘れずに。）  

\# `vi /etc/docker/daemon.json`{{execute}}  

```json
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "storage-driver": "overlay2",
  "registry-mirrors": ["https://mirror.gcr.io","https://docker-mirror.killer.sh"],
  "mtu": 1454,
  "metrics-addr": "127.0.0.1:9323",
  "experimental": true
}
```  

\# `systemctl restart docker`{{execute}}  

dockerが開始すると、メトリックエンドポイントにアクセスできるようになります。下記のコマンドで表示できます。  

\# `curl localhost:9323/metrics`{{execute}}  
