# サービスアカウントの作成

## 【masterノード（controlplane）で実施】  

サービスアカウントを作成し、「**admin-user**」権限でログインします。（全ての操作、表示が可能となります。）  

①下記のmanifestファイルを用意する。  
$ `cd`{{execute}}  

$ `vi service-account.yaml`{{execute}}  

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kubernetes-dashboard
```

②作成したmanifestファイルをデプロイします。  
$ `kubectl apply -f service-account.yaml`{{execute}}  

③下記のコマンドで、トークンを生成します。  
$ `kubectl -n kubernetes-dashboard create token admin-user`{{execute}}  

（表示例）

```text
eyJhbGciOiJSUzI1NiIsImtpZCI6ImVBaDNDeElCdG9jU3BQNmZOVTB4N1MwWlBrVGY4d2F1M191SnY2S0hETTgifQ.eyJhdWQiOlsiaHR0cHM6Ly9rdWJlcm5ldGVzLmRlZmF1bHQuc3ZjLmNsdXN0ZXIubG9jYWwiXSwiZXhwIjoxNjU4OTg3NDU1LCJpYXQiOjE2NTg5ODM4NTUsImlzcyI6Imh0dHBzOi8va3ViZXJuZXRlcy5kZWZhdWx0LnN2Yy5jbHVzdGVyLmxvY2FsIiwia3ViZXJuZXRlcy5pbyI6eyJuYW1lc3BhY2UiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsInNlcnZpY2VhY2NvdW50Ijp7Im5hbWUiOiJhZG1pbi11c2VyIiwidWlkIjoiMzc4OTBmODEtZTMzMi00MzZjLTlkNzQtZGFiNTMzN2Y2YjFkIn19LCJuYmYiOjE2NTg5ODM4NTUsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDprdWJlcm5ldGVzLWRhc2hib2FyZDphZG1pbi11c2VyIn0.x61q5p38_1Fq17RzQz0eZ0A0n9jPvwagU5ye6FINeY_p-3ucEQVoCOBFCL_P512_g5x58T6GzvGAAfhfkUi_pmpyUYTnigoZhDoRahGoDyeCcaEqRzsXUlxApB1b-Qvqp-ikg059SMoNI5J0op7YaCUibNrtBtn3v_5UwF41z8FmZR-gIUHC1oXPb5iWi7OYCX2FskJt7xQrTP34LshcwbU0XgPLu7H4QMZKlVQfPx1wJwH48JcWdOVx3L46qpG990y3c15AYk9DuL6L8M8GxzDb9yJQ1Vit16QPdOK4YJdso9o6NFVr61vcvP5Pn_hc0aB8z4FK7gcHBT_I3VSe5g
```

④上記コマンドで表示された文字列をマウスで選択し、コピーします。  
*※ここでサインインしたままの状態の場合は、次の手順を実施する前に右上の丸い人物アイコンで下の表示例のサインアウト状態してください。*
*※「error forwarding port 9090」が発生した場合は、Step11-②を再実行してください。*  

（表示例）  
![DashBoard Image](https://github.com/yamada623z/scenario-image/raw/main/KubernetesHandsOn_BuildCluster/Step11.jpg)  

⑤現在、ダッシュボードに表示されている「Kubernetes Dashboard」のウインドウ上のラジオボタン「**トークン**」をチェックし、下段の「**トークンを入力**」に④でコピーした文字列をペーストして「**サインイン**」ボタンをクリックします。  

（表示例）  
![DashBoard Image](https://github.com/yamada623z/scenario-image/raw/main/KubernetesHandsOn_BuildCluster/Step13.jpg)  

*※検索ボックス左横のネームスペースの設定を「default」から「すべてのネームスペース」としてください。*  
