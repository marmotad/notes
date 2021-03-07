# Master 组件

## API Server,scheduler, Controller-Manager Server

通过API server（k8s集群中唯一接受请求的入口 ）发送指令--->通过Controller运行指令并通过Control loop监控指令监控状态
# Node 组件
## Kube-proxy,Kubelet,Container runtime(docker,rkt,cri-o,frakti),Pod

# Kubernetes Components

>• Master Components
>• kube-apiserver
>• etcd
>• kube-scheduler
>• kube-controller-manager
>• cloud-controller-manager


# Node Components
>• kubelet
>• kube-proxy
>• Container Runtime

## • Addons

>+ DNS
>
>+ CNI (flannel, calico, ...)
>
>+ Web UI (Dashboard)
>
>+ Container Resource Monitoring
>
>+ Cluster-level Logging
>
>+ 监控系统：prometheus
>
>+ 集群日志系统：EFK、LG
>
>+ Ingress Controller

## 对象式编程语言
    以数据为中心，代码服务于数据

## 数据式编程
     以代码为中心，数据服务于代码
     数据：对象
    代码：定义类时定义的方法

## class：类
    属性，方法
    方法限制一类事物的操作接口
    对属性赋值的过程相当于的过程

 




## k8s api：REST API(主要依托Http/Https方法传输)
    resource(资源) --> objet（对象）
     
    method（支持的操作方法）:GET,PUT,POST.DELETE,PATCH,........

## K8s : cluster , 容器编排系统
    核心任务：容器编排
     
    容器：应用程序
     
    Pod Controller，Deployment  #Kube-Proxy
## 功能
    用于修改节点上的ipvs或者iptables规则

## 证书
+ k8s使用双向证书认证

![image-20210307195552049](kuberbetes.assets/image-20210307195552049.png)

# kuberneter部署的两种方式

+ 二进制程序部署
+ Pod部署、
  + Static pod
  + Pod

![image-20210307195832794](kuberbetes.assets/image-20210307195832794.png)

# k8s 两种网络类型

+ overlay：叠加网络

+ underlay：承载网络

![image-20210307200708396](kuberbetes.assets/image-20210307200708396.png)

## CNI Container Network Interface

+ flannel
+ Project Calico
+ Canal（已废弃）

![image-20210307202211029](kuberbetes.assets/image-20210307202211029.png)

## CRI Container Runtime Interface

## CSI Container Storage Interface
