# 1 时间同步

## 1.1 使用chrony自动同步时间

### 1.1.1 作用：

linux中，有些服务必须依靠准确的时间，才能够在运行的时候不出差错，例如DNS，LVS，HTTPS等，都需要后台的服务器之间保持时间的同步。而Centos系统中自带的有安装对应的同步时间的服务。centos7中默认安装的是chrony，而Centos6相比在时间服务有所不同，使用了ntp服务来同步时间，而在Centos7上则使用的是chrony服务来同步时间，相较与ntp服务。chrony服务有如下几点优势：

```html
1，更快的同步只需要数分钟而非数小时时间，从而最大程度减少了时间和频率误差，对于并非全天 24 小时运行
的虚拟计算机而言非常有用
2，能够更好地响应时钟频率的快速变化，对于具备不稳定时钟的虚拟机或导致时钟频率发生变化的节能技术而言
非常有用
3，在初始同步后，它不会停止时钟，以防对需要系统时间保持单调的应用程序造成影响
4，在应对临时非对称延迟时（例如，在大规模下载造成链接饱和时）提供了更好的稳定性
5，无需对服务器进行定期轮询，因此具备间歇性网络连接的系统仍然可以快速同步时钟
```

### 1.1.2 监听端口：

323/udp，123/udp

### 1.1.3 配置文件：

/etc/chrony.conf

## 1.2 安装与使用：

### 1.2.1 安装chrony

```shell
yum -y install chrony  
#系统默认已经安装，如未安装，请执行以下命令安装
```

### 1.2.2启动并加入开机自启动

```shell
systemctl enable --now chronyd.service
```

### 1.2.3关闭SElinux与防火墙

```shell
systemctl disable --now firewalld
setenforce 0 #临时关闭SElinux
sed -i 's#SELINUX=enforcing#SELINUX=disabled#g' /etc/sysconfig/selinux
sed -i 's#SELINUX=enforcing#SELINUX=disabled#g' /etc/selinux/config
#关闭SElinux
```

### 1.2.4 配置chrony

```shell
cat /etc/chrony.conf
#下方是默认的四个同步时间的服务器，不过该服务器同步时间略慢，可以按照格式修改成本地的时间服务器
server 0.centos.pool.ntp.org iburst
server 1.centos.pool.ntp.org iburst
server 2.centos.pool.ntp.org iburst
server 3.centos.pool.ntp.org iburst
......
# 指定一台主机、子网，或者网络以允许或拒绝NTP连接到扮演时钟服务器的机器
#allow 192.168.0.0/16
#deny 192.168/16
......
# 指定日志文件的目录
logdir /var/log/chrony
......
```

## 1.3 设置时区

```shell
timedatectl 
#查看系统的当前的时区
				Local time: 日 2019-05-26 10:42:00 CST
				Universal time: 日 2019-05-26 02:42:00 UTC
				RTC time: 日 2019-05-26 02:42:00
				Time zone: Asia/Shanghai (CST, +0800)
				NTP enabled: yes
				NTP synchronized: no
				RTC in local TZ: no
				DST active: n/a
```

如果当前时区不是亚洲/上海时区，可以用如下命令设置

```html
timedatectl set-timezone Asia/Shanghai
```

## 1.4 服务器集群之间的系统时间同步

```shell
服务器端：
注释掉默认的时间服务器
#server 0.centos.pool.ntp.org iburst
#server 1.centos.pool.ntp.org iburst
#server 2.centos.pool.ntp.org iburst
#server 3.centos.pool.ntp.org iburst
并添加以下内容：（内网的时间同步器或互联网中的时间同步器）
server 172.22.0.1 iburst 
配置完成后重启服务，这样我们需求的一台内网时间服务器已经配置完毕。
1.2.3.4.5.6.7.8.9.
客户端：
同样注释掉其他server，并在客户端（192.168.1.10）添加刚配置的时间服务器的IP地址：
server 192.168.1.9 iburst
#将这一行取消注释，当无法从时间服务器中获得正确的时间时，可以让本服务器充当网络内的时间服务器
# Allow NTP client access from local network.
allow 192.168.0.0/24
到此已经完成系统时间的同步。如有多台机器，操作亦是如此
```

## 1.5 常用命令

```shell
查看时间同步源：
chronyc sources -v
查看时间同步源状态：
chronyc sourcestats -v
设置硬件时间
硬件时间默认为UTC：
timedatectl set-local-rtc 1
启用NTP时间同步：
timedatectl set-ntp yes
校准时间服务器：
chronyc tracking
```

