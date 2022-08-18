# kubernetesクラスターからのpodの削除

Step6で作成したmanifestファイルで、kubernetesクラスターからPodを削除します。  
*※このステップを実施した場合は、Step7を再度、実施してください。*  

## 【masterノードで実施（controlplane:Tab1）】  

①下記のコマンドでkubernetesクラスターからPodを削除します。  

$ `kubectl delete -f nginxphp_pod.yaml`{{execute}}  

②Podの起動状況を確認します。

$ `kubectl get pods`{{execute}}  
