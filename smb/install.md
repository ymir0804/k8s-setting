# SMB

# CSI driver 설치
```
curl -skSL https://raw.githubusercontent.com/kubernetes-csi/csi-driver-smb/v1.17.0/deploy/install-driver.sh | bash -s v1.17.0 --
```

# SMB 계정정보 생성
```
kubectl create secret generic smbcreds --from-literal username=USERNAME --from-literal password="PASSWORD"
```

# storage class 생성
```
kubectl create -f smb_storage_class.yaml
```

# 설치 후 확인
```
kubectl -n kube-system get pod -o wide --watch -l app=csi-smb-controller
kubectl -n kube-system get pod -o wide --watch -l app=csi-smb-node
```

# 설치 시 주의 사항
- source 값에는 \\SMB서버주소\디렉토리 경로값으로 지정해줘야함