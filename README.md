# k3s. Нет доступа к интернету из pod

У меня имеется кластер из 1 master-node и 2 worker-node
```bash
kubectl get nodes
```
```console
NAME                       STATUS   ROLES                  AGE    VERSION
k3s-master-01              Ready    control-plane,master   114m   v1.25.6+k3s1
1960955-cr63564.twc1.net   Ready    <none>                 15m    v1.27.5+k3s1
dimweb-b560-hd3            Ready    worker                 38m    v1.27.5+k3s1
```

```bash
kubectl describe node
```
<details>
  <summary>
    Информация о всех нодах
  </summary>
  
  ```console
  Name:               k3s-master-01
  Roles:              control-plane,master
  Labels:             beta.kubernetes.io/arch=amd64
                      beta.kubernetes.io/instance-type=k3s
                      beta.kubernetes.io/os=linux
                      egress.k3s.io/cluster=true
                      kubernetes.io/arch=amd64
                      kubernetes.io/hostname=k3s-master-01
                      kubernetes.io/os=linux
                      node-role.kubernetes.io/control-plane=true
                      node-role.kubernetes.io/master=true
                      node.kubernetes.io/instance-type=k3s
                      server_type=master
  Annotations:        flannel.alpha.coreos.com/backend-data: {"VNI":1,"VtepMAC":"16:05:4a:ed:ac:85"}
                      flannel.alpha.coreos.com/backend-type: vxlan
                      flannel.alpha.coreos.com/kube-subnet-manager: true
                      flannel.alpha.coreos.com/public-ip: 90.156.226.73
                      k3s.io/hostname: k3s-master-01
                      k3s.io/internal-ip: 90.156.226.73
                      k3s.io/node-args: ["server","--disable","traefik","--write-kubeconfig-mode","644","--node-name","k3s-master-01"]
                      k3s.io/node-config-hash: AP4HSPWZKYNSF3R5O3HSKAAB7TJIPDVHJMVRAHRD5C4VIXFKCTXA====
                      k3s.io/node-env: {"K3S_DATA_DIR":"/var/lib/rancher/k3s/data/630c40ff866a3db218a952ebd4fd2a5cfe1543a1a467e738cb46a2ad4012d6f1"}
                      node.alpha.kubernetes.io/ttl: 0
                      volumes.kubernetes.io/controller-managed-attach-detach: true
  CreationTimestamp:  Wed, 13 Sep 2023 12:37:01 +0300
  Taints:             <none>
  Unschedulable:      false
  Lease:
    HolderIdentity:  k3s-master-01
    AcquireTime:     <unset>
    RenewTime:       Wed, 13 Sep 2023 14:29:49 +0300
  Conditions:
    Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
    ----             ------  -----------------                 ------------------                ------                       -------
    MemoryPressure   False   Wed, 13 Sep 2023 14:27:04 +0300   Wed, 13 Sep 2023 12:37:00 +0300   KubeletHasSufficientMemory   kubelet has sufficient memory available
    DiskPressure     False   Wed, 13 Sep 2023 14:27:04 +0300   Wed, 13 Sep 2023 12:37:00 +0300   KubeletHasNoDiskPressure     kubelet has no disk pressure
    PIDPressure      False   Wed, 13 Sep 2023 14:27:04 +0300   Wed, 13 Sep 2023 12:37:00 +0300   KubeletHasSufficientPID      kubelet has sufficient PID available
    Ready            True    Wed, 13 Sep 2023 14:27:04 +0300   Wed, 13 Sep 2023 12:37:09 +0300   KubeletReady                 kubelet is posting ready status. AppArmor enabled
  Addresses:
    InternalIP:  90.156.226.73
    Hostname:    k3s-master-01
  Capacity:
    cpu:                2
    ephemeral-storage:  51506508Ki
    hugepages-1Gi:      0
    hugepages-2Mi:      0
    memory:             3912Mi
    pods:               110
  Allocatable:
    cpu:                2
    ephemeral-storage:  50105530944
    hugepages-1Gi:      0
    hugepages-2Mi:      0
    memory:             3912Mi
    pods:               110
  System Info:
    Machine ID:                 30a6a96a8b464228bec9eb4d0466688d
    System UUID:                8bf3dc01-ae6a-4d18-9b46-134562f0c7ad
    Boot ID:                    295b3fb4-a371-48db-b38d-c99c8d100818
    Kernel Version:             5.15.0-83-generic
    OS Image:                   Ubuntu 22.04.3 LTS
    Operating System:           linux
    Architecture:               amd64
    Container Runtime Version:  containerd://1.6.15-k3s1
    Kubelet Version:            v1.25.6+k3s1
    Kube-Proxy Version:         v1.25.6+k3s1
  PodCIDR:                      10.42.0.0/24
  PodCIDRs:                     10.42.0.0/24
  ProviderID:                   k3s://k3s-master-01
  Non-terminated Pods:          (15 in total)
    Namespace                   Name                                             CPU Requests  CPU Limits  Memory Requests  Memory Limits  Age
    ---------                   ----                                             ------------  ----------  ---------------  -------------  ---
    kube-system                 coredns-597584b69b-7r6bt                         100m (5%)     0 (0%)      70Mi (1%)        170Mi (4%)     112m
    cert-manager                cert-manager-74d949c895-vqpqm                    0 (0%)        0 (0%)      0 (0%)           0 (0%)         89m
    default                     traefik-69464d9c8b-67vfd                         0 (0%)        0 (0%)      0 (0%)           0 (0%)         93m
    kube-system                 nvidia-device-plugin-daemonset-s7dwk             0 (0%)        0 (0%)      0 (0%)           0 (0%)         35m
    kube-system                 svclb-traefik-9e9846aa-dfkqs                     0 (0%)        0 (0%)      0 (0%)           0 (0%)         93m
    cert-manager                cert-manager-cainjector-d9bc5979d-52bgp          0 (0%)        0 (0%)      0 (0%)           0 (0%)         89m
    kube-system                 local-path-provisioner-79f67d76f8-4tpkv          0 (0%)        0 (0%)      0 (0%)           0 (0%)         112m
    default                     lingvo-gap-back-deployment-7d468b5945-7qhln      300m (15%)    300m (15%)  512Mi (13%)      512Mi (13%)    76m
    default                     lingvo-gap-back-deployment-7d468b5945-wdm4k      300m (15%)    300m (15%)  512Mi (13%)      512Mi (13%)    76m
    default                     lingvo-gap-front-deployment-57cc6fdf76-p5pgg     100m (5%)     100m (5%)   128Mi (3%)       128Mi (3%)     76m
    default                     lingvo-gap-front-deployment-57cc6fdf76-ffb6d     100m (5%)     100m (5%)   128Mi (3%)       128Mi (3%)     76m
    cert-manager                cert-manager-webhook-84b7ddd796-dz278            0 (0%)        0 (0%)      0 (0%)           0 (0%)         89m
    gitlab-agent-kuber-master   kuber-master-gitlab-agent-v1-78487c59cc-kktxb    0 (0%)        0 (0%)      0 (0%)           0 (0%)         95m
    gitlab-agent-kuber-master   kuber-master-gitlab-agent-v1-78487c59cc-sq8nr    0 (0%)        0 (0%)      0 (0%)           0 (0%)         95m
    kube-system                 metrics-server-5f9f776df5-9dhzx                  100m (5%)     0 (0%)      70Mi (1%)        0 (0%)         112m
  Allocated resources:
    (Total limits may be over 100 percent, i.e., overcommitted.)
    Resource           Requests      Limits
    --------           --------      ------
    cpu                1 (50%)       800m (40%)
    memory             1420Mi (36%)  1450Mi (37%)
    ephemeral-storage  0 (0%)        0 (0%)
    hugepages-1Gi      0 (0%)        0 (0%)
    hugepages-2Mi      0 (0%)        0 (0%)
  Events:
    Type     Reason                   Age                  From                   Message
    ----     ------                   ----                 ----                   -------
    Normal   Starting                 33m                  kube-proxy             
    Normal   Starting                 48m                  kube-proxy             
    Normal   Starting                 77m                  kube-proxy             
    Normal   Starting                 89m                  kube-proxy             
    Normal   Starting                 112m                 kube-proxy             
    Normal   Starting                 113m                 kubelet                Starting kubelet.
    Warning  InvalidDiskCapacity      113m                 kubelet                invalid capacity 0 on image filesystem
    Warning  InvalidDiskCapacity      112m                 kubelet                invalid capacity 0 on image filesystem
    Normal   Starting                 112m                 kubelet                Starting kubelet.
    Normal   NodeHasNoDiskPressure    112m (x2 over 112m)  kubelet                Node k3s-master-01 status is now: NodeHasNoDiskPressure
    Normal   NodeHasSufficientMemory  112m (x2 over 112m)  kubelet                Node k3s-master-01 status is now: NodeHasSufficientMemory
    Normal   NodeHasSufficientPID     112m (x2 over 112m)  kubelet                Node k3s-master-01 status is now: NodeHasSufficientPID
    Normal   Synced                   112m                 cloud-node-controller  Node synced successfully
    Normal   NodeAllocatableEnforced  112m                 kubelet                Updated Node Allocatable limit across pods
    Normal   RegisteredNode           112m                 node-controller        Node k3s-master-01 event: Registered Node k3s-master-01 in Controller
    Normal   NodeReady                112m                 kubelet                Node k3s-master-01 status is now: NodeReady
    Normal   Starting                 90m                  kubelet                Starting kubelet.
    Normal   NodeAllocatableEnforced  90m                  kubelet                Updated Node Allocatable limit across pods
    Warning  InvalidDiskCapacity      90m                  kubelet                invalid capacity 0 on image filesystem
    Normal   NodeHasSufficientMemory  89m                  kubelet                Node k3s-master-01 status is now: NodeHasSufficientMemory
    Normal   NodeHasNoDiskPressure    89m                  kubelet                Node k3s-master-01 status is now: NodeHasNoDiskPressure
    Normal   NodeHasSufficientPID     89m                  kubelet                Node k3s-master-01 status is now: NodeHasSufficientPID
    Normal   RegisteredNode           89m                  node-controller        Node k3s-master-01 event: Registered Node k3s-master-01 in Controller
    Normal   Starting                 77m                  kubelet                Starting kubelet.
    Warning  InvalidDiskCapacity      77m                  kubelet                invalid capacity 0 on image filesystem
    Normal   NodeAllocatableEnforced  77m                  kubelet                Updated Node Allocatable limit across pods
    Normal   NodeHasSufficientPID     77m                  kubelet                Node k3s-master-01 status is now: NodeHasSufficientPID
    Normal   NodeHasSufficientMemory  77m                  kubelet                Node k3s-master-01 status is now: NodeHasSufficientMemory
    Normal   NodeHasNoDiskPressure    77m                  kubelet                Node k3s-master-01 status is now: NodeHasNoDiskPressure
    Normal   RegisteredNode           77m                  node-controller        Node k3s-master-01 event: Registered Node k3s-master-01 in Controller
    Warning  InvalidDiskCapacity      48m                  kubelet                invalid capacity 0 on image filesystem
    Normal   Starting                 48m                  kubelet                Starting kubelet.
    Normal   NodeAllocatableEnforced  48m                  kubelet                Updated Node Allocatable limit across pods
    Normal   NodeHasSufficientPID     48m                  kubelet                Node k3s-master-01 status is now: NodeHasSufficientPID
    Normal   NodeHasSufficientMemory  48m                  kubelet                Node k3s-master-01 status is now: NodeHasSufficientMemory
    Normal   NodeHasNoDiskPressure    48m                  kubelet                Node k3s-master-01 status is now: NodeHasNoDiskPressure
    Normal   RegisteredNode           48m                  node-controller        Node k3s-master-01 event: Registered Node k3s-master-01 in Controller
    Normal   Starting                 33m                  kubelet                Starting kubelet.
    Warning  InvalidDiskCapacity      33m                  kubelet                invalid capacity 0 on image filesystem
    Normal   NodeAllocatableEnforced  33m                  kubelet                Updated Node Allocatable limit across pods
    Normal   NodeHasSufficientMemory  33m                  kubelet                Node k3s-master-01 status is now: NodeHasSufficientMemory
    Normal   NodeHasNoDiskPressure    33m                  kubelet                Node k3s-master-01 status is now: NodeHasNoDiskPressure
    Normal   NodeHasSufficientPID     33m                  kubelet                Node k3s-master-01 status is now: NodeHasSufficientPID
    Warning  Rebooted                 33m                  kubelet                Node k3s-master-01 has been rebooted, boot id: 295b3fb4-a371-48db-b38d-c99c8d100818
    Normal   RegisteredNode           33m                  node-controller        Node k3s-master-01 event: Registered Node k3s-master-01 in Controller
  
  
  Name:               1960955-cr63564.twc1.net
  Roles:              <none>
  Labels:             beta.kubernetes.io/arch=amd64
                      beta.kubernetes.io/instance-type=k3s
                      beta.kubernetes.io/os=linux
                      kubernetes.io/arch=amd64
                      kubernetes.io/hostname=1960955-cr63564.twc1.net
                      kubernetes.io/os=linux
                      node.kubernetes.io/instance-type=k3s
                      server_type=gpu2
  Annotations:        flannel.alpha.coreos.com/backend-data: {"VNI":1,"VtepMAC":"de:80:8c:6b:02:08"}
                      flannel.alpha.coreos.com/backend-type: vxlan
                      flannel.alpha.coreos.com/kube-subnet-manager: true
                      flannel.alpha.coreos.com/public-ip: 92.255.77.52
                      k3s.io/hostname: 1960955-cr63564.twc1.net
                      k3s.io/internal-ip: 92.255.77.52,2a03:6f00:4::63eb
                      k3s.io/node-args: ["agent"]
                      k3s.io/node-config-hash: NBA6C5I5BTKXVJUSI5SDI3O4FT5NME5CZT6JREYA3QQPQXYJU3LQ====
                      k3s.io/node-env:
                        {"K3S_DATA_DIR":"/var/lib/rancher/k3s/data/8a84c92c5c245778005e7fa2a03c4d84118fde366594fe826bcd7351d8b88d21","K3S_TOKEN":"********","K3S_U...
                      node.alpha.kubernetes.io/ttl: 0
                      volumes.kubernetes.io/controller-managed-attach-detach: true
  CreationTimestamp:  Wed, 13 Sep 2023 14:15:45 +0300
  Taints:             <none>
  Unschedulable:      false
  Lease:
    HolderIdentity:  1960955-cr63564.twc1.net
    AcquireTime:     <unset>
    RenewTime:       Wed, 13 Sep 2023 14:29:53 +0300
  Conditions:
    Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
    ----             ------  -----------------                 ------------------                ------                       -------
    MemoryPressure   False   Wed, 13 Sep 2023 14:27:29 +0300   Wed, 13 Sep 2023 14:15:45 +0300   KubeletHasSufficientMemory   kubelet has sufficient memory available
    DiskPressure     False   Wed, 13 Sep 2023 14:27:29 +0300   Wed, 13 Sep 2023 14:15:45 +0300   KubeletHasNoDiskPressure     kubelet has no disk pressure
    PIDPressure      False   Wed, 13 Sep 2023 14:27:29 +0300   Wed, 13 Sep 2023 14:15:45 +0300   KubeletHasSufficientPID      kubelet has sufficient PID available
    Ready            True    Wed, 13 Sep 2023 14:27:29 +0300   Wed, 13 Sep 2023 14:15:46 +0300   KubeletReady                 kubelet is posting ready status. AppArmor enabled
  Addresses:
    InternalIP:  92.255.77.52
    InternalIP:  2a03:6f00:4::63eb
    Hostname:    1960955-cr63564.twc1.net
  Capacity:
    cpu:                2
    ephemeral-storage:  51506508Ki
    hugepages-1Gi:      0
    hugepages-2Mi:      0
    memory:             4005892Ki
    pods:               110
  Allocatable:
    cpu:                2
    ephemeral-storage:  50105530944
    hugepages-1Gi:      0
    hugepages-2Mi:      0
    memory:             4005892Ki
    pods:               110
  System Info:
    Machine ID:                 30a6a96a8b464228bec9eb4d0466688d
    System UUID:                cc9bbf6f-db8f-4529-b0a5-8c07fcde2681
    Boot ID:                    0aef34e3-2b78-44a9-8cc4-bf50d605cc96
    Kernel Version:             5.15.0-83-generic
    OS Image:                   Ubuntu 22.04.3 LTS
    Operating System:           linux
    Architecture:               amd64
    Container Runtime Version:  containerd://1.7.3-k3s1
    Kubelet Version:            v1.27.5+k3s1
    Kube-Proxy Version:         v1.27.5+k3s1
  PodCIDR:                      10.42.2.0/24
  PodCIDRs:                     10.42.2.0/24
  ProviderID:                   k3s://1960955-cr63564.twc1.net
  Non-terminated Pods:          (3 in total)
    Namespace                   Name                                    CPU Requests  CPU Limits  Memory Requests  Memory Limits  Age
    ---------                   ----                                    ------------  ----------  ---------------  -------------  ---
    kube-system                 svclb-traefik-9e9846aa-zbmwp            0 (0%)        0 (0%)      0 (0%)           0 (0%)         14m
    kube-system                 nvidia-device-plugin-daemonset-n6wsz    0 (0%)        0 (0%)      0 (0%)           0 (0%)         14m
    default                     network-troubleshoot-timeweb-agent      0 (0%)        0 (0%)      0 (0%)           0 (0%)         12m
  Allocated resources:
    (Total limits may be over 100 percent, i.e., overcommitted.)
    Resource           Requests  Limits
    --------           --------  ------
    cpu                0 (0%)    0 (0%)
    memory             0 (0%)    0 (0%)
    ephemeral-storage  0 (0%)    0 (0%)
    hugepages-1Gi      0 (0%)    0 (0%)
    hugepages-2Mi      0 (0%)    0 (0%)
  Events:
    Type     Reason                   Age                From                   Message
    ----     ------                   ----               ----                   -------
    Normal   Starting                 14m                kube-proxy             
    Normal   Synced                   14m                cloud-node-controller  Node synced successfully
    Normal   Starting                 14m                kubelet                Starting kubelet.
    Warning  InvalidDiskCapacity      14m                kubelet                invalid capacity 0 on image filesystem
    Normal   NodeAllocatableEnforced  14m                kubelet                Updated Node Allocatable limit across pods
    Normal   NodeHasSufficientMemory  14m (x2 over 14m)  kubelet                Node 1960955-cr63564.twc1.net status is now: NodeHasSufficientMemory
    Normal   NodeHasNoDiskPressure    14m (x2 over 14m)  kubelet                Node 1960955-cr63564.twc1.net status is now: NodeHasNoDiskPressure
    Normal   NodeHasSufficientPID     14m (x2 over 14m)  kubelet                Node 1960955-cr63564.twc1.net status is now: NodeHasSufficientPID
    Normal   NodeReady                14m                kubelet                Node 1960955-cr63564.twc1.net status is now: NodeReady
    Normal   RegisteredNode           14m                node-controller        Node 1960955-cr63564.twc1.net event: Registered Node 1960955-cr63564.twc1.net in Controller
  
  
  Name:               dimweb-b560-hd3
  Roles:              worker
  Labels:             beta.kubernetes.io/arch=amd64
                      beta.kubernetes.io/instance-type=k3s
                      beta.kubernetes.io/os=linux
                      kubernetes.io/arch=amd64
                      kubernetes.io/hostname=dimweb-b560-hd3
                      kubernetes.io/os=linux
                      node-role.kubernetes.io/worker=gpu1
                      node.kubernetes.io/instance-type=k3s
                      server_type=gpu1
  Annotations:        flannel.alpha.coreos.com/backend-data: {"VNI":1,"VtepMAC":"e2:5c:ef:b8:a4:63"}
                      flannel.alpha.coreos.com/backend-type: vxlan
                      flannel.alpha.coreos.com/kube-subnet-manager: true
                      flannel.alpha.coreos.com/public-ip: 192.168.120.25
                      k3s.io/hostname: dimweb-b560-hd3
                      k3s.io/internal-ip: 192.168.120.25
                      k3s.io/node-args: ["agent"]
                      k3s.io/node-config-hash: NBA6C5I5BTKXVJUSI5SDI3O4FT5NME5CZT6JREYA3QQPQXYJU3LQ====
                      k3s.io/node-env:
                        {"K3S_DATA_DIR":"/var/lib/rancher/k3s/data/8a84c92c5c245778005e7fa2a03c4d84118fde366594fe826bcd7351d8b88d21","K3S_TOKEN":"********","K3S_U...
                      node.alpha.kubernetes.io/ttl: 0
                      volumes.kubernetes.io/controller-managed-attach-detach: true
  CreationTimestamp:  Wed, 13 Sep 2023 13:52:41 +0300
  Taints:             <none>
  Unschedulable:      false
  Lease:
    HolderIdentity:  dimweb-b560-hd3
    AcquireTime:     <unset>
    RenewTime:       Wed, 13 Sep 2023 14:29:52 +0300
  Conditions:
    Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
    ----             ------  -----------------                 ------------------                ------                       -------
    MemoryPressure   False   Wed, 13 Sep 2023 14:27:51 +0300   Wed, 13 Sep 2023 13:52:41 +0300   KubeletHasSufficientMemory   kubelet has sufficient memory available
    DiskPressure     False   Wed, 13 Sep 2023 14:27:51 +0300   Wed, 13 Sep 2023 13:52:41 +0300   KubeletHasNoDiskPressure     kubelet has no disk pressure
    PIDPressure      False   Wed, 13 Sep 2023 14:27:51 +0300   Wed, 13 Sep 2023 13:52:41 +0300   KubeletHasSufficientPID      kubelet has sufficient PID available
    Ready            True    Wed, 13 Sep 2023 14:27:51 +0300   Wed, 13 Sep 2023 13:52:42 +0300   KubeletReady                 kubelet is posting ready status. AppArmor enabled
  Addresses:
    InternalIP:  192.168.120.25
    Hostname:    dimweb-b560-hd3
  Capacity:
    cpu:                12
    ephemeral-storage:  982862268Ki
    hugepages-1Gi:      0
    hugepages-2Mi:      0
    memory:             32723604Ki
    pods:               110
  Allocatable:
    cpu:                12
    ephemeral-storage:  956128413561
    hugepages-1Gi:      0
    hugepages-2Mi:      0
    memory:             32723604Ki
    pods:               110
  System Info:
    Machine ID:                 0ae8c9f50f074ca998bce9960e25a6aa
    System UUID:                03c00218-044d-05cc-9806-420700080009
    Boot ID:                    0abf2458-119d-47b4-bffa-a2900d9c0319
    Kernel Version:             6.2.0-32-generic
    OS Image:                   Ubuntu 22.04.3 LTS
    Operating System:           linux
    Architecture:               amd64
    Container Runtime Version:  containerd://1.7.3-k3s1
    Kubelet Version:            v1.27.5+k3s1
    Kube-Proxy Version:         v1.27.5+k3s1
  PodCIDR:                      10.42.1.0/24
  PodCIDRs:                     10.42.1.0/24
  ProviderID:                   k3s://dimweb-b560-hd3
  Non-terminated Pods:          (3 in total)
    Namespace                   Name                                    CPU Requests  CPU Limits  Memory Requests  Memory Limits  Age
    ---------                   ----                                    ------------  ----------  ---------------  -------------  ---
    kube-system                 nvidia-device-plugin-daemonset-97f88    0 (0%)        0 (0%)      0 (0%)           0 (0%)         35m
    kube-system                 svclb-traefik-9e9846aa-66jxg            0 (0%)        0 (0%)      0 (0%)           0 (0%)         37m
    default                     network-troubleshoot-mygpu              0 (0%)        0 (0%)      0 (0%)           0 (0%)         27m
  Allocated resources:
    (Total limits may be over 100 percent, i.e., overcommitted.)
    Resource           Requests  Limits
    --------           --------  ------
    cpu                0 (0%)    0 (0%)
    memory             0 (0%)    0 (0%)
    ephemeral-storage  0 (0%)    0 (0%)
    hugepages-1Gi      0 (0%)    0 (0%)
    hugepages-2Mi      0 (0%)    0 (0%)
  Events:
    Type     Reason                   Age                From                   Message
    ----     ------                   ----               ----                   -------
    Normal   Starting                 37m                kube-proxy             
    Normal   Starting                 32m                kube-proxy             
    Warning  InvalidDiskCapacity      37m                kubelet                invalid capacity 0 on image filesystem
    Normal   NodeAllocatableEnforced  37m                kubelet                Updated Node Allocatable limit across pods
    Normal   NodeHasSufficientMemory  37m (x2 over 37m)  kubelet                Node dimweb-b560-hd3 status is now: NodeHasSufficientMemory
    Normal   NodeHasNoDiskPressure    37m (x2 over 37m)  kubelet                Node dimweb-b560-hd3 status is now: NodeHasNoDiskPressure
    Normal   NodeHasSufficientPID     37m (x2 over 37m)  kubelet                Node dimweb-b560-hd3 status is now: NodeHasSufficientPID
    Normal   Starting                 37m                kubelet                Starting kubelet.
    Normal   Synced                   37m                cloud-node-controller  Node synced successfully
    Normal   NodeReady                37m                kubelet                Node dimweb-b560-hd3 status is now: NodeReady
    Normal   RegisteredNode           37m                node-controller        Node dimweb-b560-hd3 event: Registered Node dimweb-b560-hd3 in Controller
    Normal   RegisteredNode           33m                node-controller        Node dimweb-b560-hd3 event: Registered Node dimweb-b560-hd3 in Controller
    Normal   Starting                 32m                kubelet                Starting kubelet.
    Normal   NodeAllocatableEnforced  32m                kubelet                Updated Node Allocatable limit across pods
    Normal   NodeHasSufficientMemory  32m (x2 over 32m)  kubelet                Node dimweb-b560-hd3 status is now: NodeHasSufficientMemory
    Normal   NodeHasNoDiskPressure    32m (x2 over 32m)  kubelet                Node dimweb-b560-hd3 status is now: NodeHasNoDiskPressure
    Normal   NodeHasSufficientPID     32m (x2 over 32m)  kubelet                Node dimweb-b560-hd3 status is now: NodeHasSufficientPID
    Warning  Rebooted                 32m                kubelet                Node dimweb-b560-hd3 has been rebooted, boot id: 0abf2458-119d-47b4-bffa-a2900d9c0319
    Warning  InvalidDiskCapacity      32m                kubelet                invalid capacity 0 on image filesystem
  ```