# 2 基础配置

## 2.1 配置yum

```shell
yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
cat <<EOF > /etc/yum.repos.d/ku
bernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64/
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg https://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
EOF
sed -i -e '/mirrors.cloud.aliyuncs.com/d' -e '/mirrors.aliyuncs.com/d' /etc/yum.repos.d/CentOS-Base.repo
```
## 2.2 安装必备工具

```shell
yum install -y yum-utils device-mapper-persistent-data lvm2
yum install wget jq psmisc vim net-tools telnet yum-utils device-mapper-persistent-data lvm2 git -y
```

## 2.3 所有节点关闭防火墙、selinux、dnsmasq、swap

### 2.3.1 关闭防火墙、selinux、dnsmasq、swap

```shell
systemctl disable --now firewalld dnsmasq NetworkManager
# centos8需要开启NetworkManager
setenforce 0
sed -i 's#SELINUX=enforcing#SELINUX=disabled#g' /etc/sysconfig/selinux
sed -i 's#SELINUX=enforcing#SELINUX=disabled#g' /etc/selinux/config
```

### 2.3.2 关闭swap分区

```shell
swapoff -a && sysctl -w vm.swappiness=0
sed -ri '/^[^#]*swap/s@^@#@' /etc/fstab
```

### 2.3.3 所有节点配置limit：

```shell
ulimit -SHn 65535
# 临时生效
vim /etc/security/limits.conf
# 末尾添加如下内容
* soft nofile 65536
* hard nofile 131072
* soft nproc 65535
* hard nproc 655350
* soft memlock unlimited
* hard memlock unlimited
```

### 2.3.4 在一个节点配置免密登录

```shell
ssh-keygen -t rsa
for i in master1 master2 master3 node1 node2;do ssh-copy-id -i .ssh/id_rsa.pub $i;done
```

# 3 升级内核

CentOS7 需要升级内核至4.18+，本地升级的版本为4.19

## 3.1 所有节点下载内核

```shell
cd /root
wget http://193.49.22.109/elrepo/kernel/el7/x86_64/RPMS/kernel-ml-devel-4.19.12-1.el7.elrepo.x86_64.rpm
wget http://193.49.22.109/elrepo/kernel/el7/x86_64/RPMS/kernel-ml-4.19.12-1.el7.elrepo.x86_64.rpm
```

## 3.2 所有节点安装内核

```
cd /root && yum localinstall -y kernel-ml*
```

## 3.3 所有节点更改内核启动顺序

```shell
grub2-set-default 0 && grub2-mkconfig -o /etc/grub2.cfg
grubby --args="user_namespace.enable=1" --update-kernel="$(grubby --default-kernel)"
```

## 3.4 检查默认内核

```shell
 ~]# grubby --default-kernel

/boot/vmlinuz-4.19.12-1.el7.elrepo.x86_64
```

## 3.5 重启所有节点并检查内核版本

```shell
~]# uname -a
Linux k8s-master02 4.19.12-1.el7.elrepo.x86_64 #1 SMP Fri Dec 21 11:06:36 EST 2018 x86_64 x86_64 x86_64 GNU/Linux
```

# 4 配置ipvs并安装ipvsadm

## 4.2 安装ipvsadm

```shell
yum install ipvsadm ipset sysstat conntrack libseccomp -y
```

## 4.3 配置ipvs

```shell
vim /etc/modules-load.d/ipvs.conf 
# 加入以下内容
ip_vs
ip_vs_lc
ip_vs_wlc
ip_vs_rr
ip_vs_wrr
ip_vs_lblc
ip_vs_lblcr
ip_vs_dh
ip_vs_sh
ip_vs_fo
ip_vs_nq
ip_vs_sed
ip_vs_ftp
ip_vs_sh
nf_conntrack
#在内核4.19+版本nf_conntrack_ipv4已经改为nf_conntrack， 4.18以下使用nf_conntrack_ipv4即可
ip_tables
ip_set
xt_set
ipt_set
ipt_rpfilter
ipt_REJECT
ipip
```

## 4.4 启动ipvs

```shell
systemctl enable --now systemd-modules-load.service
```

# 5 修改k8s相关内核参数

## 5.1 修改内核参数

+ 所有节点配置k8s内核：

