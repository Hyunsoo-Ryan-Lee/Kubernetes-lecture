## 0. DOCS
> https://jamesdefabia.github.io/docs/user-guide/kubectl/kubectl/

## 1. kubectl run
1. nginx pod 실행
> kc run nginx --image=nginx

2. nginx pod port 선언
> kc run nginx-pod --image=nginx --port=80

3. nginx pod와 service 연결 (ClusterIP)
> kc expose pod nginx-pod --name=svc-cluster

4. nginx pod와 service 연결 (NodePort)
> kc expose pod nginx-pod --type=NodePort --name=svc-nodeport

5. pod 내부로 환경변수 pass
> kubectl run nginx --image=nginx --env="DNS_DOMAIN=cluster" --env="POD_NAMESPACE=default"

6. pod 여러개 올리기
> kubectl run nginx --image=nginx --replicas=5

7. Dry run. Print the corresponding API objects without creating them.
> kubectl run nginx --image=nginx --dry-run



## 2. kubectl get
- 명령어 : kubectl get <리소스 유형>
- 설명 : 클러스터 내의 특정 리소스 유형을 조회합니다.
- 예제 : 
```shell
kubectl get pods : 현재 실행 중인 모든 Pod를 나열합니다.
kubectl get services : 현재 서비스를 나열합니다.
kubectl get nodes : 클러스터의 노드 목록을 나열합니다.
```
## 3. kubectl describe
- 명령어 : kubectl describe <리소스 유형> <리소스 이름>
- 설명 : 특정 리소스의 상세 정보를 표시합니다.
- 예제 : 
```shell
kubectl describe pod my-pod 명령어를 사용하여 "my-pod" Pod의 상세 정보를 확인합니다.
```
## 4. kubectl create
- 명령어 : kubectl create -f <파일명 또는 URL>
- 설명 : YAML 파일 또는 URL에서 정의된 리소스를 생성합니다.
- 예제 : 
```shell
kubectl create -f my-pod.yaml 명령어를 사용하여 "my-pod.yaml" 파일에서 정의된 Pod를 생성합니다.
```
## 5. kubectl apply
- 명령어 : kubectl apply -f <파일명 또는 URL>
- 설명 : YAML 파일 또는 URL에서 정의된 리소스를 생성 또는 업데이트합니다. 리소스가 이미 존재하면 업데이트하고, 없으면 생성합니다.
- 예제 : 
```shell
kubectl apply -f my-deployment.yaml 명령어를 사용하여 "my-deployment.yaml" 파일에서 정의된 Deployment를 생성 또는 업데이트합니다.
```
## 6. kubectl delete
- 명령어 : kubectl delete <리소스 유형> <리소스 이름>
- 설명 : 특정 리소스를 삭제합니다.
- 예제 : 
```shell
kubectl delete pod my-pod 명령어를 사용하여 "my-pod" Pod를 삭제합니다.
```
## 7. kubectl exec
- 명령어 : kubectl exec -it <Pod 이름> -- <명령어>
- 설명 : 실행 중인 Pod 내에서 특정 명령어를 실행합니다.
- 예제 : 
```shell
kubectl exec -it my-pod -- /bin/bash 명령어를 사용하여 "my-pod" Pod 내에서 대화형 쉘을 실행합니다.
```
## 8. kubectl logs
- 명령어 : kubectl logs <Pod 이름>
- 설명 : Pod의 로그를 확인합니다.
- 예제 : 
```shell
kubectl logs my-pod 명령어를 사용하여 "my-pod" Pod의 로그를 출력합니다.
```
## 9. kubectl scale
- 명령어 : kubectl scale --replicas=<개수> <리소스 유형> <리소스 이름>
- 설명 : ReplicaSet, Deployment 등과 같은 리소스의 복제본 수를 조절합니다.
- 예제 : 
```shell
kubectl scale --replicas=3 deployment/my-deployment 명령어를 사용하여 "my-deployment" Deployment의 복제본 수를 3개로 조절합니다.
```