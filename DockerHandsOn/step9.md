# イメージの削除（docker rmi）

Dockerホストマシンにダウンロードされたイメージは、コマンド「**docker images**」で確認することができます。  

$ `docker images`{{execute}}  

必要のないDockerイメージはDockerホストマシンから削除することができます。  
コマンドは「**docker rmi** *image-name* または *image-id*」です。  
*image-name* はリポジトリ名とタグの組み合わせです。  
*image-id*は「**docker images**」で確認することができます。  

$ `docker rmi nginx`{{execute}}  

DockerイメージがDockerホストマシンから削除されたことを確認します。  

$ `docker images`{{execute}}  
