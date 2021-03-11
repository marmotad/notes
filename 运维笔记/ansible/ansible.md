# 1.1 anslble相关文件

```shell
/usr/bin/ansible                        #命令行工具
/usr/bin/ansible-doc                    #帮助文档
/usr/bin/ansible-playbook               #剧本执行工具
/usr/bin/ansible-galaxy                 #下载/上传优秀代码或Roles模块的官网平台
/usr/bin/ansible-pull                   #远程执行命令的工具
/usr/bin/ansible-vault                  #文件加密工具
/usr/bin/ansible-console                #基于Console界面与用户交互的执行工具
/etc/ansible/ansible.cfg                #主配置文件
/etc/ansible/hosts                      #管理的主机清单
/etc/ansible/roles                      #角色存放处
```

# 1.2 Ansible系列命令

```shell
ansible
ansible-doc
ansible-playbook
ansible-vault
ansible-console
ansible-galaxy
ansible-pull
```

## 1.2.1 ansible-doc

```
ansible-doc: 显示模块帮助
ansible-doc [options] [module...]
-a 显示所有模块的文档
-l, --list 列出可用模块
-s, --snippet显示指定模块的playbook片段
示例：
ansible-doc -l 列出所有模块
ansible-doc ping 查看指定模块帮助用法
ansible-doc -s ping 查看指定模块帮助用法
```

## 1.2.2 ansible

+ ansible通过ssh实现配置管理、应用部署、任务执行等功能，建议配置ansible端能基于密钥认证的方式联系各被管理节点

```shell
ansible <host-pattern> [-m module_name] [-a args]
--version 显示版本
-m module 指定模块，默认为command
-v 详细过程 –vv -vvv更详细
--list-hosts 显示主机列表，可简写 --list
-k, --ask-pass 提示输入ssh连接密码，默认Key验证
-C, --check 检查，并不执行
-T, --timeout=TIMEOUT 执行命令的超时时间，默认10s
-u, --user=REMOTE_USER 执行远程执行的用户
-b, --become 代替旧版的sudo 切换
--become-user=USERNAME 指定sudo的runas用户，默认为root
-K, --ask-become-pass 提示输入sudo时的口令ansible的Host-pattern
```

### 1.2.3.3 ansable 常用模块

+ command：在远程主机执行命令，默认模块，可忽略-m选项
  + ansible srvs -m command -a ‘service vsftpd start’
  + ansible srvs -m command -a ‘echo magedu |passwd --stdin wang’
    此命令不支持 $VARNAME < > | ; & 等，用shell模块实现
+ Shell：和command相似，用shell执行命令
  + ansible srv -m shell -a ‘echo magedu |passwd –stdin wang’   调用bash执行命令
  + 类似 cat /tmp/stanley.md | awk -F‘|’ ‘{print $1,$2}’ &> /tmp/example.txt 这些复杂命令，即使使用shell也可能会失败，解决办法：写到脚本时， copy到远程，执行，再把需要的结果拉回执行命令的机器
+ Script：在远程主机上运行ansible服务器上的脚本
  + -a "/PATH/TO/SCRIPT_FILE“
  + ansible websrvs -m script -a /data/f1.sh

### 1.2.3.2 ansible使用示例

+ 以wang用户执行ping存活检测
  + ansible all -m ping -u wang -k
+ 以wang sudo至root执行ping存活检测
  + ansible all -m ping -u wang -k -b
+ 以wang sudo至mage用户执行ping存活检测
  + ansible all -m ping -u wang -k -b --become-user=mage
+ 以wang sudo至root用户执行ls
  ansible all -m command -u wang -a 'ls /root' -b --become-user=root -k -K  

## 1.2.4 ansible的Host-pattern

```shell
ansible的Host-pattern
匹配主机的列表
All ：表示所有Inventory中的所有主机
ansible all –m ping
* :通配符
ansible “*” -m ping
ansible 192.168.1.* -m ping
ansible “*srvs” -m ping
或关系
ansible “websrvs:appsrvs” -m ping
ansible “192.168.1.10:192.168.1.20” -m pingansible的Host-pattern
逻辑与
ansible “websrvs:&dbsrvs” –m ping
在websrvs组并且在dbsrvs组中的主机
逻辑非
ansible ‘websrvs:!dbsrvs’ –m ping
在websrvs组，但不在dbsrvs组中的主机
注意：此处为单引号
综合逻辑
ansible ‘websrvs:dbsrvs:&appsrvs:!ftpsrvs’ –m ping
正则表达式
ansible “websrvs:&dbsrvs” –m ping
ansible “~(web|db).*\.magedu\.com” –m pingansible命令执行过程
```

# 1.3 ansible命令执行过程

1. 加载自己的配置文件 默认/etc/ansible/ansible.cfg
2. 加载自己对应的模块文件，如command
3. 通过ansible将模块或命令生成对应的临时py文件，并将该文件传输至远程服务器的对应执行用户$HOME/.ansible/tmp/ansible-tmp-数字/XXX.PY文件
4. 给文件+x执行
5. 执行并返回结果
6. 删除临时py文件，退出
7. 执行状态：
    绿色：执行成功并且不需要做改变的操作
    黄色：执行成功并且对目标主机做变更
    红色：执行失败

 

 

```
 
 
```