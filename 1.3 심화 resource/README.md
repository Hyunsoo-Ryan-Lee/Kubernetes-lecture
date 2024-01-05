## 1. StatefulSet

- StatefulSet은 순차적인 네이밍 및 안정적인 네트워크 식별자를 가진 Pod를 관리합니다. 주로 데이터베이스, 메시지 큐와 같은 상태를 가진 애플리케이션에 사용됩니다.
- 예제 YAML
```yaml
Copy code
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: my-statefulset
spec:
  replicas: 3
  serviceName: my-statefulset-service
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: nginx
```
## 2. DaemonSet
- DaemonSet은 각 노드에 하나의 Pod 인스턴스를 배포합니다. Logging과 같이 모든 노드에서 실행되어야 하는 백그라운드 작업을 위해 사용됩니다.
- 예제 YAML
```yaml
Copy code
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: my-daemonset
spec:
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: nginx
```
## 3. Job
- Job은 한 번 실행되고 완료되는 작업을 나타냅니다. 주로 일회성 작업 또는 배치 작업을 실행하는 데 사용됩니다.
- 예제 YAML
```yaml
Copy code
apiVersion: batch/v1
kind: Job
metadata:
  name: my-job
spec:
  template:
    spec:
      containers:
      - name: my-container
        image: busybox
        args:
        - /bin/sh
        - -c
        - echo "Hello, Kubernetes!"
      restartPolicy: Never
```
## 4. CronJob
- CronJob은 정기적으로 실행되는 작업을 스케줄링합니다. 주기적인 작업을 실행하는 데 사용됩니다.
- 예제 YAML
```yaml
Copy code
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: my-cronjob
spec:
  schedule: "*/1 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: my-container
            image: busybox
            args:
            - /bin/sh
            - -c
            - echo "Hello, Kubernetes from CronJob!"
          restartPolicy: OnFailure
```
## 5. Horizontal Pod Autoscaler(HPA)
- HPA는 CPU 사용률 또는 기타 지표에 따라 Pod의 수를 자동으로 조절하여 스케일링을 지원합니다.
- 예제 YAML HPA는 별도의 YAML 파일을 사용하지만, Deployment 또는 ReplicaSet과 함께 사용됩니다.
```yaml
Copy code
apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
  name: my-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-deployment  # HPA가 조절할 대상 리소스
  minReplicas: 2  # 최소 복제본 수
  maxReplicas: 5  # 최대 복제본 수
  metrics:
  - type: Resource
    resource:
      name: cpu
      targetAverageUtilization: 70
      # CPU 사용률이 70% 이상이면 Pod 수를 2개에서 5개까지 조절할 수 있도록 설정한 HPA
```

## 기타 리소스
- RBAC : https://velog.io/@newnew_daddy/K8S03
- VOLUMES : https://velog.io/@newnew_daddy/K8S04