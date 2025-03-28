# NFS

## 모든 노드에 NFS Client 설치
```
sudo apt update && sudo apt install nfs-common -y
```

## NFS Client Provisioner 설치
```
kubectl create namespace nfs-client
helm repo add nfs-subdir-external-provisioner https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner/
helm install nfs-subdir-external-provisioner nfs-subdir-external-provisioner/nfs-subdir-external-provisioner \
--namespace nfs-client \
--set nfs.server=__NAS_IP__ \
--set nfs.path=__NAS_PATH__ \
--set storageClass.name=nfs-client \
--set storageClass.defaultClass=true
# 나의 설정은 __NAS_IP__ 192.168.0.x, __NAS_PATH__ /nfs
```

## 설치 확인
```
kubectl get storageclass
NAME                          PROVISIONER                                     AGE
nfs-client                    cluster.local/nfs-subdir-external-provisioner   5m49s
nks-block-storage (default)   blk.csi.ncloud.com                              3h39m
```

## Default로 지정
```
kubectl patch storageclass nfs-client -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
```

## PV,PVC 확인(Jenkins)
```
helm install ci stable/jenkins
```

[출처 NCP NFS Docs](https://guide.ncloud-docs.com/docs/k8s-k8suse-nfs)