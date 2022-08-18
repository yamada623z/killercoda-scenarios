# スケーリング（kubectlコマンド利用）の動作確認

kubectlコマンドはkubernetesに関する各種操作を行うコマンドです。  
kubectlコマンドを利用してPodのスケーリング（サービスを継続したままでのPod数の増減）の操作確認を実施します。  

## 【masterノードで実施（controlplane:Tab1）】  

①現在のPodの状態を確認する。  
$ `kubectl get pods`{{execute}}  

②kubectlコマンド利用してPodをスケールします。（数字の部分を変更します）  
$ `kubectl scale --replicas=3 deployment.apps/nginx`{{execute}}  

- 現在のPod数より増やすとスケールアウト（Pod数が増える。）  
- 現在のPod数より減らすとスケールイン（Podの数が減る。）  

③下記のコマンドでPodの状態を確認する。（Pod数が②で指定した数であることを確認します）  
$ `kubectl get pods`{{execute}}  

④Step9でアクセスした、**現在アクセス中のPodの名前が表示されているブラウザ** をリロードして、サービスが継続していることを確認します。  

（表示例）
![Welcome Image](https://github.com/yamada623z/scenario-image/raw/main/KubernetesHandsOn_BuildPod/Uname.jpg)  
