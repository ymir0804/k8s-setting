# SMB

## CSI driver 설치
```
curl -skSL https://raw.githubusercontent.com/kubernetes-csi/csi-driver-smb/v1.17.0/deploy/install-driver.sh | bash -s v1.17.0 --
```

## SMB 계정정보 생성
```
kubectl create secret generic smbcreds --from-literal username=USERNAME --from-literal password="PASSWORD"
```

## storage class 생성
```
kubectl create -f https://raw.githubusercontent.com/kubernetes-csi/csi-driver-smb/master/deploy/example/storageclass-smb.yaml
```

## 설치 후 확인
```
kubectl -n kube-system get pod -o wide --watch -l app=csi-smb-controller
kubectl -n kube-system get pod -o wide --watch -l app=csi-smb-node
kubectl apply -f smb-pv.yaml
kubectl apply -f smb-pvc.yaml
kubectl apply -f deployment.yaml

```

## 설치 시 주의 사항
- PV의 해당 옵션을 다음과 같이 넣어줘야함
```
    volumeAttributes:
      source: "//192.168.0.1/mysmb" # //SMB서버/디렉토리
```

## 확인 후 생성한 요소 삭제
```
kubectl delete -f deployment.yaml
kubectl delete -f smb-pvc.yaml
kubectl delete -f smb-pv.yaml
```

[출처](https://www.youtube.com/watch?v=3S5oeB2qhyg)