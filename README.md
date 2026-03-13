# ⚖️ K-OpenLaw
### OpenHash + 이종 LLM 기반 사법 자동화 시스템

> **"수년이 걸리는 재판을 1시간 안에. 수천만 원의 소송비용을 10만 원으로."**

🌐 **데모:** [https://openhash.kr/law](https://openhash.kr/law)
&nbsp;&nbsp;&nbsp;&nbsp;🔗 **OpenHash:** [https://github.com/team-jupeter/openhash](https://github.com/team-jupeter/openhash)
&nbsp;&nbsp;&nbsp;&nbsp;🔗 **고팡(Gopang):** [https://github.com/team-jupeter/gopang](https://github.com/team-jupeter/gopang)
&nbsp;&nbsp;&nbsp;&nbsp;📧 **문의:** tensor.city@gmail.com

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](LICENSE)
[![Patent](https://img.shields.io/badge/특허출원-15건-green.svg)](#특허-출원-현황)
[![Status](https://img.shields.io/badge/Status-Prototype_운영중-orange.svg)](https://openhash.kr/law)
[![AI Models](https://img.shields.io/badge/AI-Claude·Gemini·DeepSeek-purple.svg)](#기술-스택)

---

## 목차

1. [개요](#개요)
2. [핵심 문제: 왜 AI 판사가 없는가?](#핵심-문제-왜-ai-판사가-없는가)
3. [K-OpenLaw의 해법](#k-openlaw의-해법)
4. [기존 사법 체계 대비 성능](#기존-사법-체계-대비-성능)
5. [3중 아키텍처](#3중-아키텍처)
6. [실제 적용 사례](#실제-적용-사례)
7. [특허 출원 현황](#특허-출원-현황)
8. [기술가치 평가](#기술가치-평가)
9. [핵심 기술 문서](#핵심-기술-문서)
10. [철학과 비전](#철학과-비전)
11. [오픈소스 철학](#오픈소스-철학)
12. [시작하기](#시작하기)

---

## 개요

K-OpenLaw는 **OpenHash(분산원장 기반 증거 무결성)** + **고팡 PDV(Private Data Vault)** + **이종 LLM 대립 논증** 기술을 결합한 사법 자동화 시스템입니다.

민·형사 소송, 특허 출원, ADR(대안적 분쟁 해결)을 AI가 자동으로 처리하며, 기존 사법 체계의 4가지 근본 문제—**시간, 비용, 공정성, 접근성**—를 동시에 해결합니다.

한국 법조 인력 **44,235명**(변호사 38,950명 · 판사 3,251명 · 검사 2,034명)의 역할을 상당 부분 대신할 수 있습니다.

---

## 핵심 문제: 왜 AI 판사가 없는가?

AI는 이미 어떤 판사보다 정교한 판결문을 작성할 수 있습니다. 그럼에도 AI 판사가 없는 이유는 단 하나입니다.

> **입력 데이터의 신뢰성을 담보할 방안이 없기 때문입니다.**

법정에 제출된 증거나 증언이 거짓이면, 아무리 뛰어난 AI도 오판합니다. K-OpenLaw는 **OpenHash** 기술로 이 문제를 근본적으로 해결합니다.

---

## K-OpenLaw의 해법

```
사건 발생
    │
    ▼
① PDV 자동 기록 (고팡)
   모든 대화·거래·문서를 실시간으로 OpenHash에 저장
    │
    ▼
② 증거 인출 (OpenHash)
   SHA-256 이중 재해싱 + 계층적 분산 저장으로
   위변조 불가능한 증거를 4ms 내에 인출
    │
    ▼
③ 대립 논증 (이종 LLM)
   조력 AI (원고측) ↔ 방해 AI (피고측)
   쟁점별 순차 대립 → 편향·환각 구조적 방지
    │
    ▼
④ 판정 (중재 AI + 인간 승인)
   합의 품질 점수(CQS) 산출 → 최종 결정권은 인간 귀속
```

---

## 기존 사법 체계 대비 성능

> ※ 아래 수치는 개발자 자체 분석 결과이며, **독립적인 제3자 검증을 적극 환영합니다.**

| 비교 항목 | 1심 법원 | 2심 법원 | **K-OpenLaw** |
|---|---|---|---|
| 종합 공정성 점수 | 40점 (D) | 34점 (F) | **90점 이상 (A)** |
| 법리·절차 오류 수 | 11개 | 8개 (누적 19개) | **0개 (구조적 최소화)** |
| 총 재판 기간 (1~3심) | 약 3년 | — | **1시간** |
| 총 비용 (3심 누적) | 수천만~수억 원 | — | **약 10만 원** |
| 증거 검증 방식 | 서류·감정·증인신문 (수개월) | — | **PDV + OpenHash (수초 내)** |
| 처리 속도 비율 | 1 | — | **1/14,400** |
| 비용 비율 | 1 | — | **1/1,000** |

---

## 3중 아키텍처

### 제1층: OpenHash — 데이터 무결성 인프라

```
읍면동 (L1) → 시군구 (L2) → 광역시도 (L3) → 국가 (L4)
```

기존 행정구역 계층을 그대로 활용한 **계층적 샤딩** 구조입니다.

- **위변조 불가:** SHA-256 이중 재해싱 + BLS 서명 검증 → 기록 생성 이후 단 한 글자도 변경 불가
- **실시간 검증:** 평균 **4ms** 이내 무결성 검증 (블록체인 대비 10만 배 빠름)
- **에너지 효율:** 기존 블록체인 대비 **98.5% 절감**
- **다중 서명:** 거래 당사자 쌍방 서명 + 노드 서명 필수 → 공모 위변조 구조적 차단

### 제2층: 고팡(Gopang) — Private Data Vault

고팡의 PDV는 사람·사물·기관이 일상과 업무를 **6하 원칙**에 따라 기록한 LOG 파일입니다. OpenHash 기술로 기록 하나하나의 진실성이 보장됩니다.

> 고팡 사용자 증가 → OpenHash 증거량 비례 증가 → 사법 자동화 시장 자연 창출

### 제3층: 이종 LLM 대립 논증 시스템

| 역할 | 모델 | 기능 |
|---|---|---|
| **조력 AI (LLM-A)** | Claude / Gemini | 사용자(원고, 피해자) 이익 극대화 |
| **방해 AI (LLM-B)** | DeepSeek / GPT | 사회·국가 이익 관점에서 반박 |
| **중재 AI (LLM-C)** | Claude Opus | 쟁점별 순차 합의 도출, CQS 산출 |
| **승인 모듈 (MODULE-D)** | 인간 | 최종 결정권 및 법적 책임 귀속 |

**CQS (합의 품질 종합 점수)** = 양측 수용도(BAS) × 가중치 + 양보 대칭성(CSI) + 쟁점 해소율(IRR)

---

## 실제 적용 사례

### 사례 1. 민사 소송 — 1·2심 기각 사건 분석

- **상황:** 1·2심에서 원고 청구 기각, 현재 3심(대법원) 진행 중
- **K-OpenLaw 역할:** 판결문 분석 → 1·2심 법리·절차 오류 19개 발견 → 3심 승소 가능성 평가 → 상고장·상고이유서 작성 보조
- **결과:** 공정성 점수 1심 40점(D), 2심 34점(F) vs K-OpenLaw **90점 이상(A)**

### 사례 2. 형사 고발 — 증거 위변조 입증

- **상황:** 피고 제출 증거의 사후 위변조 의심
- **K-OpenLaw 역할:** OpenHash 기술로 타임스탬프 불일치 및 해시 불일치 입증, 검사 업무 보조

### 사례 3. 특허 출원·심사 자동화

- **K-OpenLaw 역할:** 특허 명세서·도면 작성, 청구항 구성, 심사관 역할 대행
- 본 레포지토리의 **15건 특허출원서** 전부 K-OpenLaw로 초안 작성

🔗 [실시예 상세 보기](https://openhash.kr/law/#sec-cases)

---

## 특허 출원 현황

| 번호 | 특허 명칭 | 상태 |
|---|---|---|
| 1 | 확률적 계층 분산 기반 데이터 무결성 검증 시스템 | ✅ 출원 완료 |
| 2 | 이종 LLM 기반 대립 논증·판정 자동화 시스템 및 그 운영 방법 | ✅ 출원 완료 |
| 3~15 | OpenHash 네트워크, PDV, ODR, EGCT 관련 특허 | 📋 명세서 공개 (본 레포) |

> 특허 명세서 전문은 [`/ip`](https://github.com/team-jupeter/openhash-website/tree/main/ip) 디렉토리에서 확인하실 수 있습니다.

---

## 기술가치 평가

Claude, Gemini, DeepSeek 복수 AI 모델의 독립 평가 결과입니다.

| 평가 항목 | 결과 |
|---|---|
| **특허 등급** | 신규성·진보성·고유성 **A+** · 혁신성 **S** |
| **특허 등록 가능성** | **95% 이상** |
| **기술 가치 (한국)** | **₩3,200억 원** |
| **유효 시장 (SAM)** | **약 9조 원** |
| **5년차 매출 목표** | **₩9,500억 원** (2031년) |
| **글로벌 시장** | 5,400억~1.1조 원 |

🔗 [평가 보고서 전문 보기](https://openhash.kr/law/#sec-patent-eval)

---

## 핵심 기술 문서

| 문서 | 링크 | 내용 |
|---|---|---|
| OpenLaw 특허출원 명세서 | [openlaw.html](https://openhash.kr/law/openlaw.html) | 시스템 전체 특허 명세 |
| 고팡 Private Data Vault | [pdv.html](https://openhash.kr/law/pdv.html) | PDV 설계 및 운영 원리 |
| 다중 독립 AI LLM | [multi_llm.html](https://openhash.kr/law/multi_llm.html) | 이종 LLM 대립 논증 구조 |
| OpenHash 네트워크 | [openhash_network.html](https://openhash.kr/law/openhash_network.html) | 계층적 샤딩 네트워크 설계 |
| 법치도 평가 방법론 | [methodology.html](https://openhash.kr/law/methodology.html) | CQS 및 공정성 지표 산출 방식 |

---

## 철학과 비전

> **"법치(法治)를 기술적으로 보강한다."**

K-OpenLaw는 판결을 `1+1=2`와 같은 자연과학적 명제로 치환하려 하지 않습니다. 대신 아리스토텔레스의 삼단논법 구조로 각 쟁점과 주장을 **단계적으로 Reducing**하여:

- 분쟁의 원인과 대상을 명확히 드러내고
- 법리 해석의 차이를 투명하게 제시하며
- 누구나 검증 가능한 논리적 경로를 구성합니다

시뮬레이션 결과, K-OpenLaw만으로 해결하기 어려운 사건은 전체의 **약 1%** 수준으로 추정됩니다.

---

## 오픈소스 철학

K-OpenLaw는 **GPL-3.0 라이선스** 하에 다음을 공개합니다:

- 15건의 특허출원 명세서 전문
- 이종 LLM 대립 논증 System Prompt
- OpenHash 네트워크 설정 코드
- 법치도 평가 방법론 및 테스트 케이스

> 전 세계 누구나 성능을 검증하고 개선할 수 있습니다.  
> 법조인 여러분의 비판적 검토와 독립적 검증을 환영합니다.

---

## 시작하기

```bash
git clone https://github.com/team-jupeter/k-openlaw.git
cd k-openlaw
```

데모 및 상세 사용 방법: **[https://openhash.kr/law](https://openhash.kr/law)**

---

## 관련 레포지토리

| 레포 | 내용 |
|---|---|
| [openhash](https://github.com/team-jupeter/openhash) | 데이터 무결성 보장 — 확률적 계층 분산 해시 저장 |
| [gopang](https://github.com/team-jupeter/gopang) | 채팅 앱 기반 국가 인프라 통합 플랫폼 |
| [openhash-website](https://github.com/team-jupeter/openhash-website) | 공식 웹사이트 소스 |

---

© 2026 K-OpenLaw · AI City Inc. · 제주특별자치도  
*본 레포지토리의 특허 명세서 및 기술 문서는 GPL-3.0 라이선스에 따라 공개됩니다.*