```shell
cat <<EOF > /etc/sysctl.d/k8s.conf
net.ipv4.ip_forward = 1
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-ip6tables = 1
fs.may_detach_mounts = 1
vm.overcommit_memory=1
vm.panic_on_oom=0
fs.inotify.max_user_watches=89100
fs.file-max=52706963
fs.nr_open=52706963
net.netfilter.nf_conntrack_max=2310720

net.ipv4.tcp_keepalive_time = 600
net.ipv4.tcp_keepalive_probes = 3
net.ipv4.tcp_keepalive_intvl =15
net.ipv4.tcp_max_tw_buckets = 36000
net.ipv4.tcp_tw_reuse = 1
net.ipv4.tcp_max_orphans = 327680
net.ipv4.tcp_orphan_retries = 3
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_max_syn_backlog = 16384
net.ipv4.ip_conntrack_max = 65536
net.ipv4.tcp_max_syn_backlog = 16384
net.ipv4.tcp_timestamps = 0
net.core.somaxconn = 16384
EOF
sysctl --system
```

## 5.2 重启服务器，保证重启后内核依旧加载

```shell
reboot
lsmod | grep --color=auto -e ip_vs -e nf_conntrack
```

# 6 安装基本组件

## 6.1 安装docker

```shell
yum install docker-ce-19.03.* docker-cli-19.03.* -y
```

## 6.2 修改docker的CgroupDriver

+ 由于新版kubelet建议使用systemd，所以可以把docker的CgroupDriver改成systemd

```shell
mkdir /etc/docker
cat > /etc/docker/daemon.json <<EOF
{
  "exec-opts": ["native.cgroupdriver=systemd"]
}
EOF
systemctl enable --now docker.service 
```

## 6.3 安装k8s基础组件

### 6.3.1 所有节点安装kubeadm、kubectl、kubelet

```shell
yum install kubeadm-1.20* kubelet-1.20* kubectl-1.20* -y
```

### 6.3.2 修改kubeadm镜像源

+ 默认配置的pause镜像使用gcr.io仓库，国内可能无法访问，所以这里配置Kubelet使用阿里云的pause镜像：

```shell
cat >/etc/sysconfig/kubelet<<EOF
KUBELET_EXTRA_ARGS="--cgroup-driver=systemd --pod-infra-container-image=registry.cn-hangzhou.aliyuncs.com/google_containers/pause-amd64:3.2"
EOF
```

### 6.3.3 设置kubelet开机启动

```shell
systemctl daemon-reload
systemctl enable --now kubelet	
```

# 7 安装keepalived、haproxy

## 7.1 Master节点安装HAProxy和KeepAlived

```shell
yum install keepalived haproxy -y
```

## 7.2 节点配置HAProxy

### 7.2.1 修改全局配置

+ 所有master节点使用相同配置

```shell
]# vim /etc/haproxy/haproxy.cfg 

global
  maxconn  2000
  ulimit-n  16384
  log  127.0.0.1 local0 err
  stats timeout 30s

defaults
  log global
  mode  http
  option  httplog
  timeout connect 5000
  timeout client  50000
  timeout server  50000
  timeout http-request 15s
  timeout http-keep-alive 15s

frontend monitor-in
  bind *:33305
  mode http
  option httplog
  monitor-uri /monitor

frontend k8s-master
  bind 0.0.0.0:16443
  bind 127.0.0.1:16443
  mode tcp
  option tcplog
  tcp-request inspect-delay 5s
  default_backend k8s-master

backend k8s-master
  mode tcp
  option tcplog
  option tcp-check
  balance roundrobin
  default-server inter 10s downinter 5s rise 2 fall 2 slowstart 60s maxconn 250 maxqueue 256 weight 100
  server master1	172.18.20.1:6443  check
  server master2	172.18.20.2:6443  check
  server master3	172.18.20.3:6443  check
```

### 7.2.2 修改节点配置

+ 每个节点配置不同，需要修改节点ip、网卡名

```shell
~]# vim /etc/keepalived/keepalived.conf 

! Configuration File for keepalived
global_defs {
    router_id LVS_DEVEL
script_user root
    enable_script_security
}
vrrp_script chk_apiserver {
    script "/etc/keepalived/check_apiserver.sh"
    # 检测脚本位置
    interval 5
    weight -5
    fall 2  
rise 1
}
vrrp_instance VI_1 {
    state MASTER
    interface ens33 # 网卡名
    mcast_src_ip # 当前节点IP
    virtual_router_id 51
    priority 101
    # 当前节点vip的优先级（vip优先在数字大的节点上绑定）
    advert_int 2
    authentication {
        auth_type PASS
        auth_pass K8SHA_KA_AUTH
    }
    virtual_ipaddress {
        192.168.0.236
        # VIP
    }
    track_script {
       chk_apiserver
    }
}
```

