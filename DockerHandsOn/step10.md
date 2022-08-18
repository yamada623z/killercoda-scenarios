# コンテナ上でのコマンド実行

Dockerで新たに作られたUbuntu環境のコンテナで「**ps**」コマンドを内部的に実行して、「**ps**」コマンドの実行結果を出力します。  

$ `docker run ubuntu ps`{{execute}}  

（表示例）  

```text
PID  TTY  TIME  CMD  
1  ?  00:00:00:00  ps 
```
