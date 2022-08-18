# ダッシュボードの認証方法

## 【masterノード（controlplane）で実施】  

新たにターミナル「**Tab2**」を生成して、手順を進めます。  

> **Killercodaのターミナルの生成方法：**  
> ①ターミナルペインの「**Tab1**」「**＋**」のタグの「**＋**」をクリックします。  
> ②しばらくするとターミナルペインの「**Tab1**」「**＋**」のタグの並びに「**Tab2**」が出現するので、それをクリックします。  

ダッシュボードをtokenで認証し、ログインします。  

①権限は細かく分かれており、デフォルトで色々な種類があります。「**kubectl**」コマンドを使用して「**deployment-controller**」権限でログインを試みます。  
$ `kubectl -n kube-system create token deployment-controller`{{execute}}  

（表示例）  

```text
eyJhbGciOiJSUzI1NiIsImtpZCI6ImVBaDNDeElCdG9jU3BQNmZOVTB4N1MwWlBrVGY4d2F1M191SnY2S0hETTgifQ.eyJhdWQiOlsiaHR0cHM6Ly9rdWJlcm5ldGVzLmRlZmF1bHQuc3ZjLmNsdXN0ZXIubG9jYWwiXSwiZXhwIjoxNjU4OTg5OTE3LCJpYXQiOjE2NTg5ODYzMTcsImlzcyI6Imh0dHBzOi8va3ViZXJuZXRlcy5kZWZhdWx0LnN2Yy5jbHVzdGVyLmxvY2FsIiwia3ViZXJuZXRlcy5pbyI6eyJuYW1lc3BhY2UiOiJrdWJlLXN5c3RlbSIsInNlcnZpY2VhY2NvdW50Ijp7Im5hbWUiOiJkZXBsb3ltZW50LWNvbnRyb2xsZXIiLCJ1aWQiOiI3MzQ1N2UyZi05ODliLTRhOTAtYjhhOC02N2FjMTZjY2VhMzEifX0sIm5iZiI6MTY1ODk4NjMxNywic3ViIjoic3lzdGVtOnNlcnZpY2VhY2NvdW50Omt1YmUtc3lzdGVtOmRlcGxveW1lbnQtY29udHJvbGxlciJ9.X1oryC4gKbsgP8-M6pOLtAiG_4zl7eqRiEbsLRIE_D3PZllVc9ZOPjmkcRJH026DgUR0pUMZ9wrVWbetDkE31GMSyO3ozAp8pZ_xybtPjHO0lTYSDcGOpHIfhjwfv7SdcDEcBAdORr33r-Jt9tp1uSraHQ26OHI9yaISdLYIGJYCfVFIQflaD3y4N7jV0Ij_MYrbbqaXrEzkq9lSqXyua2K3laL_Ei5Zpi56UuYb37w6Z1mQBpsh2Gh5bSFHxh0BANtB3EJT-Q7_rbwe7O-6Htt70J5w1xhvSNqaEDVyoxEnoefgOf5aPAOd-TZMoOwlVV8rRHA4X3Zr02sYxsu-gA
```

②上記コマンドで表示された文字列をマウスで選択し、コピーします。  

③現在、ダッシュボードに表示されている「Kubernetes Dashboard」のウインドウ上のラジオボタン「**トークン**」をチェックし、下段の「**トークンを入力**」に②でコピーした文字列をペーストして「**サインイン**」ボタンをクリックします。  

**（表示例）**  
![DashBoard Image](https://github.com/yamada623z/scenario-image/raw/main/KubernetesHandsOn_BuildCluster/Step12.jpg)  
