---
categories: [Miscellaneous]
tags: [杂项]
math: true
mermaid: true
render_with_liquid: true
img_path: 
description: 手动申请nginx SSL证书的流程
pin: 
---

手动申请 Nginx 免费证书通常是通过使用 Let's Encrypt 这样的服务来实现的。Let's Encrypt 提供免费的 SSL/TLS 证书，并且有许多工具可以简化证书的申请和配置流程。最常用的工具是 **Certbot**。以下是手动申请和配置 Nginx 免费证书的步骤：

### 1\. 安装 Certbot

首先，确保你已经安装了 Certbot。根据你的操作系统，使用以下命令进行安装。

#### 对于 Ubuntu / Debian

`sudo apt update
sudo apt install certbot python3-certbot-nginx` 

#### 对于 CentOS / RHEL

`sudo yum install epel-release
sudo yum install certbot python2-certbot-nginx` 

### 2\. 配置 Nginx

确保你的 Nginx 已经安装和配置，并且你已经有一个域名指向你的服务器 IP 地址。你可以在 `/etc/nginx/sites-available/your_domain` 中配置 Nginx 服务器块，假设你的 Nginx 配置文件中有类似如下内容：

`server {
 listen 80;
 server_name your_domain.com www.your_domain.com;

 location / {
 root /var/www/your_domain;
 index index.html index.htm;
 }
}` 

确保你在此配置中替换相应的域名和文档根目录。

### 3\. 申请 SSL 证书

运行以下命令来使用 Certbot 申请 SSL 证书并自动配置 Nginx：

`sudo certbot --nginx` 

这将启动一个交互式过程。你需要提供有关你的域名和电子邮件地址的信息。Certbot 会检查 Nginx 配置文件，并自动为匹配的域名申请 SSL 证书。

*   **输入域名**：按照提示输入你的域名。
*   **电子邮件地址**：Certbot 通常要求提供电子邮件地址以便接收证书更新和使用安全警告。
*   **同意服务条款**：确认您同意 Let's Encrypt 的服务条款。
*   **是否选择自动重定向**：选择是否将所有 HTTP 流量重定向到 HTTPS。

### 4\. 手动配置（如果不使用 `--nginx` 标志）

如果你不希望 Certbot 自动配置 Nginx，可以使用以下命令手动申请证书：

`sudo certbot certonly --webroot -w /var/www/your_domain -d your_domain.com -d www.your_domain.com` 

这个命令将会申请证书，只创建证书文件，而不会修改 Nginx 配置。确保将 `/var/www/your_domain` 替换为你的网页根目录。  
This command will apply for a certificate and only create the certificate file without modifying the Nginx configuration. Make sure to replace `/var/www/your_domain` with your web page root directory.

### 5\. 验证 SSL 证书

完成证书申请后，你可以通过运行以下命令来验证 SSL 证书是否成功申请：

`sudo certbot certificates` 

你将看到你申请的证书的详细信息。

### 6\. 配置 Nginx 以使用 SSL 证书

如果没有自动配置，或者你想手动配置 Nginx，请将你的 Nginx 配置文件更新为类似以下内容：

`server {
 listen 443 ssl;
 server_name your_domain.com www.your_domain.com;

 ssl_certificate /etc/letsencrypt/live/your_domain.com/fullchain.pem;
 ssl_certificate_key /etc/letsencrypt/live/your_domain.com/privkey.pem;

 location / {
 root /var/www/your_domain;
 index index.html index.htm;
 }
}

server {
 listen 80;
 server_name your_domain.com www.your_domain.com;
 return 301 https://$host$request_uri; # 重定向 HTTP 到 HTTPS
}` 

### 7\. 重新加载 Nginx

配置完后，需要重新加载 Nginx 使更改生效：

`sudo systemctl reload nginx` 

### 8\. 设置自动续期（可选）

Let's Encrypt 的证书有效期为 90 天。您可以通过设置定期任务（cron job）来自动续期证书。使用 `certbot` 可以很方便地进行自动续期：

`sudo crontab -e` 

在文件中添加以下行：

`0 0 * * * /usr/bin/certbot renew --quiet` 

这会每天午夜运行证书续期命令。

### 总结

通过以上步骤，你可以成功手动申请 Nginx 的免费 SSL 证书。当一切设置完成后，访问你的域名时应该可以通过 HTTPS 安全地查看网页。确保定期检查和更新证书，以保持网站的安全。
