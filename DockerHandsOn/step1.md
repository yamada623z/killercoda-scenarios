# dockerのインストール  

**※本レッスンでは必要ありませんが、dockerコンテナを動作させる実ノードでは下記の手順でdockerをインストール必要があります。**

①rootにユーザを切り替える。

$ `sudo -s`

②dockerをインストールする。（ubuntuの場合）

\# `apt install docker.io`

③システム起動時に起動するように設定する。

\# `systemctl enable docker`
