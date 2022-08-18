# コンテナイメージの検索（docker search）

Nginxを実行するように構成されているDockerイメージの名前を特定します。 Dockerを使用すると、すべてのコンテナがDockerイメージに基づいて開始されます。 これらのイメージには、プロセスの起動に必要なすべてのものが含まれています。 ホストは構成や依存関係を必要としません。

$ `docker search nginx`{{execute}}

コマンド「**docker search** *name*」を使用して、既存のイメージを見つけることができます。 たとえば、Nginxのイメージを見つけるには、「**docker search** *nginx*」を使用します。
