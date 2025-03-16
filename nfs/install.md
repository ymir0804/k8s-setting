# NFS

## NFS Client Provisioner 설치
```
helm repo add nfs-subdir-external-provisioner https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner/

helm install --kubeconfig=$KUBE_CONFIG  nfs-subdir-external-provisioner nfs-subdir-external-provisioner/nfs-subdir-external-provisioner \

--set nfs.server=__NAS_IP__ \
--set nfs.path=__NAS_PATH__
```

## 설치 확인
```
kubectl get storageclass
NAME                          PROVISIONER                                     AGE
nfs-client                    cluster.local/nfs-subdir-external-provisioner   5m49s
nks-block-storage (default)   blk.csi.ncloud.com                              3h39m
```

## PV,PVC 확인(Jenkins)
```
helm install ci stable/jenkins
```

[출처 NCP NFS Docs](https://guide.ncloud-docs.com/docs/k8s-k8suse-nfs)