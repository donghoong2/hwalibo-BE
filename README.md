# 🚽 화리보 (Hwaribo) - 화장실 리뷰 보기

<div align="center">
  <h3>"지하철역 화장실, 가기 전에 미리 확인하세요!"</h3>
  <p>
    수도권 1~8호선 지하철역 화장실의 위치, 청결도, 시설 정보를<br/>
    실사용자 리뷰와 함께 제공하는 웹 서비스입니다.
  </p>
</div>

<div align="center">
  
  <img src="https://img.shields.io/badge/Java-21-007396?style=flat-square&logo=java&logoColor=white"/>
  <img src="https://img.shields.io/badge/Spring%20Boot-3.x-6DB33F?style=flat-square&logo=springboot&logoColor=white"/>
  <img src="https://img.shields.io/badge/MySQL-8.0-4479A1?style=flat-square&logo=mysql&logoColor=white"/>
  <img src="https://img.shields.io/badge/Redis-Cache-DC382D?style=flat-square&logo=redis&logoColor=white"/>
  <img src="https://img.shields.io/badge/AWS-EC2%20%26%20S3-232F3E?style=flat-square&logo=amazon-aws&logoColor=white"/>
  
</div>

<br/>

## 🗂️ 목차
1. [프로젝트 개요](#-프로젝트-개요)
2. [문제 인식 및 해결](#-문제-인식-및-해결)
3. [핵심 기능](#-핵심-기능)
4. [기술 스택](#%EF%B8%8F-기술-스택)
5. [아키텍처](#%EF%B8%8F-아키텍처)
6. [트러블 슈팅 & 기술적 도전](#-트러블-슈팅--기술적-도전)
7. [기대 효과](#-기대-효과)
8. [API 명세](#-api-명세-담당-파트)

---

## 📌 프로젝트 개요
- **개발 기간**: 2025.09.14 ~ 2025.11.28
- **팀 구성**: 백엔드 3명, 프론트엔드 2명, 디자이너 1명
- **내 역할**: **Backend Developer** (이미지 처리, 리뷰 시스템)
- [cite_start]**타겟 사용자**: 수도권 1~8호선 지하철 이용객 중 급하게 화장실을 찾는 사람들 [cite: 43]

<br/>

## 💡 문제 인식 및 해결

### 1. 정보의 부재
> [cite_start]**Problem:** 지하철역마다 화장실이 개찰구 안/밖 어디에 있는지, 몇 번 출구 근처인지 미리 알기 어려움[cite: 23].  
> [cite_start]**Solution:** 각 역사의 화장실 상세 위치 정보(개찰구 유무, 출구 정보)를 직관적으로 제공[cite: 47].

### 2. 상태 정보의 편차 및 불확실성
> [cite_start]**Problem:** 역마다 청결도나 시설(비데, 기저귀 교환대 등) 수준이 천차만별인데 방문 전에는 알 수 없음[cite: 25].  
> [cite_start]**Solution:** 양변기/소변기 수, 장애인 화장실 유무 등 구체적인 시설 정보를 제공하고, **AI 요약**을 통해 전체적인 상태를 한눈에 파악 가능하게 함[cite: 113].

### 3. 신뢰할 수 있는 리뷰의 부재
> [cite_start]**Problem:** 화장실에 대한 구체적이고 믿을 수 있는 평판 정보가 없음[cite: 27].  
> [cite_start]**Solution:** 실사용자 기반 리뷰 시스템을 구축하고, 네이버 소셜 로그인을 통해 투명하게 관리[cite: 49]. [cite_start]**Google Vision API**로 부적절한 이미지를 필터링하여 신뢰도 확보[cite: 75].

<br/>

## 🚀 핵심 기능

### 🏠 홈 & 검색
* [cite_start]**내 주변 화장실**: 위치 기반으로 가장 가까운 지하철역 3곳 자동 추천[cite: 57].
* [cite_start]**통합 검색**: 역 이름으로 검색하여 원하는 역사의 화장실 정보 확인[cite: 107].
* [cite_start]**상세 정보**: 호선, 개찰구 안/밖 여부, 상세 위치, 변기 개수, 평균 평점 제공[cite: 111].

### 📝 리뷰 시스템 (Deep Dive)
* [cite_start]**리뷰 작성**: 별점(1~5점), 키워드 태그(긍정/부정 최대 3개), 텍스트, 사진(최대 2장) 작성[cite: 135, 136, 137].
* **포토 리뷰 정책**:
    * [cite_start]**기본 비공개**: 불쾌감을 줄 수 있어 '보기' 버튼 클릭 시에만 노출[cite: 73].
    * [cite_start]**이성 열람 제한**: 성별에 따라 이성 화장실 사진은 열람 불가[cite: 74].
    * [cite_start]**AI 클린봇**: `Google Cloud Vision API`를 도입하여 유해/부적절 이미지 자동 차단[cite: 75].
    * [cite_start]**AI 요약**: 쌓인 리뷰들을 분석하여 "바닥이 깨끗하고 악취가 없음"과 같이 한 줄 요약 제공[cite: 113].

### 👤 마이페이지
* [cite_start]**활동 관리**: 내가 쓴 리뷰 모아보기, 수정/삭제[cite: 162].
* [cite_start]**활동 뱃지**: '상위 N% 리뷰어' 뱃지 제공으로 활동 동기 부여[cite: 161].

<br/>

## 🛠️ 기술 스택

| Category | Stack |
| --- | --- |
| **Backend** | Java 21, Spring Boot 3.x, Spring Data JPA, QueryDSL |
| **Security** | Spring Security, JWT, OAuth2 (Naver Login) |
| **Database** | MySQL 8.0 (Transaction), Redis (Cache, Refresh Token, Blacklist) |
| **Infra & DevOps** | AWS EC2, S3, GitHub Actions, Docker |
| **External API** | Google Cloud Vision API (이미지 검수) |
| **Tools** | GitHub, Notion, Postman, Swagger |

<br/>

## 🏛️ 아키텍처

<div align="center">
  <img src="./assets/architecture.png" alt="Architecture Diagram" width="80%" />
</div>

<br/>

## 💥 트러블 슈팅 & 기술적 도전

### 1. 비동기 이미지 검수 시스템 구축 (UX 개선)
* **문제**: 이미지 업로드 시 Google Cloud Vision API 동기 호출로 인한 응답 지연 발생.
* **해결**: `@Async`를 적용하여 검수 로직을 비동기로 분리, 사용자 대기 시간 **Zero** 달성.
* **심화**: `TransactionSynchronizationManager`를 활용해 트랜잭션 커밋 후 검수가 실행되도록 하여 데이터 정합성 보장.

### 2. 대용량 데이터 조회 성능 최적화 (No-Offset)
* **문제**: 리뷰 데이터 증가에 따른 OFFSET 페이징 쿼리 속도 저하.
* **해결**: `createdAt`과 `id`를 조합한 **커서 기반(No-Offset) 페이지네이션** 도입으로 조회 성능 **O(1)** 유지.

### 3. N+1 문제 해결 및 쿼리 최적화
* **문제**: 리뷰 목록 조회 시 연관 엔티티(작성자, 사진) 조회로 인한 N+1 문제 발생.
* **해결**: `Fetch Join`과 `DISTINCT`를 적용하여 단일 쿼리로 조회 성능 최적화.

### 4. 데이터 정합성 보장 (보상 트랜잭션)
* **문제**: S3 업로드 성공 후 DB 저장 실패 시 '고아 파일' 발생 문제.
* **해결**: 예외 발생 시 업로드된 S3 파일을 즉시 삭제하는 **보상 트랜잭션 로직** 구현.

<br/>

## 🌟 기대 효과
1.  [cite_start]**이용자 편의 증대**: 화장실 위치와 상태를 미리 파악하여 헤매는 시간과 불편함 감소[cite: 169].
2.  [cite_start]**공공 서비스 개선**: 축적된 리뷰 데이터를 바탕으로 공공기관의 효율적인 시설 개선 유도[cite: 170].
3.  [cite_start]**선진 화장실 문화**: 투명한 정보 공유를 통해 안전하고 청결한 공중화장실 문화 조성에 기여[cite: 171].

<br/>

## 💻 API 명세 (담당 파트)

| Tag | Method | URI | Description |
| :--- | :---: | :--- | :--- |
| **Toilet** | `GET` | `/api/toilets/{toiletId}` | 화장실 상세 정보 조회 |
| **Review** | `GET` | `/api/reviews` | 리뷰 목록 조회 (No-Offset) |
| | `POST` | `/api/reviews` | 리뷰 작성 |
| | `POST` | `/api/reviews/{id}/images` | 리뷰 이미지 삽입 (비동기 검수) |
| | `PUT` | `/api/reviews/{id}/images` | 리뷰 이미지 수정 |
| | `POST` | `/api/reviews/{id}/likes` | 리뷰 좋아요 |
| **Photo** | `GET` | `/api/photo-reviews` | 포토 리뷰 모아보기 |
| | `GET` | `/api/photo-reviews/{id}` | 포토 리뷰 상세보기 |
| **Image** | `GET` | `/api/images/{id}/status` | 이미지 검증 상태 조회 |

<br/>

---
<div align="center">
  Thank you for visiting Hwaribo Project! 🚽
</div>
