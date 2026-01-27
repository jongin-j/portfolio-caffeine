# Caffeine — 개인 기여 요약 (Portfolio)

> 소비 패턴을 예측하고, 맞춤형 쿠폰과 인사이트를 제공하는 개인 소비 관리 앱

이 문서는 팀 프로젝트 Caffeine의 개인 기여/구현 요약입니다.

전체 구현/배포/최신 문서는 팀 GitHub에서 확인 가능합니다. /
(팀 레포 링크: https://github.com/HosikYOON/caffeine)

**프로젝트 기간**: 2025.11.17 ~ 2025.12.31 (약 6주)  
**팀 규모**: 5명  
**Role**: Full-stack (User-facing App: Mobile + API)

---

## What I Built (요약)
- **OAuth2 소셜 로그인(Kakao/Google)**: Authorization Code Flow + JWT 세션 구조로 인증 플로우 구현
- **User App(React Native/Expo)**: 로그인/대시보드/거래내역/쿠폰 등 핵심 화면 및 사용자 흐름 구현
- **FastAPI 백엔드**: 인증/거래/예산/쿠폰 REST API 설계 및 구현, 프론트 연동
- **AI 예측 결과 연동**: XGBoost 예측 결과 API 연결, 예측 카테고리 기반 쿠폰 자동 발급 플로우 구성
- **CSV 거래내역 업로드**: 업로드 + 인코딩(UTF-8/EUC-KR) 자동 감지로 은행별 파일 호환성 확보
- **데이터 전처리**: 2,438만 건 원본 데이터 기간 필터링/카테고리 매핑 로직 설계
- **LLM 인사이트(Gemini)**: 프롬프트 설계 및 맞춤형 소비 인사이트 제공(기능 PoC)

---

## My Role & Contributions
| 영역 | 담당 내용 |
|------|----------|
| **Mobile(User App) 프론트엔드** | React Native(Expo)로 로그인/대시보드/거래내역/쿠폰 등 핵심 화면 구현 |
| **백엔드(API)** | FastAPI로 인증/거래/예산/쿠폰 REST API 설계 및 구현 |
| **OAuth2 소셜 로그인** | Kakao/Google 연동, Authorization Code Flow + JWT 기반 인증 |
| **AI 소비 예측 연동** | XGBoost 예측 결과 API 연동, 예측 카테고리 기반 쿠폰 자동 발급 |
| **LLM 소비 분석** | Gemini API 연동, 프롬프트 설계 및 맞춤형 인사이트 제공(PoC) |
| **데이터 전처리** | 2,438만 건 원본 데이터 기간 필터링/카테고리 매핑 로직 설계 |

---

## 핵심 기능
### 1) 소셜 로그인 (Kakao / Google)
- Authorization Code Flow 기반 인증(보안/구조 명확화)
- 백엔드에서 토큰 교환 처리, JWT로 세션 관리

### 2) 대시보드
- 월별 총 지출 / 카테고리별 통계 시각화
- 최근 거래 내역 조회

### 3) AI 소비 예측 + 쿠폰 발급
- XGBoost 모델로 다음 달 주요 소비 카테고리 예측
- 예측 결과 기반 맞춤형 쿠폰 자동 발급

### 4) LLM 소비 분석 (잠깐만 AI)
- Gemini API를 활용한 소비 패턴 분석(PoC)
- 사용자 맞춤형 절약 팁 및 인사이트 제공

### 5) CSV 거래내역 동기화
- 은행별 CSV 파일 업로드 지원
- UTF-8/EUC-KR 인코딩 자동 감지로 한글 깨짐 방지

---

## 아키텍처
<img width="3840" height="2160" alt="architecture" src="https://github.com/user-attachments/assets/5a808003-264b-4206-b65d-d551538fda8b" />


### 데이터 흐름
`User App` → `FastAPI` → `PostgreSQL` → `XGBoost / Gemini API`

**배포**: AWS ECS + RDS (+ Docker Compose로 로컬 실행)

---

## 트러블슈팅
### 1) OAuth2 redirect_uri 불일치 오류
| 항목 | 내용 |
|------|------|
| **증상** | Kakao 로그인 시 redirect_uri 불일치 에러 |
| **원인** | 프론트엔드 요청 URI와 개발자 콘솔 등록 URI 불일치 |
| **해결** | Authorization Code Flow로 전환, 환경변수로 redirect URI 관리 |
| **결과** | 로컬/배포 환경에서 로그인 플로우 정상 동작 |
| **배운점** | OAuth2 플로우 구조 이해, 보안을 고려한 설계의 중요성 |

### 2) CSV 파일 한글 깨짐
| 항목 | 내용 |
|------|------|
| **증상** | 일부 은행 CSV 파일에서 한글 깨짐 |
| **원인** | 은행별 인코딩 방식 상이 (UTF-8 / EUC-KR) |
| **해결** | 인코딩 자동 감지 로직 구현(UTF-8/EUC-KR 대응) |
| **결과** | 은행별 CSV 업로드 시 한글 깨짐 문제 재현 케이스 해결 |
| **배운점** | 다양한 입력 데이터를 고려한 방어적 코딩 |

---

## 기술 스택
| 분류 | 기술 |
|------|------|
| Frontend | React Native, Expo |
| Backend | FastAPI, Python |
| Database | PostgreSQL, SQLAlchemy |
| Auth | JWT, OAuth2 (Kakao, Google) |
| AI/ML | XGBoost, Gemini API |
| DevOps | Docker, AWS (ECS, RDS) |

---

※ 본 저장소는 포트폴리오 요약용 README 입니다.