### 7.2.3 配置健康检查脚本

```shell
~]# cat /etc/keepalived/check_apiserver.sh 
#!/bin/bash

err=0
for k in $(seq 1 3)
do
    check_code=$(pgrep haproxy)
    if [[ $check_code == "" ]]; then
        err=$(expr $err + 1)
        sleep 1
        continue
    else
        err=0
        break
    fi
done

if [[ $err != "0" ]]; then
    echo "systemctl stop keepalived"
    /usr/bin/systemctl stop keepalived
    exit 1
else
    exit 0
fi
```

```shell
~]# chmod +x /etc/keepalived/check_apiserver.sh
```

## 7.3 启动haproxy和keepalived

```shell\
~]# systemctl daemon-reload 
~]# systemctl enable --now keepalived haproxy
```

# 8 集群初始化

## 8.1 Master1节点创建kubeadm-config.yaml

+ 宿主机网段、podSubnet网段、serviceSubnet网段不能重复

```yaml
apiVersion: kubeadm.k8s.io/v1beta2
bootstrapTokens:
- groups:
  - system:bootstrappers:kubeadm:default-node-token
  token: 7t2weq.bjbawausm0jaxury
  ttl: 24h0m0s
  usages:
  - signing
  - authentication
kind: InitConfiguration
localAPIEndpoint:
  advertiseAddress: 172.18.20.1
  bindPort: 6443
nodeRegistration:
  criSocket: /var/run/dockershim.sock
  name: master1
  taints:
  - effect: NoSchedule
    key: node-role.kubernetes.io/master
---
apiServer:
  certSANs:
  - 172.18.20.0
  timeoutForControlPlane: 4m0s
apiVersion: kubeadm.k8s.io/v1beta2
certificatesDir: /etc/kubernetes/pki
clusterName: kubernetes
controlPlaneEndpoint: 172.18.20.0:16443 # vip
controllerManager: {}
dns:
  type: CoreDNS
etcd:
  local:
    dataDir: /var/lib/etcd
imageRepository: registry.cn-hangzhou.aliyuncs.com/google_containers
kind: ClusterConfiguration
kubernetesVersion: v1.20.0
networking:
  dnsDomain: cluster.local
  podSubnet: 172.168.0.0/12
  serviceSubnet: 10.96.0.0/12
scheduler: {}
```

## 8.2 更新kubeadm文件

```shell
kubeadm config migrate --old-config kubeadm-config.yaml --new-config new.yaml
```

## 8.3 所有节点设置开机自启动kubelet

```shell
systemctl enable --now kubelet
```

## 8.4 节点初始化

### 8.4.1 初始化master节点


```shell
kubeadm init --config /root/new.yaml  --upload-certs
```

+ 如果初始化失败，重置后再次初始化，命令如下：

```shell
kubeadm reset -f ; ipvsadm --clear  ; rm -rf ~/.kube
```

### 8.4.2 配置环境变量，访问Kubernetes集群：

```shell
cat <<EOF >> /root/.bashrc
export KUBECONFIG=/etc/kubernetes/admin.conf
EOF
source /root/.bashrc
```

### 8.4.3 查看节点状态

```she
~]# kubectl get nodes
NAME           STATUS     ROLES                  AGE   VERSION
k8s-master01   NotReady   control-plane,master   84m   v1.20.11
```

## 8.5 初始化其他master节点

+ 以下步骤是上述init命令产生的Token过期了才需要执行以下步骤，如果没有过期不需要执行

```shell
#Token过期后生成新的token：
kubeadm token create --print-join-command
#Master需要生成--certificate-key
kubeadm init phase upload-certs  --upload-certs
```

+ 初始化其他master加入集群

```shell
kubeadm join 192.168.0.236:16443 --token fgtxr1.bz6dw1tci1kbj977     --discovery-token-ca-cert-hash sha256:06ebf46458a41922ff1f5b3bc49365cf3dd938f1a7e3e4a8c8049b5ec5a3aaa5 \
    --control-plane --certificate-key 03f99fb57e8d5906e4b18ce4b737ce1a055de1d144ab94d3cdcf351dfcd72a8b
```

## 8.6 Node节点的配置

```shell
kubeadm join 192.168.0.236:16443 --token 7t2weq.bjbawausm0jaxury \
    --discovery-token-ca-cert-hash sha256:8c92ecb336be2b9372851a9af2c7ca1f7f60c12c68f6ffe1eb513791a1b8a908
```

