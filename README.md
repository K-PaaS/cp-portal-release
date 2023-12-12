## Related Repositories

<table>
  <tr>
    <td colspan=2 align=center>플랫폼</td>
    <td colspan=2 align=center><a href="https://github.com/K-PaaS/cp-deployment">컨테이너 플랫폼</a></td>
    <td colspan=2 align=center><a href="https://github.com/K-PaaS/sidecar-deployment">사이드카</a></td>
    <td colspan=2 align=center><a href="https://github.com/K-PaaS/ap-deployment">어플리케이션 플랫폼</a></td>
  </tr>
  <tr>
    <td colspan=2 align=center>포털</td>
    <td colspan=2 align=center><a href="https://github.com/K-PaaS/cp-portal-release">🚩CP 포털</a></td>
    <td colspan=2 align=center>-</td>
    <td colspan=2 align=center><a href="https://github.com/K-PaaS/portal-deployment">AP 포털</a></td>
  </tr>
  <tr align=center>
    <td colspan=2 rowspan=9>Component<br>/ 서비스</td>
    <td colspan=2><a href="https://github.com/K-PaaS/cp-portal-common-api">Common API</a></td>
    <td colspan=2>-</td>
    <td colspan=2><a href="https://github.com/K-PaaS/ap-mongodb-shard-release">MongoDB</a></td>
  </tr>
  <tr align=center>
    <td colspan=2><a href="https://github.com/K-PaaS/cp-metrics-api">Metric API</a></td>
    <td colspan=2>  </td>
    <td colspan=2><a href="https://github.com/K-PaaS/ap-mysql-release">MySQL</a></td>
  </tr>
  <tr align=center>
    <td colspan=2><a href="https://github.com/K-PaaS/cp-portal-api">Portal API</a></td>
    <td colspan=2>  </td>
    <td colspan=2><a href="https://github.com/K-PaaS/ap-pipeline-release">Pipeline</a></td>
  </tr>
  <tr align=center>
    <td colspan=2><a href="https://github.com/K-PaaS/cp-portal-ui">Portal UI</a></td>
    <td colspan=2>  </td>
    <td colspan=2><a href="https://github.com/K-PaaS/ap-rabbitmq-release">RabbintMQ</a></td>
  </tr>
  <tr align=center>
    <td colspan=2><a href="https://github.com/K-PaaS/cp-portal-service-broker">Service Broker</a></td>
    <td colspan=2>  </td>
    <td colspan=2><a href="https://github.com/K-PaaS/ap-on-demand-redis-release">Redis</a></td>
  </tr>
  <tr align=center>
    <td colspan=2><a href="https://github.com/K-PaaS/cp-metrics-api">Terraman API</a></td>
    <td colspan=2>  </td>
    <td colspan=2><a href="https://github.com/K-PaaS/ap-source-control-release">SoureceControl</a></td>
  </tr>
</table>

<i>🚩 You are here.</i>

<br>

## K-PaaS 컨테이너 플랫폼 이미지 빌드
### 소개
컨테이너 플랫폼 프로젝트를 빌드하고 이미지를 생성하여 레파지토리에 이미지를 업로드하는 방법에 대해 기술하였다.
#### 사전 설치
- JDK 설치
- Gradle 설치
- Docker 설치

<br>

### 컨테이너 플랫폼 빌드 방법
컨테이너 플랫폼 프로젝트의 jar 파일 생성을 위해 빌드를 진행한다.
```
$ gradle build
```
<br>

### 컨테이너 플랫폼 이미지 생성 방법
컨테이너 플랫폼 프로젝트 이미지 생성에 필요한 파일을 동일한 디렉토리 내에 위치 시킨다.
+ 컨테이너 플랫폼 포털 소스
  - [container-platform-portal-api](https://github.com/K-PaaS/cp-portal-api)
  - [container-platform-portal-common-api](https://github.com/K-PaaS/cp-portal-common-api)
  - [container-platform-portal-ui](https://github.com/K-PaaS/cp-portal-ui)
  - [container-platform-portal-service-broker](https://github.com/K-PaaS/cp-portal-service-broker)
  - [container-platform-metrics-api](https://github.com/K-PaaS/cp-metrics-api)
  - [container-platform-terraman](https://github.com/K-PaaS/cp-terraman)

<br>

> `cp-portal-api`를 예시로 진행한다.

- 파일 디렉토리 구성
```bash
├── Dockerfile
├── application.yml
└── cp-portal-api.jar
```
- Dockerfile 확인
```bash
$ cat Dockerfile
```
```
FROM openjdk:8-jdk-alpine
ARG JAR_FILE=build/libs/*.jar
RUN addgroup -S 1000 && adduser -S 1000 -G 1000
RUN mkdir -p /home/1000
COPY ${JAR_FILE} /home/1000/container-platform-api.jar
RUN chown -R 1000:1000 /home/1000
ENTRYPOINT ["java","-jar","-Dspring.profiles.active=prod","/home/1000/container-platform-api.jar"]
```
- 이미지 생성<br><br>
  **REPOSITORY URL** : `https://harbor.{HOST_DOMAIN}.nip.io`
  > {HOST_DOMAIN} : 컨테이너 플랫폼 포털 배포 시 [[컨테이너 플랫폼 포털 변수 정의]](https://github.com/K-PaaS/container-platform/blob/master/install-guide/container-platform-portal/cp-portal-deployment-standalone-guide.md#312-컨테이너-플랫폼-포털-변수-정의) 에서 정의한 **HOST_DOMAIN** 값 입력

```bash
$ sudo podman build --tag harbor.{HOST_DOMAIN}.nip.io/cp-portal-repository/container-platform-api:latest .
```
- 이미지 생성 확인
```bash
$ sudo podman images

REPOSITORY                                                                 TAG      IMAGE ID         CREATED             SIZE
harbor.{HOST_DOMAIN}.nip.io/cp-portal-repository/container-platform-api    latest   45918a869bfd     38 seconds ago      140MB
```

<br>

### 컨테이너 플랫폼 이미지 Private Repository 업로드 방법
> podman를 기준으로 진행한다.

- 배포된 Private Repository인 Harbor에 로그인을 진행한다.
```bash
$ sudo podman login harbor.{HOST_DOMAIN}.nip.io --username $REPOSITORY_USERNAME --password $REPOSITORY_PASSWORD
```

- 로그인한 Private Repository에 컨테이너 플랫폼 이미지를 Push한다.
```bash
$ sudo podman push harbor.{HOST_DOMAIN}.nip.io/cp-portal-repository/container-platform-api:latest
```