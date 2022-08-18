# ＜今回の目標＞

## 【基盤構築】

- kubernetesの環境（masterノード（controlplane））を構築する。  
- workerノードを1台作成し、 kubernetesの環境（クラスタ）に追加する。  
- kubernetesの環境（masterノード（controlplane））にダッシュボードを実装する。  

## 【必要条件】

実ノードでの必要条件は以下の通り。  
（参考：`https://kubernetes.io/ja/docs/setup/independent/install-kubeadm/`）  

- 次のいずれかを実行する1つ以上のマシン：  
  - Ubuntu 16.04+  
  - Debian 9+  
  - CentOS 7  
  - RHEL 7  
  - Fedora 25+  
  - HypriotOS v1.0.1+  
  - Container Linux（1800.6.0でテスト済み）  
- マシンごとに2GB以上のRAM（これより少ないと、アプリ用のスペースがほとんどなくなります）  
- 2CPU以上  
- クラスタ内のすべてのマシン間の完全なネットワーク接続（パブリックまたはプライベートネットワークで問題ありません）  
- 各ノードの一意のホスト名、MACアドレス、およびproduct_uuid （カーネルによって生成されるシステム固有のID）  
- マシンで特定のポートが開いている。  
- スワップは無効です。kubeletが正常に機能するには、スワップを無効にする必要があります。  

## 【注意】

*通常はrootユーザーのプロンプトは「#」ですが、Killercodaでは「sudo -s」コマンドでrootユーザーに切り替えてもプロンプトは「$」のままとなります。*  