# 9 部署dashboard

## 9.1Metrics部署

+ 新版的Kubernetes中系统资源的采集均使用Metrics-server，可以通过Metrics采集节点和Pod的内存、磁盘、CPU和网络的使用率。

### 9.1.1  复制crt文件

+ 将Maste01节点的front-proxy-ca.crt复制到所有Node节点

```shell
scp /etc/kubernetes/pki/front-proxy-ca.crt node1:/etc/kubernetes/pki/front-proxy-ca.crt
scp /etc/kubernetes/pki/front-proxy-ca.crt nodeX(其他节点自行拷贝):/etc/kubernetes/pki/front-proxy-ca.crt
```

### 9.1.2 安装metrics server

```yaml
[root@master1 ~]# cat /root/k8s-ha-install/metrics-server-0.4.x-kubeadm/comp.yaml 
apiVersion: v1
kind: ServiceAccount
metadata:
  labels:
    k8s-app: metrics-server
  name: metrics-server
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  labels:
    k8s-app: metrics-server
    rbac.authorization.k8s.io/aggregate-to-admin: "true"
    rbac.authorization.k8s.io/aggregate-to-edit: "true"
    rbac.authorization.k8s.io/aggregate-to-view: "true"
  name: system:aggregated-metrics-reader
rules:
  - apiGroups:
      - metrics.k8s.io
    resources:
      - pods
      - nodes
    verbs:
      - get
      - list
      - watch
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  labels:
    k8s-app: metrics-server
  name: system:metrics-server
rules:
  - apiGroups:
      - ""
    resources:
      - pods
      - nodes
      - nodes/stats
      - namespaces
      - configmaps
    verbs:
      - get
      - list
      - watch
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  labels:
    k8s-app: metrics-server
  name: metrics-server-auth-reader
  namespace: kube-system
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: extension-apiserver-authentication-reader
subjects:
  - kind: ServiceAccount
    name: metrics-server
    namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  labels:
    k8s-app: metrics-server
  name: metrics-server:system:auth-delegator
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: system:auth-delegator
subjects:
  - kind: ServiceAccount
    name: metrics-server
    namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  labels:
    k8s-app: metrics-server
  name: system:metrics-server
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: system:metrics-server
subjects:
  - kind: ServiceAccount
    name: metrics-server
    namespace: kube-system
---
apiVersion: v1
kind: Service
metadata:
  labels:
    k8s-app: metrics-server
  name: metrics-server
  namespace: kube-system
spec:
  ports:
    - name: https
      port: 443
      protocol: TCP
      targetPort: https
  selector:
    k8s-app: metrics-server
---
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    k8s-app: metrics-server
  name: metrics-server
  namespace: kube-system
spec:
  selector:
    matchLabels:
      k8s-app: metrics-server
  strategy:
    rollingUpdate:
      maxUnavailable: 0
  template:
    metadata:
      labels:
        k8s-app: metrics-server
    spec:
      containers:
        - args:
            - --cert-dir=/tmp
            - --secure-port=4443
            - --metric-resolution=30s
            - --kubelet-insecure-tls
            - --kubelet-preferred-address-types=InternalIP,ExternalIP,Hostname
            - --requestheader-client-ca-file=/etc/kubernetes/pki/front-proxy-ca.crt # change to front-proxy-ca.crt for kubeadm
            - --requestheader-username-headers=X-Remote-User
            - --requestheader-group-headers=X-Remote-Group
            - --requestheader-extra-headers-prefix=X-Remote-Extra-
          image: registry.cn-beijing.aliyuncs.com/dotbalo/metrics-server:v0.4.1
          imagePullPolicy: IfNotPresent
          livenessProbe:
            failureThreshold: 3
            httpGet:
              path: /livez
              port: https
              scheme: HTTPS
            periodSeconds: 10
          name: metrics-server
          ports:
            - containerPort: 4443
              name: https
              protocol: TCP
          readinessProbe:
            failureThreshold: 3
            httpGet:
              path: /readyz
              port: https
              scheme: HTTPS
            periodSeconds: 10
          securityContext:
            readOnlyRootFilesystem: true
            runAsNonRoot: true
            runAsUser: 1000
          volumeMounts:
            - mountPath: /tmp
              name: tmp-dir
            - name: ca-ssl
              mountPath: /etc/kubernetes/pki
      nodeSelector:
        kubernetes.io/os: linux
      priorityClassName: system-cluster-critical
      serviceAccountName: metrics-server
      volumes:
        - emptyDir: {}
          name: tmp-dir
        - name: ca-ssl
          hostPath:
            path: /etc/kubernetes/pki
---
apiVersion: apiregistration.k8s.io/v1
kind: APIService
metadata:
  labels:
    k8s-app: metrics-server
  name: v1beta1.metrics.k8s.io
spec:
  group: metrics.k8s.io
  groupPriorityMinimum: 100
  insecureSkipTLSVerify: true
  service:
    name: metrics-server
    namespace: kube-system
  version: v1beta1
  versionPriority: 100
```

