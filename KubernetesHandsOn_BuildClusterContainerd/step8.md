# クラスターのノード状態の確認（kubectl get nodes）

## 【masterノード（controlplane）で実施】  

①ノード状態を確認し、クラスターの正常性を確認します。  

$ `kubectl get nodes`{{execute}}  

（表示例）

```text  
$ kubectl get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   84s   v1.18.0
node01         Ready    <none>          24s   v1.18.0
```  