</details>

Потом я дал тег каждому из серверов. Теги названы `gpu1` просто так.
```bash
kubectl label nodes dimweb-b560-hd3 server_type=gpu1
```

```bash
kubectl label nodes 1960955-cr63564.twc1.net server_type=gpu2
```
Потом создал 2 пода с образом busybox, на разных серверах.

```yaml
# network-troubleshoot-mygpu.yaml
apiVersion: v1
kind: Pod
metadata:
  name: network-troubleshoot-mygpu
spec:
  # hostNetwork: true
  containers:
    - name: troubleshoot
      image: busybox
      command: ["sleep", "3600"]
      securityContext:
        privileged: true
        # capabilities:
        #   add: ["NET_ADMIN", "SYS_ADMIN"]
  restartPolicy: Always
  nodeSelector:
    server_type: gpu1
```

```bash
kubectl apply -f ./network-troubleshoot-mygpu.yaml
```

```yaml
# network-troubleshoot-timeweb-agent.yaml
apiVersion: v1
kind: Pod
metadata:
  name: network-troubleshoot-timeweb-agent
spec:
  # hostNetwork: true
  containers:
    - name: troubleshoot
      image: busybox
      command: ["sleep", "3600"]
      securityContext:
        privileged: true
        # capabilities:
        #   add: ["NET_ADMIN", "SYS_ADMIN"]
  restartPolicy: Always
  nodeSelector:
    server_type: gpu2
```

