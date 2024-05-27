---
title: "k8s 명령어 정리"
date: "2024-05-05"
lastmod: "2024-05-05"
description: "k8s 학습하며 알게된 명령어 대충 정리해놓기"
summary: "k8s 명령어"
tags: ["k8s", "command"]
categories: ["k8s"]
ShowToc: true
TocOpen: false
---
# kubectl
- `kubectl `: 쿠버 컨트롤

get
- `kubectl get nodes`: 노드들 확인
- `kubectl get pod`: 파드들 확인
- `kubectl get pod -o wide`: 배포한 파드의 ip 확인
- `kubectl get pod -o wide -w`: watch 명령어. 변화가 생기는 경우 콘솔에 재출력
- `kubectl get service`: 서비스 확인
- `kubectl get pods -n (네임스페이스)`: 네임스페이스로 해당 구역 파드들 확인

run
- `kubectl run (이름) --image=(이미지 이름)`: 실행할 파드명과 이미지명을 명시하여 파드를 실행시킴

expose
- `kubectl expose pod (파드명) --type=NodePort --port=(포트)`: 파드가 떠있는 노드에 직접 포트를 연결하여 외부로 노출
- `kubectl expose deployment (디플로이명) --type=NodePort --port=(포트)`: 디플로이먼트가 떠있는 노드에 직접 포트를 연결하여 외부로 노출
- `kubectl expose deployment (디플로이명) --type=LoadBalancer --port=(포트)`: 디플로이먼트에 선언한 로드밸런서로 포트를 연결하여 외부로 노출

create
- `kubectl create deployment (디플로이명) --image=(이미지명)`: 이미지명과 디플로이명으로 디플로이 배포

apply
- `kubectl apply -f (파일 경로)`: 파일로 선언, 설치

scale
- `kubectl scale deployment (디플로이명) --replica=(파드 수)`: 디플로이먼트 안의 파드 수 설정

delete
- `kubectl delete pod (파드명)`: 파드 삭제
- `kubectl delete deployment (디플로이명)`: 디플로이먼트 삭제
- `kubectl delete service (서비스명)`: 서비스 삭제
- `kubectl delete -f (파일명)`: 파일로 삭제

edit
- `kubectl edit deployment (디플로이명)`: 디플로이의 추구하는 상태를 확인

exec
- `kubectl exec (파드명) -it -- /bin/bash`: 직접 파드 내부에 들어가는 명령어

# k8s 업그레이드
- `kubeadm upgrade plan`: 최신 버전 확인
-  `yum upgrade kubeadm-(버전) -y`: kubeadm에서 upgrade를 진행하기 전에 kubeadm 자체를 해당 버전으로 업그레이드 해줘야 함
- `yum upgrade kubelet-(버전) -y`: kubelet 업그레이드
- `kubeadm upgrade apply`: 실제 노드 업그레이드=