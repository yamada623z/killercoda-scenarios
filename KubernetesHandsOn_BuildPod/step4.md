# コンテナイメージの作成

Pod作成に必要な二つのコンテナイメージを作成します。  

## 【masterノードで実施（controlplane:Tab1）】  

①Topフォルダ（nginxphp）と作成するコンテナイメージ毎（nginx,php-fpm）にフォルダを作成します。  

$ `mkdir nginxphp`{{execute}}  

$ `mkdir nginxphp/nginx`{{execute}}  

$ `mkdir nginxphp/phpfpm`{{execute}}  

②nginxのコンテナイメージ作成に必要なファイルを移動します。  

$ `mv default.conf nginxphp/nginx`{{execute}}  

③php-fpmのコンテナイメージに必要なフォルダの作成し、ファイルを移動します。  

$ `mkdir nginxphp/phpfpm/php-fpm.d`{{execute}}  

$ `mv php.ini nginxphp/phpfpm/`{{execute}}  

$ `mv php-fpm.conf nginxphp/phpfpm/`{{execute}}  

$ `mv *.php nginxphp/phpfpm/`{{execute}}  

$ `mv www.conf nginxphp/phpfpm/php-fpm.d`{{execute}}  

④nginxのコンテナイメージを作成します。「Dockerfile」を作成して、コンテナイメージ「mynginx:1.0」を作成します。  

$ `cd nginxphp/nginx`{{execute}}  

$ `vi Dockerfile`{{execute}}  

```text
FROM nginx
ADD default.conf /etc/nginx/conf.d
```{{copy}}

$ `sudo docker build -t mynginx:1.0 .`{{execute}}  

⑤php-fpmのコンテナイメージを作成します。「Dockerfile」を作成して、コンテナイメージ「myphpfpm:1.0」を作成します。  
  
$ `cd ../phpfpm`{{execute}}  

$ `vi Dockerfile`{{execute}}  

```text
FROM php:7-fpm
ADD php.ini /usr/local/etc/php/php.ini
ADD php-fpm.conf /usr/local/etc/php-fpm.conf
ADD php-fpm.d /usr/local/etc/php-fpm.d
ADD index.php /var/www/html
ADD test.php /var/www/html
```{{copy}}

$ `sudo docker build -t myphpfpm:1.0 .`{{execute}}  
