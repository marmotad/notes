# Git Lab

二、安装gitlab

1、下载giltlab包

+ 官网下载对应包

2、安装gitlab

`yum install gitlabxxx`

3、修改gitlab配置文件

```
[root@localhost ~]# egrep -vn "^$|^#" /etc/gitlab/gitlab.rb 
32:external_url 'http://172.18.128.4'
69:gitlab_rails['time_zone'] = 'Asia/Shanghai'
91:gitlab_rails['smtp_enable'] = true
92:gitlab_rails['smtp_address'] = "smtp.qq.com"
93:gitlab_rails['smtp_port'] = 25
94:gitlab_rails['smtp_user_name'] = "1209837078@qq.com"  ##自己的qq邮箱账号
95:gitlab_rails['smtp_password'] = "qriuvijuofhghjgd"  ##开通smtp时返回的授权码
96:gitlab_rails['smtp_domain'] = "qq.com"
97:gitlab_rails['smtp_authentication'] = "login"   
98:gitlab_rails['smtp_enable_starttls_auto'] = true
99:gitlab_rails['smtp_tls'] = false
100:gitlab_rails['gitlab_email_from'] = "1209837078@qq.com"  ##指定发送邮件的邮箱地址
101:user["git_user_email"] = "1209837078@qq.com"   ##指定接收邮件的邮箱地址
1799:alertmanager['admin_email'] = '1209837078@qq.com'

```

4、加载配置文件并启动gitlab

```
gitlab-ctl reconfigure
gitlab-ctl start
gitlab-ctl status
```

![image-20201117204529907](Git%20Lab.assets/image-20201117204529907.png)