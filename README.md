# K-PaaS 컨테이너 플랫폼 이미지 빌드

<table>
  <tr>
    <td colspan=2 align=center>플랫폼</td>
    <td colspan=2 align=center><a href="https://github.com/K-PaaS/ap-deployment">어플리케이션 플랫폼</a></td>
    <td colspan=2 align=center><a href="https://github.com/K-PaaS/cp-deployment">컨테이너 플랫폼</a></td>
  </tr>
  <tr>
    <td colspan=2 rowspan=2 align=center>포털</td>
    <td colspan=2 align=center><a href="https://github.com/K-PaaS/portal-deployment">AP 포털</a></td>
    <td colspan=2 align=center><a href="https://github.com/K-PaaS/cp-portal-release">🚩 CP 포털</a></td>
  </tr>
  <tr align=center>
    <td colspan=4><a href="https://github.com/K-PaaS/K-PaaS-Monitoring">모니터링 대시보드</a></td>
  </tr>
  <tr align=center>
    <td rowspan=2 colspan=2><a href="https://github.com/K-PaaS/monitoring-deployment">모니터링</a></td>
    <td><a href="https://github.com/K-PaaS/PaaS-TA-Monitoring-Release">Monitoring</a></td>
    <td><a href="https://github.com/K-PaaS/paas-ta-monitoring-logsearch-release">Logsearch</a></td>
    <td><a href="https://github.com/K-PaaS/paas-ta-monitoring-influxdb-release">InfluxDB</a></td>
    <td><a href="https://github.com/K-PaaS/paas-ta-monitoring-redis-release">Redis</a></td>
  </tr>
  <tr align=center>
    <td><a href="https://github.com/K-PaaS/PAAS-TA-PINPOINT-MONITORING-RELEASE">Pinpoint</td>
    <td><a href="https://github.com/K-PaaS/PAAS-TA-PINPOINT-MONITORING-BUILDPACK">Pinpoint Buildpack</td>
    <td></td>
    <td></td>
  </tr>
  </tr>
  <tr align=center>
    <td rowspan=4 colspan=2><a href="https://github.com/K-PaaS/service-deployment">AP 서비스</a></td>
    <td><a href="https://github.com/K-PaaS/ap-cubrid-release">Cubrid</a></td>
    <td><a href="https://github.com/K-PaaS/ap-api-gateway-release">Gateway</a></td>
    <td><a href="https://github.com/K-PaaS/ap-glusterfs-release">GlusterFS</a></td>
    <td><a href="https://github.com/K-PaaS/ap-app-lifecycle-release">Lifecycle</a></td>
  </tr>
  <tr align=center>
    <td><a href="https://github.com/K-PaaS/ap-logging-release">Logging</a></td>
    <td><a href="https://github.com/K-PaaS/ap-mongodb-release">MongoDB</a></td>
    <td><a href="https://github.com/K-PaaS/ap-mysql-release">MySQL</a></td>
    <td><a href="https://github.com/K-PaaS/ap-pinpoint-release">Pinpoint APM</a></td>
  </tr>
  <tr align=center>
    <td><a href="https://github.com/K-PaaS/ap-delivery-pipeline-release">Pipeline</a></td>
    <td align=center><a href="https://github.com/K-PaaS/rabbitmq-release">RabbitMQ</a></td>
    <td><a href="https://github.com/K-PaaS/ap-on-demand-redis-release">Redis</a></td>
    <td><a href="https://github.com/K-PaaS/ap-source-control-release">Source Control</a></td>
  </tr>
  <tr align=center>
    <td><a href="https://github.com/K-PaaS/ap-web-ide-release">WEB-IDE</a></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr align=center>
    <td rowspan=2 colspan=2><a href="https://github.com/K-PaaS/cp-deployment">CP 서비스</a></td>
    <td><a href="https://github.com/K-PaaS/cp-portal-ui">Portal UI</a></td>
    <td><a href="https://github.com/K-PaaS/cp-portal-api">Portal API</a></td>
    <td><a href="https://github.com/K-PaaS/cp-portal-common-api">Common API</a></td>
    <td><a href="https://github.com/K-PaaS/cp-portal-common-api">Service Broker</a></td>
  </tr>
  <tr align=center>
    <td><a href="https://github.com/K-PaaS/cp-metrics-api">Metric API</a></td>
    <td><a href="https://github.com/K-PaaS/cp-terraman">Terraman API</a></td>
    <td></td>
    <td></td>
  </tr>
</table>
<i>🚩 You are here.</i>

## 소개
컨테이너 플랫폼 프로젝트를 빌드하고 이미지를 생성하여 레파지토리에 이미지를 업로드하는 방법에 대해 기술하였다.
### 사전 설치
- JDK 설치
- Gradle 설치
- Docker 설치

<br>

### 컨테이너 플랫폼 빌드 방법
- K-PaaS 컨테이너 플랫폼 프로젝트의 jar 파일 생성을 위해 빌드를 진행한다.
```
$ gradle build
```

<br>

### 컨테이너 플랫폼 이미지 생성 방법
- 컨테이너 플랫폼 프로젝트 이미지 생성에 필요한 파일을 동일한 디렉토리 내에 위치 시킨다.
- 파일 위치 : <br>
  + 컨테이너 플랫폼 포털
      - [cp-portal-api](portal/cp-portal-api)
      - [cp-portal-common-api](portal/cp-portal-common-api)
      - [cp-portal-webadmin](portal/cp-portal-webadmin)
      - [cp-portal-webuser](portal/cp-portal-webuser)
  + 컨테이너 플랫폼 서비스 브로커
      - [cp-portal-admin-service-broker](service-broker/cp-portal-admin-service-broker)
      - [cp-portal-user-service-broker](service-broker/cp-portal-user-service-broker)  
      - [cp-portal-jenkins-service-broker](service-broker/cp-portal-jenkins-service-broker)  

<br>

> 'cp-portal-api'를 예시로 진행한다.

- 파일 디렉토리 구성
```
├── Dockerfile
├── application.yml
└── cp-portal-api.jar
```
- Dockerfile 확인
```
$ cat Dockerfile
```
```
FROM openjdk:8-jdk-alpine
ARG JAR_FILE=*.jar
COPY ${JAR_FILE} container-platform-api.jar
COPY application.yml /application.yml
ENTRYPOINT ["java","-jar","-Dspring.config.location=application.yml","-Dspring.profiles.active=prod","/container-platform-api.jar"]
```
- 이미지 생성
  + {K8s_MASTER_NODE_IP} : Cluster에 배포된 Private Image Repository 인 Harbor로 접속하기 위해 외부에서 Cluster에 통신할 수 있는 MasterNode의 IP로 지정한다.
```
$ sudo docker build --tag {K8s_MASTER_NODE_IP}:30002/cp-portal-repository/container-platform-api:latest .
```
- 이미지 생성 확인
```
$ sudo podman images

REPOSITORY                                                            TAG                 IMAGE ID            CREATED             SIZE
xx.xxx.xxx.xx:30002/cp-portal-repository/container-platform-api          latest              45918a869bfd        38 seconds ago      140MB
```

<br>

### 컨테이너 플랫폼 이미지 Private Repository 업로드 방법
> podman를 기준으로 진행한다.

- 배포된 Private Repository인 Harbor에 로그인을 진행한다.
```
$ sudo podman login http://{K8s_MASTER_NODE_IP}:30002 --username admin --password Harbor12345
```

- 로그인한 Private Repository에 컨테이너 플랫폼 이미지를 Push한다.
```
$ sudo docker push {K8s_MASTER_NODE_IP}:30002/cp-portal-repository/cp-portal-api:latest
```