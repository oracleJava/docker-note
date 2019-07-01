#### 一、配置gitlab配置文件，/srv/gitlab/config/gitlab.rb 添加如下配置：

```
external_url 'http://192.168.160.137' # 克隆的外部地址

# 邮件相关配置
gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = "smtp.126.com" # 系统邮件发送服务器
gitlab_rails['smtp_port'] = 25 # 系统邮件发送服务器端口
gitlab_rails['smtp_user_name'] = "xxxxx@126.com" # 系统邮件发送账号
gitlab_rails['smtp_password'] = "xxxxx" # 系统邮件发送账号密码
gitlab_rails['smtp_domain'] = "126.com" # 系统邮件发送服务器域名
gitlab_rails['smtp_authentication'] = "login" # 系统邮件发送服务器认证类型
gitlab_rails['smtp_enable_starttls_auto'] = true
gitlab_rails['smtp_openssl_verify_mode'] = 'peer'
gitlab_rails['gitlab_email_from'] = 'xxxxx@126.com'
gitlab_rails['gitlab_email_reply_to'] = 'xxxxx@126.com'
```
#### 二、如果系统Selinux是否已开启（/etc/selinux/config 文件中SELINUX值是否为enforcing）

1.  SElinux开启
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
2.  SElinux未开启
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
3. 启动日志查看：
  ```
  docker logs -f gitlab
  ```

#### 三、启动成功后第一次访问需要设置root密码：

![avatar](https://raw.githubusercontent.com/oracleJava/docker-note/master/images/gitlabs%E5%90%AF%E5%8A%A8%E5%90%8E%E7%AC%AC%E4%B8%80%E6%AC%A1%E8%AE%BF%E9%97%AE%E9%A1%B5%E9%9D%A2.png)

#### 四、重置密码后就可以登录到系统了

![avatar](https://raw.githubusercontent.com/oracleJava/docker-note/master/images/root%E7%99%BB%E5%BD%95%E7%B3%BB%E7%BB%9F%E5%90%8E%E9%A1%B5%E9%9D%A2.png)
