# dockerのインストール

本レッスンでは必要ありませんが、dockerコンテナを動作させる実ノードでは下記の手順でdockerをインストール必要があります。  
*※①の手順のみ、次以降のStepで必要なため、実施してください。*  

①rootにユーザを切り替える。

$ `sudo -s`{{execute}}

②dockerをインストールする。（ubuntuの場合）

\# `apt install docker.io`

③システム起動時に起動するように設定する。

\# `systemctl enable docker`
