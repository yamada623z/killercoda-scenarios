# オートヒーリングの動作確認

kubectlコマンドを利用してPodのオートヒーリング（サービスを継続したままでのPodの自動復旧）の操作確認を実施します。  

## 【masterノードで実施（controlplane:Tab1）】  

①現在のPodの状態を確認する。  
$ `kubectl get pods`{{execute}}  

②Podを削除します。  

- ①のコマンドで表示されたPod名（nginx-xxxxxxxx-xxxx）を指定します。  

$ `kubectl delete pods nginx-xxxxxxxx-xxxx`  

③下記のコマンドでPodの状態を確認する。  
$ `kubectl get pods`{{execute}}  

- 削除した分のPodが新たに生成されていることを確認する。（削除したPod名の消滅、新たなPod名での生成を確認します）  

④Step9でアクセスした、**現在アクセス中のPodの名前が表示されているブラウザ** をリロードして、サービスが継続していることを確認します。  

（表示例）  
![Welcome Image](https://github.com/yamada623z/scenario-image/raw/main/KubernetesHandsOn_BuildPod/Uname.jpg)  
