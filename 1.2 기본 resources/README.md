## 1. Pod 
- 가장 기본적인 배포 단위로, 하나 이상의 컨테이너를 포함합니다.
- 예제 YAML
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    tier: frontend
spec:
  containers:
  - name: nginx-container
    image: nginx
```

## 2. ReplicaSet
- 특정 수의 Pod 복제본을 관리하고 유지하는 역할을 하는 리소스로 파드와 레플리카셋(ReplicaSet)에 대한 선언적 업데이트를 제공한다
- 예제 YAML
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-replicaset
spec:
  replicas: 3  # 3개의 Pod 복제본을 유지
  selector:
    matchLabels:
      app: my-app  # Pod 라벨이 'app: my-app'인 것만 관리
  template:
    metadata:
      labels:
        app: my-app  # 생성되는 Pod에 'app: my-app' 라벨 적용
    spec:
      containers:
      - name: my-container
        image: nginx
```

## 3. Deployment
- Pod의 관리와 롤링 업데이트를 관리하는 리소스입니다.
- 예제 YAML
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: nginx
        image: nginx
```
## 4. Service
- 서비스 디스커버리 및 로드 밸런싱을 제공하는 리소스입니다.
- 예제 YAML
```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: ClusterIP / NodePort / LoadBalancer
```
## 5. ConfigMap
- 애플리케이션 설정을 분리하고 구성 관리를 가능하게 하는 리소스입니다.
- 예제 YAML
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  key1: value1
  key2: value2
```
## 6. Secret
- 비밀 정보(패스워드, API 토큰 등)를 안전하게 저장하는 데 사용하는 리소스입니다.
    > kubectl create secret generic ncp-secret-key \
            --from-literal=USER=[KEY_ID] \
            --from-literal=PASSWORD=[KEY_SECRET]
- 예제 YAML
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: dXNlcm5hbWU=  # base64-encoded "username"
  password: cGFzc3dvcmQ=  # base64-encoded "password"
```
## 7. Namespace
- Kubernetes 클러스터 내에서 리소스를 격리하고 구분하는 데 사용하는 가상 클러스터입니다.
- 예제 YAML
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: my-namespace
```
## 8. Ingress
- HTTP 및 HTTPS 트래픽을 애플리케이션으로 라우팅하는 리소스입니다.
- 예제 YAML
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /app
        pathType: Prefix
        backend:
          service:
            name: my-app-service
            port:
              number: 80
```