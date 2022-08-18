# Weave Scopeの起動  

Weave Scopeはブラウザを通して、ホスト上でどのようなコンテナやアプリケーション（プロセス）が稼働しているかどうか見ることができ、その関連性をリアルタイムでマッピング（地図化）するためのものです。

Weave Scopeはコンテナとして実行され、HTTP経由でアクセスされます。  

Weave Scopeを起動するには、視覚化するホストでコマンド「scope launch」を実行します。（「weavescope」コンテナが起動します。）  

\# `wget -O scope git.io/scope`{{execute}}  
\# `chmod +x ./scope`{{execute}}  
\# `cp ./scope /usr/local/bin/scope`{{execute}}  

\# `scope launch`{{execute}}  
