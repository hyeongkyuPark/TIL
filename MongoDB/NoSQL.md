# 📚 NoSQL

## 🔍 NoSQL 이란?
- “Non Relational Operation Database SQL” 의 줄임말로써 “관계형 데이터베이스가 아닌 SQL”
- 일반적인 관계형 데이터베이스는 데이터의 중복을 제거하고 무결성을 보장하기 위해 정규화를 하게 되는데 이러한 정규화가 과도한 JSON으로 인해 성능 저하가 있을 수 있음
- NoSQL은 중첩 데이터 형태를 띔으로써 불필요한 JSON을 최소화

## 📕 NoSQL의 장점
1. 불필요한 Join의 최소화
1. 유연성있는 서버 구조 제공
1. 비정형 데이터 구조로 설계비용 감소
1. 저렴한 비용으로 분산처리 및 병렬처리 가능

## 📕 NoSQL 종류
- KEY-VALUE : Redis, Memcached
- COLUMN : Hbase, Casandra
- DOCUMENT : MongoDB
- GRAPH : GraphDB

## 📕 MongoDB(몽고DB)
- JSON 타입의 Document 방식의 NoSQL
### 특징
- JSON 형식의 데이터구조
- CRUD 위주의 다중 트랜잭션 처리 가능
- Sharding(분산) / Replica(복제) 기능 제공
- Memory Mapping 기술을 기반으로 빅데이터 처리에 성능이 탁월
- 몽고db는 NoSQL이기 때문에 관계형 데이터베이스 테이블 개념이 없음. 대신 여러 데이터가 모인 하나의 단위를 컬렉션이라고 함

### 구성
- 데이터베이스 : 컬렉션의 집합
- 컬렉션 : 여러개의 문서객체를 가짐
- 문서객체 : 속성들의 집합으로 한 사람의 이름과 나이 등을 저장하고 싶을 때 하나의 문서 객체를 만든 후 그 안에 자바스크립트 객체와 같이 속성들을 추가하여 저장할 수 있음