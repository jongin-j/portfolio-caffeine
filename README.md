# portfolio-caffeine(AI 기반 소비 관리 서비스)

> 소비 패턴을 예측하고, 맞춤형 쿠폰과 인사이트를 제공하는 개인 소비 관리 앱
**프로젝트 기간**: 2024.11.17 ~ 2024.12.31 (약 6주)  
**팀 규모**: 5명  
**포지션**: User App 풀스택 개발
---
## 👤 My Role & Contributions
| 영역 | 담당 내용 |
|------|----------|
| **User App 프론트엔드** | React Native(Expo)로 로그인/대시보드/거래내역/쿠폰 전체 화면 구현 |
| **User App 백엔드** | FastAPI로 인증/거래/예산/쿠폰 REST API 설계 및 구현 |
| **OAuth2 소셜 로그인** | Kakao/Google 연동, Authorization Code Flow + JWT 기반 인증 |
| **AI 소비 예측** | XGBoost 예측 결과 API 연동, 예측 카테고리 기반 쿠폰 자동 발급 |
| **LLM 소비 분석** | Gemini API 연동, 프롬프트 설계 및 맞춤형 소비 인사이트 제공 |
| **데이터 전처리** | 2,438만 건 원본 데이터 기간 필터링/카테고리 매핑 로직 설계 기여 |
---
## ⚙️ 핵심 기능
### 1. 소셜 로그인 (Kakao / Google)
- Authorization Code Flow 방식으로 보안 강화
- 백엔드에서 토큰 교환 처리, JWT로 세션 관리
### 2. 대시보드
- 월별 총 지출, 카테고리별 통계 시각화
- 최근 거래 내역 조회
### 3. AI 소비 예측 + 쿠폰 발급
- XGBoost 모델로 다음 달 주요 소비 카테고리 예측
- 예측 결과 기반 맞춤형 쿠폰 자동 발급
### 4. LLM 소비 분석 (잠깐만 AI)
- Gemini API를 활용한 소비 패턴 분석
- 사용자 맞춤형 절약 팁 및 인사이트 제공
### 5. CSV 거래내역 동기화
- 은행별 CSV 파일 업로드 지원
- UTF-8/EUC-KR 인코딩 자동 감지
---

## 🏗️ 아키텍처
[Frontend] [Backend] [Database] [AI/ML] React Native → FastAPI → PostgreSQL ← XGBoost (Expo) ↓ (AWS RDS) Gemini API JWT 인증 REST API


**배포**: AWS ECS + RDS + Docker Compose

---

## 🔧 트러블슈팅

### 1. OAuth2 redirect_uri 불일치 오류
| 항목 | 내용 |
|------|------|
| **증상** | Kakao 로그인 시 redirect_uri 불일치 에러 |
| **원인** | 프론트엔드 요청 URI와 개발자 콘솔 등록 URI 불일치 |
| **해결** | Authorization Code Flow로 전환, 환경변수로 URI 관리 |
| **배운점** | OAuth2 플로우 구조 이해, 보안을 고려한 설계의 중요성 |

### 2. CSV 파일 한글 깨짐
| 항목 | 내용 |
|------|------|
| **증상** | 일부 은행 CSV 파일에서 한글 깨짐 |
| **원인** | 은행별 인코딩 방식 상이 (UTF-8 / EUC-KR) |
| **해결** | 정규식 기반 인코딩 자동 감지 로직 구현 |
| **배운점** | 다양한 입력 데이터를 고려한 방어적 코딩 |

---

## 🛠️ 기술 스택

| 분류 | 기술 |
|------|------|
| Frontend | React Native, Expo |
| Backend | FastAPI, Python |
| Database | PostgreSQL, SQLAlchemy |
| Auth | JWT, OAuth2 (Kakao, Google) |
| AI/ML | XGBoost, Gemini API |
| DevOps | Docker, AWS (ECS, RDS) |

---

## 🚀 실행 방법

```bash
# 로컬 실행 (Docker Compose)
docker-compose up --build