```bash
kubectl apply -f ./network-troubleshoot-timeweb-agent.yaml
```

```bash
kubectl get po
```
```console
NAME                                           READY   STATUS    RESTARTS      AGE
traefik-69464d9c8b-67vfd                       1/1     Running   1 (48m ago)   108m
network-troubleshoot-mygpu                     1/1     Running   0             41m
network-troubleshoot-timeweb-agent             1/1     Running   0             27m
```

```bash
kubectl describe po network-troubleshoot-mygpu network-troubleshoot-timeweb-agent 
```
<details>
  <summary>
    Описание каждого пода
  </summary>

  ```console
  Name:             network-troubleshoot-mygpu
  Namespace:        default
  Priority:         0
  Service Account:  default
  Node:             dimweb-b560-hd3/192.168.120.25
  Start Time:       Wed, 13 Sep 2023 14:05:55 +0300
  Labels:           <none>
  Annotations:      <none>
  Status:           Running
  IP:               10.42.1.18
  IPs:
    IP:  10.42.1.18
  Containers:
    troubleshoot:
      Container ID:  containerd://366636882e893ea081adb5a84b4aa0f7b3f8d8a57901eedbd1baa45bcb92aaef
      Image:         busybox
      Image ID:      docker.io/library/busybox@sha256:3fbc632167424a6d997e74f52b878d7cc478225cffac6bc977eedfe51c7f4e79
      Port:          <none>
      Host Port:     <none>
      Command:
        sleep
        3600
      State:          Running
        Started:      Wed, 13 Sep 2023 14:05:57 +0300
      Ready:          True
      Restart Count:  0
      Environment:    <none>
      Mounts:
        /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-n4msq (ro)
  Conditions:
    Type              Status
    Initialized       True 
    Ready             True 
    ContainersReady   True 
    PodScheduled      True 
  Volumes:
    kube-api-access-n4msq:
      Type:                    Projected (a volume that contains injected data from multiple sources)
      TokenExpirationSeconds:  3607
      ConfigMapName:           kube-root-ca.crt
      ConfigMapOptional:       <nil>
      DownwardAPI:             true
  QoS Class:                   BestEffort
  Node-Selectors:              server_type=gpu1
  Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                               node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
  Events:
    Type     Reason            Age   From               Message
    ----     ------            ----  ----               -------
    Warning  FailedScheduling  43m   default-scheduler  0/2 nodes are available: 2 node(s) didn't match Pod's node affinity/selector. preemption: 0/2 nodes are available: 2 Preemption is not helpful for scheduling.
    Normal   Scheduled         40m   default-scheduler  Successfully assigned default/network-troubleshoot-mygpu to dimweb-b560-hd3
    Normal   Pulling           40m   kubelet            Pulling image "busybox"
    Normal   Pulled            40m   kubelet            Successfully pulled image "busybox" in 1.307685905s (1.307692864s including waiting)
    Normal   Created           40m   kubelet            Created container troubleshoot
    Normal   Started           40m   kubelet            Started container troubleshoot
  
  
  Name:             network-troubleshoot-timeweb-agent
  Namespace:        default
  Priority:         0
  Service Account:  default
  Node:             1960955-cr63564.twc1.net/92.255.77.52
  Start Time:       Wed, 13 Sep 2023 14:16:58 +0300
  Labels:           <none>
  Annotations:      <none>
  Status:           Running
  IP:               10.42.2.4
  IPs:
    IP:  10.42.2.4
  Containers:
    troubleshoot:
      Container ID:  containerd://ef72cd982c1bcd0d89660b30ca98ba669af4cdf9f7222228c74aa7c5eee37940
      Image:         busybox
      Image ID:      docker.io/library/busybox@sha256:3fbc632167424a6d997e74f52b878d7cc478225cffac6bc977eedfe51c7f4e79
      Port:          <none>
      Host Port:     <none>
      Command:
        sleep
        3600
      State:          Running
        Started:      Wed, 13 Sep 2023 14:17:01 +0300
      Ready:          True
      Restart Count:  0
      Environment:    <none>
      Mounts:
        /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-8426w (ro)
  Conditions:
    Type              Status
    Initialized       True 
    Ready             True 
    ContainersReady   True 
    PodScheduled      True 
  Volumes:
    kube-api-access-8426w:
      Type:                    Projected (a volume that contains injected data from multiple sources)
      TokenExpirationSeconds:  3607
      ConfigMapName:           kube-root-ca.crt
      ConfigMapOptional:       <nil>
      DownwardAPI:             true
  QoS Class:                   BestEffort
  Node-Selectors:              server_type=gpu2
  Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                               node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
  Events:
    Type    Reason     Age   From               Message
    ----    ------     ----  ----               -------
    Normal  Scheduled  29m   default-scheduler  Successfully assigned default/network-troubleshoot-timeweb-agent to 1960955-cr63564.twc1.net
    Normal  Pulling    29m   kubelet            Pulling image "busybox"
    Normal  Pulled     29m   kubelet            Successfully pulled image "busybox" in 3.133547021s (3.13355831s including waiting)
    Normal  Created    29m   kubelet            Created container troubleshoot
    Normal  Started    29m   kubelet            Started container troubleshoot
  ```
