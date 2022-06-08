## [AKHQ를 이용한 Apache Kafka Monitoring 방법]

<br>

### [Usage & Advantage]

<br>

> #### AKHQ는 인증 및 메시지 조회/검색이 가능하며, Kafka 핵시 서비스와 연동을 지원

- 다양한 기능 제공 : Message 검색, Live Tail, 인증(LDAP 등) 연동
- 운영 기능 제공 : Topic의 Message 전송, Topic 설정 관리, Group 별 권한 관리 가능 (CMAK에서는 Topic에 대한 partition 조절이 가능하지만 AKHQ는 지원 X)
- Kafka 핵심 서비스 연동 : Scheme Registry 연동, Kafka Connect 연동

<br>

### [환경 구성도]

![image](https://user-images.githubusercontent.com/30817824/172547058-105e295d-215f-49b6-9a3b-a9434b1cf6c0.png)

(refer: https://github.com/freepsw/kafka-metrics-monitoring)

<br><br>

----------------------------------------------------

<br><br>

> ## STG.02. Install & Configure

<br>

#### 01. Java 11 설치 (AKHQ는 java 11 부터 설치가 가능함)

```
## 설치 가능한 java version 확인
> yum list java*jdk-devel
Available Packages
java-1.6.0-openjdk-devel.x86_64
java-1.7.0-openjdk-devel.x86_64 
java-1.8.0-openjdk-devel.i686 
java-1.8.0-openjdk-devel.x86_64  
java-11-openjdk-devel.i686  
java-11-openjdk-devel.x86_64
java-latest-openjdk-devel.x86_64 

## jdk 11 설치 
sudo yum install -y java-11-openjdk-devel.x86_64

## 설치된 java version 확인
> java -version
openjdk version "11.0.13" 2021-10-19 LTS
```

<br>

#### 02. AKHQ 설치

```
cd ~
curl -LO https://github.com/tchiotludo/akhq/releases/download/0.19.0/akhq.jar
```


<br>


#### 03. AKHQ 실행
```
## 모니터링 할 broker 접속 정보를 config 파일에 추가
> vi ~/akhq_config_simple.yml

akhq:
  connections:
    local:
      properties:
        bootstrap.servers: "broker-01:9092"


## AKHQ 실행
cd ~
java -Dmicronaut.config.files=akhq_config_simple.yml -jar akhq.jar
```

<br>

#### 04. GCP VPC Network Firewall 설정 (8080 port 허용)

<br>

![image](https://user-images.githubusercontent.com/30817824/172518925-0a960d8a-8a56-4d92-9af6-bf24231fcf53.png)

![image](https://user-images.githubusercontent.com/30817824/172541307-5011100c-2428-4d12-aa07-93d52feeb89d.png)



#### 05. Web Browser에서 접속 확인

```
http://<External IP>:8080
```

![image](https://user-images.githubusercontent.com/30817824/172548191-a4090c34-4888-45ae-8289-4e5a3a8772a0.png)


