# kubernetes上のpodの動作確認

ブラウザでアドレスを指定して表示を確認します。

- nginxのwelcomeメッセージが表示されることを確認します。  

  ブラウザからのアクセスは以下の通りです。（例：「xxx.xxx.xxx.xxx」はmasterノードのIPアドレスです。）  
  `https://xxx.xxx.xxx.xxx:31001`  

> **KillercodaのWebアクセス方法：**  
> ①ターミナルペインの「**Tab1**」「**Tab2**」「**＋**」のタグの並びの一番右にある「**三**」をクリックする。  
> ②表示されるドロップリストから「**Traffic / Ports**」をクリックする。
> ③新しいブラウザタブ「**Traffic Port Accessor**」が表示されたら、「**Host 1**」「**Custom Ports**」の下のボックスに「**31001**」を入力し、「**Access**」をクリックします。  

（表示例）  
![Welcome Image](https://github.com/yamada623z/scenario-image/raw/main/KubernetesHandsOn_BuildPod/Welcome.jpg)  

- 現在アクセス中のPodの名前が表示されることを確認します。  

  ブラウザからのアクセスは以下の通りです。（例：「xxx.xxx.xxx.xxx」はmasterノードのIPアドレスです。）
  `https://xxx.xxx.xxx.xxx:31001/test.php`  

> **KillercodaのWebアクセス方法：**  
> ①ターミナルペインの「**Tab1**」「**Tab2**」「**＋**」のタグの並びの一番右にある「**三**」をクリックする。  
> ②表示されるドロップリストから「**Traffic / Ports**」をクリックする。
> ③新しいブラウザタブ「**Traffic Port Accessor**」が表示されたら、「**Host 1**」「**Custom Ports**」の下のボックスに「**31001**」を入力し、「**Access**」をクリックします。  
> ④ブラウザのURLの末尾に「/test.php」を追加すると、アクセス中のPodの名前が表示される。  

（表示例）  
![Uname Image](https://github.com/yamada623z/scenario-image/raw/main/KubernetesHandsOn_BuildPod/Uname.jpg)  

- phpの情報が表示されることを確認します。  

  ブラウザからのアクセスは以下の通りです。（例：「xxx.xxx.xxx.xxx」はmasterノードのIPアドレスです。）
  `https://xxx.xxx.xxx.xxx:31001/index.php`  

> **KillercodaのWebアクセス方法：**  
> ①ターミナルペインの「**Tab1**」「**Tab2**」「**＋**」のタグの並びの一番右にある「**三**」をクリックする。  
> ②表示されるドロップリストから「**Traffic / Ports**」をクリックする。
> ③新しいブラウザタブ「**Traffic Port Accessor**」が表示されたら、「**Host 1**」「**Custom Ports**」の下のボックスに「**31001**」を入力し、「**Access**」をクリックします。  
> ④ブラウザのURLの末尾に「/index.php」を追加すると、php情報（phpinfo()）が表示される。  

（表示例）  
![Info Image](https://github.com/yamada623z/scenario-image/raw/main/KubernetesHandsOn_BuildPod/Info.jpg)  