```shell
~ ]# kubectl  create -f comp.yaml 
```

### 9.1.3 查看状态

```shell
 ~]# kubectl  top node
NAME      CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%   
master1   993m         24%    1530Mi          40%       
master2   983m         24%    1109Mi          29%       
master3   1091m        27%    1246Mi          32%       
node1     496m         12%    820Mi           21%       
node2     434m         10%    772Mi           20%    
```

## 9.2 Dashboard部署

+ Dashboard用于展示集群中的各类资源，同时也可以通过Dashboard实时查看Pod的日志和在容器中执行一些命令等。

### 9.2.1  安装最新版本dashboard

官方GitHub地址：https://github.com/kubernetes/dashboard

+ 可以在官方dashboard查看到最新版dashboard

```shell
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.3/aio/deploy/recommended.yaml
```

### 9.2.2 创建管理员用户

```shell
 ~]# cat admin.yaml

apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding 
metadata: 
  name: admin-user
  annotations:
    rbac.authorization.kubernetes.io/autoupdate: "true"
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kube-system
```

```shell
kubectl apply -f admin.yaml -n kube-system
```

### 9.2.3 登录dashboard

+ 将ClusterIP更改为NodePort

```shell
kubectl edit svc kubernetes-dashboard -n kubernetes-dashboard
```

![image-20211025125947184](kubeadm安装k8s.assets/image-20211025125947184-16383308561871.png)

+ 查看端口号：

```shell
kubectl get svc kubernetes-dashboard -n kubernetes-dashboard
```

![image-20211025125955102](kubeadm安装k8s.assets/image-20211025125955102.png)

+ 查看token值

```shell
~]# kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | awk '{print $1}')
Name:         admin-user-token-r4vcp
Namespace:    kube-system
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: admin-user
              kubernetes.io/service-account.uid: 2112796c-1c9e-11e9-91ab-000c298bf023

Type:  kubernetes.io/service-account-token

Data
====
ca.crt:     1025 bytes
namespace:  11 bytes
token:      eyJhbGciOiJSUzI1NiIsImtpZCI6IiJ9.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlLXN5c3RlbSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJhZG1pbi11c2VyLXRva2VuLXI0dmNwIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6ImFkbWluLXVzZXIiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiIyMTEyNzk2Yy0xYzllLTExZTktOTFhYi0wMDBjMjk4YmYwMjMiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6a3ViZS1zeXN0ZW06YWRtaW4tdXNlciJ9.bWYmwgRb-90ydQmyjkbjJjFt8CdO8u6zxVZh-19rdlL_T-n35nKyQIN7hCtNAt46u6gfJ5XXefC9HsGNBHtvo_Ve6oF7EXhU772aLAbXWkU1xOwQTQynixaypbRIas_kiO2MHHxXfeeL_yYZRrgtatsDBxcBRg-nUQv4TahzaGSyK42E_4YGpLa3X3Jc4t1z0SQXge7lrwlj8ysmqgO4ndlFjwPfvg0eoYqu9Qsc5Q7tazzFf9mVKMmcS1ppPutdyqNYWL62P1prw_wclP0TezW1CsypjWSVT4AuJU8YmH8nTNR1EXn8mJURLSjINv6YbZpnhBIPgUGk1JYVLcn47w
```

# 10 修改为ipvs模式

## 10.1 修改yaml文件

+ 将Kube-proxy改为ipvs模式，因为在初始化集群的时候注释了ipvs配置，所以需要自行修改一下：

```shell
kubectl edit cm kube-proxy -n kube-system
# 修改mode字段值为“ipvs”
```

### 10.2 更新Kube-Proxy的Pod：

```shell
kubectl patch daemonset kube-proxy -p "{\"spec\":{\"template\":{\"metadata\":{\"annotations\":{\"date\":\"`date +'%s'`\"}}}}}" -n kube-system
```

## 10.3 验证Kube-Proxy模式

```shell
~]# curl 127.0.0.1:10249/proxyMode

ipvs
```



