gitlabs镜像

硬件要求

配置gitlab配置文件，/srv/gitlab/config/gitlab.rb 添加如下配置：
```
external_url 'http://192.168.160.137' #

# 邮件相关配置
gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = "smtp.126.com"
gitlab_rails['smtp_port'] = 25
gitlab_rails['smtp_user_name'] = "dong_fei1991@126.com"
gitlab_rails['smtp_password'] = "fufangqing1024"
gitlab_rails['smtp_domain'] = "126.com"
gitlab_rails['smtp_authentication'] = "login"
gitlab_rails['smtp_enable_starttls_auto'] = true
gitlab_rails['smtp_openssl_verify_mode'] = 'peer'
gitlab_rails['gitlab_email_from'] = 'dong_fei1991@126.com'
gitlab_rails['gitlab_email_reply_to'] = 'dong_fei1991@126.com'
```



1. 如果系统Selinux是否已开启（/etc/selinux/config 文件中SELINUX值是否为enforcing）
  1. SElinux开启
```
sudo docker run --detach \
  --hostname gitlab.example.com \
  --publish 443:443 --publish 80:80 --publish 50022:22 \
  --name gitlab \
  --restart always \
  --volume /srv/gitlab/config:/etc/gitlab:Z \
  --volume /srv/gitlab/logs:/var/log/gitlab:Z \
  --volume /srv/gitlab/data:/var/opt/gitlab:Z \
  gitlab/gitlab-ce:latest
```
  2. SElinux未开启
  ```
  sudo docker run --detach \
  --hostname gitlab.example.com \
  --publish 443:443 --publish 80:80 --publish 50022:22 \
  --name gitlab \
  --restart always \
  --volume /srv/gitlab/config:/etc/gitlab \
  --volume /srv/gitlab/logs:/var/log/gitlab \
  --volume /srv/gitlab/data:/var/opt/gitlab \
  gitlab/gitlab-ce:latest
  ```




gitlabs创建用户后，会将初始化密码连接地址发到你的邮箱

![avatar](https://raw.githubusercontent.com/oracleJava/docker-note/master/images/gitlabs%E5%88%9D%E5%A7%8B%E5%8C%96%E5%AF%86%E7%A0%81%E9%82%AE%E4%BB%B6.png)

```
gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = "smtp.126.com"
gitlab_rails['smtp_port'] = 25
gitlab_rails['smtp_user_name'] = "dong_fei1991@126.com"   
gitlab_rails['smtp_password'] = "fufangqing1024"
gitlab_rails['smtp_domain'] = "126.com"
gitlab_rails['smtp_authentication'] = "login"
gitlab_rails['smtp_enable_starttls_auto'] = true
gitlab_rails['smtp_openssl_verify_mode'] = 'peer'
gitlab_rails['gitlab_email_from'] = 'dong_fei1991@126.com'
gitlab_rails['gitlab_email_reply_to'] = 'dong_fei1991@126.com'
```
