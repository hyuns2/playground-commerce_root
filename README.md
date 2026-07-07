# 🛒 playground-commerce

> **커머스 도메인을 경험해보기 위해 진행한 개인 프로젝트
문제의 대안과 트레이드오프를 고민하고, 측정치로 판단하는 것에 집중한 흔적들**
> 

`DDD / 헥사고날` · `동시성 제어` · `SAGA / 보상 트랜잭션` · `결제 멱등성` · `부하 테스트`


## 🎯 이 프로젝트가 던지는 질문

1. [한정된 재고에 몇 천개의 동시 요청이 몰리면, 재고의 oversell을 어떻게 방지할건가](https://hyuns2.notion.site/oversell-3902ac90a22f80cbbd50ffaa6bce6312)
2. [완전한 정합성을 갖춘 보상 트랜잭션, 어디까지 고려해야 하는가](https://hyuns2.notion.site/3902ac90a22f8015b9aedf76bd209e92)
3. [요청이 2번 들어가서 발생하는 중복 요청 vs 진짜 한번 더 수행해야 하는 중복 요청](https://hyuns2.notion.site/2-vs-3902ac90a22f8024a0c3d5055ca2f8a7)
4. [튜닝 0부터 시작하여 AWS 프리티어 크레딧 한계까지, 로드 테스트와 성능 개선 반복하기](https://drive.google.com/file/d/1HDzVALc-Rc5ahZUDjqgKkEVDbcw0QGmL/view?usp=sharing)

> 많은 기능을 만드는 대신, 위 질문들을 깊게 생각해보는 시간이었습니다.
> 기능은 “주문/결제”, “전체/부분 취소”에 필요한 최소한으로 구현했습니다.


## 🛠️ 기술 스택

| 분류 | 사용 |
| --- | --- |
| Language / Framework | Java 17, Spring Boot 3, JUnit 5 |
| Persistence | MySQL 9, Spring Data JPA |
| Messaging | Kafka 4 (비동기 이벤트) |
| Cache | Redis 7 (Lua Script) |
| Infra | Docker Compose, Github Actions, AWS EC2 |
| Load test | K6 |
| Monitoring Agents | Node Exporter, CAdvisor, Micrometer
| Monitoring | Prometheus, Grafana |


## 🗂️ 프로젝트 구조

```
playground-commerce_root/    # 현재 위치
├─ gateway/                    # https://github.com/hyuns2/playground-commerce_gateway.git
├─ catalog-service/            # https://github.com/hyuns2/playground-commerce_catalog-service.git
├─ inventory-service/          # https://github.com/hyuns2/playground-commerce_inventory-service.git
├─ order-service/              # https://github.com/hyuns2/playground-commerce_order-service.git      
├─ payment-service/            # https://github.com/hyuns2/playground-commerce_payment-service.git
├─ docker-compose.yml
├─ .env
└─ .dockerignore
```


## 📊 DB 다이어그램
<img width="1465" height="1039" alt="image" src="https://github.com/user-attachments/assets/5d6fddb4-a747-4c0d-b607-2561f1f37f6d" />


## 🏗️ 시스템 아키텍처
<img width="1645" height="549" alt="image" src="https://github.com/user-attachments/assets/7e9049a0-fd36-4d5c-bdf5-2c14ec583dae" />
⬇️
<img width="1645" height="781" alt="image" src="https://github.com/user-attachments/assets/4641ee0a-9907-46c4-8014-1aceb509a1b6" />


## 🚀 실행 방법
```
>> ▶️ 실행
1. 인프라 (MySQL, Kafka, Redis) 구축 & 환경변수 설정
2. docker build -t <서비스 이미지명> <Dockerfile 경로>
	- Dockerfile에 .jar의 정확한 경로 필요
	- CI/CD 환경변수 설정했다면, 생략 가능
		-> Docker Hub에서 자동 Pulling
3. docker network create playground-network
4. docker-compose up -d

>> ⏹️ 종료
docker-compose down
```