</details>

Но при выполнении команды ping получаю следующее:

```bash
kubectl exec -it network-troubleshoot-timeweb-agent -- ping google.com
```
```console
PING google.com (108.177.14.138): 56 data bytes
64 bytes from 108.177.14.138: seq=0 ttl=111 time=4.824 ms
64 bytes from 108.177.14.138: seq=1 ttl=111 time=4.532 ms
64 bytes from 108.177.14.138: seq=2 ttl=111 time=4.477 ms
64 bytes from 108.177.14.138: seq=3 ttl=111 time=4.485 ms
^C
--- google.com ping statistics ---
4 packets transmitted, 4 packets received, 0% packet loss
round-trip min/avg/max = 4.477/4.579/4.824 ms
```

Все ок. Доступ есть.

```bash
kubectl exec -it network-troubleshoot-mygpu -- ping google.com
```
```console
ping: bad address 'google.com'
command terminated with exit code 1
```

Доступа нет.

Я искал похожую проблему в интернете. [Can't reach internet from pod / container](https://github.com/k3s-io/k3s/issues/5349). Насколько мне хватило понимая, эта проблема связана с тем, что какие-то порты блокировались провайдером и если их открыть, все решалось.

Мой network-troubleshoot-mygpu запущен у меня дома, как я думал таким провайдером может быть роутер.
![image](https://github.com/dmitrymailk/k3s_pod_network_issue/assets/39678439/7437f891-22e2-4097-b371-44ef93047bd0)
![image](https://github.com/dmitrymailk/k3s_pod_network_issue/assets/39678439/bfb2d26f-4ed6-496b-bc41-b4dd0c15f4ce)

На `network-troubleshoot-mygpu` отключен firewall
```bash
sudo ufw disable
```





