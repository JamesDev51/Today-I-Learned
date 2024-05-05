---
title: "k8s 개념 정리"
date: "2024-05-05"
lastmod: "2024-05-05"
summary: "k8s 개념, 용어"
description: "k8s 기본 개념, 용어에 대하여  정리해놓기"
tags: ["k8s", "term"]
categories: ["k8s"]
ShowToc: true
TocOpen: false
---

# 기본 철학
- MSA: 즉 각자의 일을 열심히 한다
- 선언적인 시스템: 추구하는 상태와 현재 상태를 맞추려고 함
- 상태변경  -> 감시 -> 차이 발견

## 파드와 디플로이먼트
- 파드는 죽을 수도 있음 (다시 생성하면 그만이야~)

## 오브젝트
- 추구하는 상태를 가지고 있는 것
- 선언한 상태를 변경하면 현재 상태로 그에 맞춰 변화됨

### 기본 오브젝트
- 종류
  - pod
  - service
  - namespace
    - default
  - volume

### 예약단축어
- nodes: no
- namespaces: ns
- deployments: deploy
- pods: po
- services: svc

# 구성
## 노드 구분
  - 마스터 노드
    - api 서버
      - 상태값 업로드 / 업데이트
    - etcd
      - api 서버의 선언된 값을 기록 (동기화)
    - 컨트롤러 매니저
      - api 서버의 값을 확인하여 값을 변경, 업데이트
    - 스케줄러
      - 스케줄링
  - 워커 노드
    - kubelet
      - 컨테이너 런타임에게 파드 생성 요청
    - 컨테이너 런타임
    - pod
    - kube-proxy

## 용어
- namespace
  - 구역을 나누는 단위
    - default
    - kube-system
    - metallb-system
  - 클라우드 provider의 managed k8s에서도 비슷한 구성 (kube-system)
    - AWS EKS
    - Azure AKS
    - GCP GKE
- cluster
  - 노드들 집합
  - 마스터 노드 + 워커 노드로 구성
- pod
  - 컨테이너의 집합
  - 한 가지 목적을 위해 만들어짐
- deployment
  - 여러 파드의 배포 단위
  - 파드가 모여있음
  - scale 가능 (파드 수)
- volume
  - 지속적으로 저장되어야 하는 곳
  - 파드의 데이터 영속을 위해 사용
- service
  - 클러스터 외부에 안전 구역
  - 항상 거쳐야 하는 곳
- replicaSet
  - 디플로이먼트 내부의 파드 수
-  load balancer
   -  노드의 ip를 직접 노출하지 않고 가상의 ip 사용
 
# 버전 업그레이드
1. 업그레이드 계획 수립
2. kubeadm 업그레이드
3. kubelet 업그레이드
4. 업그레이드 완료 확인
