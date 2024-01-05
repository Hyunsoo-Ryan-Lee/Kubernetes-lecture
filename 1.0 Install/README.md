## 0. 참고 문서
> https://velog.io/@newnew_daddy/microk8s

## 1. Single Node
1. docker & docker-compose install
  ```shell
  sudo apt-get update -y &&\
      apt-transport-https &&\
      ca-certificates &&\
      curl &&\
      software-properties-common
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
  sudo apt update
  apt-cache policy docker-ce
  sudo apt install -y docker-ce
  sudo usermod -aG docker $USER

  # install docker-compose
  sudo apt-get install docker-compose-plugin
  ```

2. microk8s install
  ```shell
  sudo apt update

  # hostname change
  sudo hostnamectl set-hostname master

  # microk8s install
  sudo snap install microk8s --classic --channel=1.28
  sudo usermod -a -G microk8s $USER
  sudo chown -f -R $USER ~/.kube
  sudo su - $USER
  
  # (Optional) additional service install
  microk8s enable dashboard
  microk8s enable dns
  microk8s enable registry
  microk8s enable istio

  # alias 설정
  {
      echo alias kc="'microk8s kubectl'"
      echo alias kcd="'microk8s kubectl describe'"
  } >> ~/.bashrc

  source ~/.bashrc
  ```

---
# KUBERNETES ARCHITECTURE
![](https://velog.velcdn.com/images/newnew_daddy/post/d9e6303d-49e7-47f9-84f8-62fa4a44ce9b/image.png)

## 1. Master Node

- kube-apiserver: 클러스터 API를 노출하고 관리하는 중심 API 서버입니다.
- etcd: 클러스터의 모든 상태 정보를 저장하는 분산 데이터 저장소입니다.
- kube-scheduler: Pod를 실행할 노드를 선택하는 스케줄러입니다.
- kube-controller-manager: 클러스터 상태를 계속해서 확인하고 조정하는 여러 개의 컨트롤러를 실행하는 컨트롤러 매니저입니다.

## 2. Worker Node
- kubelet: 마스터 노드에서 받은 명령을 수행하여 노드 상태를 보고하고 컨테이너를 실행합니다.
- kube-proxy: 네트워크 프록시 서비스를 제공하여 서비스의 로드 밸런싱 및 네트워크 규칙 관리를 지원합니다.
- Container Runtime: 컨테이너를 실행하는 데 사용되는 도구 (예: Docker, containerd).

## 3. Addon 및 기타 구성 요소
- DNS 서버 (kube-dns 또는 CoreDNS): 서비스 및 Pod에 대한 DNS 이름 해결을 제공합니다.
- Dashboard: 웹 기반 대시보드를 통해 클러스터 상태 및 리소스 모니터링을 제공합니다.
- Ingress Controller: 클러스터 내에서 HTTP 및 HTTPS 트래픽을 관리하는 역할을 합니다.
- CNI (Container Network Interface): Pod 간의 네트워크 통신을 관리하는 네트워크 인터페이스 플러그인입니다.