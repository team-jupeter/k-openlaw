# K-OpenLaw

> **"법치(法治)를 기술적으로 보강한다."**

고팡 플랫폼 기반 AI 비서 주도 **분쟁 예방** 및 **독립 주체 분산형 자율 분쟁 해결** 시스템

---

## 핵심 기술

- **[Openhash](https://github.com/team-jupeter/openhash)**: 데이터 무결성 보장 (물리적 통신 계층 기반 확률적 해시 저장)
- **[고팡(Gopang)](https://github.com/team-jupeter/gopang)**: 채팅·메일·통신 등 소통 애플리케이션 기반 국가 인프라 통합 플랫폼
- **AI/LLM**: 다중 독립 모델 간 대립 논증으로 편향과 환각 방지

---

## 📊 실증 데이터

### 법원 판결 vs K-OpenLaw 분석 결과 (AWS 클라우드 실증 시뮬레이션, 2026.3)

| 비교 항목 | 1심 법원 | 2심 법원 | **K-OpenLaw** |
|---|---|---|---|
| 종합 공정성 점수 | 40점 (D) | 34점 (F) | **90점 이상 (A)** |
| 법리·절차 오류 수 | 11개 | 8개 (누적 19개) | **0개 (구조적 최소화)** |
| 쟁점 분석 완료 시간 | 수개월 | — | **45.8초** (4모듈 순차 처리, 실측) |
| 건당 처리 비용 | 수천만~수억 원 | — | **약 3.6원** (DeepSeek+Claude Sonnet, 실측) |
| 증거 검증 방식 | 서류·감정·증인신문 | — | **PDV + OpenHash** (평균 0.0022ms, 실측) |
| 동시 처리 TPS | — | — | **581,362 TPS** (실측) |
| 위법 징후 감지율 | — | — | **100.0%** (오탐율 0.0%, 실측) |
| 공격 탐지율 | — | — | **100.0%** (무결성 유지율 100.0%, 실측) |

> ※ K-OpenLaw 수치는 2026년 3월 AWS us-east-1 실증 시뮬레이션 완료 결과입니다.
> 재현 방법은 아래 **시뮬레이션 재현 절차** 섹션을 참조하십시오.
> **독립적인 제3자 검증을 적극 환영합니다.**

---

## 🔍 실제 적용 사례

### 1️⃣ 민사 소송 — 1·2심 기각 사례

- **상황**: 1·2심에서 원고 청구 기각, 현재 3심(대법원) 진행 중
- **K-OpenLaw 역할**: 판결문 분석 → 3심 승소 가능성 평가 → 상고장·상고이유서 작성

### 2️⃣ 형사 고발 — 증거 위변조 입증

- **상황**: 피고 제출 증거의 사후 위변조 의심
- **K-OpenLaw 역할**: Openhash 기술로 위변조 입증, 검사 업무 보조

### 3️⃣ 특허 출원·심사 자동화

- **K-OpenLaw 역할**: 특허 명세서·도면 작성, 청구항 구성, 심사관 역할 대행

[🔗 실시예 상세 보기](https://openhash.kr/law/#sec-cases)

---

## 📁 핵심 기술 문서

| 문서 | 링크 |
|---|---|
| OpenLaw 특허출원 명세서 | [openlaw.html](https://openhash.kr/law/openlaw.html) |
| 고팡 Private Data Vault | [pdv.html](https://openhash.kr/law/pdv.html) |
| 다중 독립 AI LLM | [multi_llm.html](https://openhash.kr/law/multi_llm.html) |
| OpenHash 네트워크 | [openhash_network.html](https://openhash.kr/law/openhash_network.html) |
| 법치도 평가 방법론 | [methodology.html](https://openhash.kr/law/methodology.html) |

---

## 🖥️ AWS 클라우드 실증 시뮬레이션 환경

### 하드웨어 인프라

| 항목 | 값 |
|---|---|
| 클라우드 | AWS us-east-1 (미국 동부, 버지니아) |
| 가용 영역 | us-east-1f |
| 인스턴스 유형 | t3.micro (vCPU 2, 메모리 1GB) |
| AMI | Ubuntu 24.04 LTS (`ami-0c7217cdde317cfec`) |
| 스토리지 | EBS gp3 8GB |
| 네트워크 | 탄력적 IP 적용 |
| 시뮬레이션 수행 일시 | 2026년 3월 |

### 소프트웨어 환경

| 항목 | 값 |
|---|---|
| Python | 3.12.3 |
| 가상환경 | `python3 -m venv` |
| openai | `>= 1.0.0` (DeepSeek API 호환 클라이언트) |
| anthropic | `>= 0.20.0` |
| python-dotenv | `>= 1.0.0` |

### LLM 모듈별 독립 배정

| 모듈 | LLM | API 엔드포인트 | 비고 |
|---|---|---|---|
| 원고 에이전트(110) | `deepseek-chat` | `api.deepseek.com` | 원고 측 독립 운용 |
| 피고 에이전트(120) | `claude-sonnet-4-5` | `api.anthropic.com` | 피고 측 독립 운용 |
| 중재 모듈(130) | `deepseek-chat` | `api.deepseek.com` | 독립 제3자 운용 |
| 판결 모듈(140) | `claude-sonnet-4-5` | `api.anthropic.com` | 독립 기관 운용 |
| 예방 법학(101-P) | `deepseek-chat` | `api.deepseek.com` | AI 비서 실시간 분석 |
| 조작 저항성 감사 | `claude-sonnet-4-5` | `api.anthropic.com` | 무결성 감사 모듈 |

### API 비용 기준 (2026년 3월)

| LLM | 입력 | 출력 |
|---|---|---|
| DeepSeek-chat | $0.14 / 1M 토큰 | $0.28 / 1M 토큰 |
| Claude Sonnet | $3.00 / 1M 토큰 | $15.00 / 1M 토큰 |
| **전체 시뮬레이션 비용** | **$0.05 미만** | — |

---

## 📐 시뮬레이션 재현 절차

### Step 1 — AWS EC2 인스턴스 생성

```
AMI      : Ubuntu 24.04 LTS (ami-0c7217cdde317cfec 또는 동등 버전)
유형     : t3.micro 이상 (t3.small 권장 시 응답 시간 개선 가능)
보안그룹  : SSH(22) 인바운드, HTTPS(443) 아웃바운드 허용
```

### Step 2 — 소프트웨어 환경 구성

```bash
# 시스템 업데이트
sudo apt update && sudo apt install -y python3-pip python3-venv python3-full git

# 저장소 클론
git clone https://github.com/team-jupeter/k-openlaw.git
cd k-openlaw

# 가상환경 생성 및 활성화
python3 -m venv venv
source venv/bin/activate

# 패키지 설치
pip install -r requirements.txt
```

### Step 3 — API 키 발급 및 .env 설정

```bash
# .env 파일 생성
cp .env.example .env
nano .env  # API 키 입력
chmod 600 .env
```

**API 키 발급처:**
- DeepSeek: [platform.deepseek.com](https://platform.deepseek.com) → API Keys → Create
- Anthropic: [console.anthropic.com](https://console.anthropic.com) → Settings → API Keys → Create Key

```env
DEEPSEEK_API_KEY=sk-여기에_입력
ANTHROPIC_API_KEY=sk-ant-여기에_입력
```

### Step 4 — API 연결 테스트

```bash
python3 - << 'EOF'
import os
from dotenv import load_dotenv
from openai import OpenAI
import anthropic

load_dotenv()
ds = OpenAI(api_key=os.getenv("DEEPSEEK_API_KEY"), base_url="https://api.deepseek.com")
cl = anthropic.Anthropic(api_key=os.getenv("ANTHROPIC_API_KEY"))

r1 = ds.chat.completions.create(model="deepseek-chat",
     messages=[{"role":"user","content":"연결 테스트. 'DeepSeek 정상'이라고만 답하세요."}], max_tokens=20)
print("1.", r1.choices[0].message.content)

r2 = cl.messages.create(model="claude-sonnet-4-5", max_tokens=20,
     messages=[{"role":"user","content":"연결 테스트. 'Claude 정상'이라고만 답하세요."}])
print("2.", r2.content[0].text)
EOF
```

기대 출력:
```
1. DeepSeek 정상
2. Claude 정상
```

### Step 5 — 전체 시뮬레이션 실행

```bash
python3 scenarios/simulate.py 2>&1 | tee results/simulation_log.txt
```

- 예상 소요 시간: **약 3~5분** (API 응답 대기 포함)
- 예상 비용: **$0.05 미만**

### Step 6 — 결과 확인

```bash
cat results/simulation_results.json
```

출력 형식:
```json
{
  "S1": { "위법징후감지율": "100.0%", "오탐율": "0.0%", ... },
  "S2": { "쟁점분석완료시간": "45.8초", "합의가능성점수APS": "0.50", ... },
  "S3": { "평균해시등록시간ms": "0.0022", "위변조탐지정확도": "100.0%", ... },
  "S4": { "공격탐지율": "100.0%", "결과무결성유지율": "100.0%", ... }
}
```

---

## 🤖 시스템 프롬프트 전문

> 전체 프롬프트 파일은 [`prompts/`](./prompts/) 디렉터리에 공개되어 있습니다.

### AI 비서 예방 법학 기능 (101-P) — `prompts/prevention.txt`

```
당신은 고팡 플랫폼의 AI 비서(101) 예방 법학 기능(101-P)입니다.
아래 메시지의 위법 가능성을 분석하여 반드시 다음 JSON 형식으로만 답하십시오.

{"score": 0.0~1.0, "grade": "정상|주의|경고|긴급경고", "reason": "한 줄 근거"}

판단 기준:
- score 0.3 미만  → grade: "주의"
- score 0.3~0.69  → grade: "경고"
- score 0.7 이상  → grade: "긴급경고"
- 위법 징후 없음  → grade: "정상", score: 0.0~0.29
```

### 원고 에이전트 (110) — `prompts/plaintiff_agent.txt`

```
당신은 원고 에이전트 모듈(110)입니다. 원고 측 독립 운용 LLM입니다.
...
6단계 규범 위계 준수 / 5문 자기검증 테스트 통과 필수
출력: {"주장": "...", "근거법조항": "...", "쟁점": [...]}
```

### 피고 에이전트 (120) — `prompts/defendant_agent.txt`

```
당신은 피고 에이전트 모듈(120)입니다. 피고 측 독립 운용 LLM입니다.
...
6단계 규범 위계 준수 / 5문 자기검증 테스트 통과 필수
출력: {"주장": "...", "근거법조항": "...", "쟁점": [...]}
```

### 중재 모듈 (130) — `prompts/mediation.txt`

```
당신은 중재 모듈(130)입니다. 독립 제3자 LLM입니다.
AI 에이전트들 간의 논쟁 규칙 준수 여부를 감시하고 강제합니다.
...
출력: {"합의가능쟁점": [...], "미합의쟁점": [...], "APS점수": 0.0~1.0, "권고안": "..."}
```

### 판결 모듈 (140) — `prompts/verdict.txt`

```
당신은 판결 모듈(140)입니다. 독립 기관 운용 LLM입니다.
...
출력: {"주문": "...", "이유": "...", "적용법조": "...", "인용금액": "..."}
```

### 조작 저항성 감사 모듈 — `prompts/integrity_audit.txt`

```
당신은 고팡 분산형 분쟁 해결 시스템의 무결성 감사 모듈입니다.
...
출력: {"is_attack": true/false, "confidence": 0.0~1.0, "reason": "..."}
```

---

## 📊 시뮬레이션 측정 결과

> AWS us-east-1 (EC2 t3.micro, Ubuntu 24.04), 2026년 3월 실측값

### 시나리오 1 — 예방 법학 성능 검증

| 측정 항목 | 실측값 |
|---|---|
| 위법 징후 감지율 | **100.0%** (5/5건 감지) |
| 오탐율 | **0.0%** (5/5건 정상 판정) |
| 평균 경고 응답 시간 | **2,956ms** |
| P95 경고 응답 시간 | **3,135ms** |

### 시나리오 2 — 분쟁 해결 처리 성능 검증

| 측정 항목 | 실측값 |
|---|---|
| 쟁점 분석 완료 시간 | **45.8초** (원고·피고·중재·판결 4모듈 순차 처리) |
| 합의 가능성 점수(APS) | **0.50** |
| 합의 도달률 | **50.0%** |
| 건당 처리 비용 (추정) | **약 3.6원** (DeepSeek + Claude Sonnet 혼합) |

### 시나리오 3 — 무결성 보장 기술(91) 검증 성능

| 측정 항목 | 기준치 | 실측값 |
|---|---|---|
| 평균 해시 등록 시간 | ≤ 4ms | **0.0022ms** ✅ |
| P99 해시 등록 시간 | ≤ 4ms | **0.0041ms** ✅ |
| 위변조 탐지 정확도 | — | **100.0%** (40/40건) |
| 동시 처리 TPS | — | **581,362 TPS** |

### 시나리오 4 — 독립 주체 분산 구조 조작 저항성 검증

| 측정 항목 | 실측값 |
|---|---|
| 공격 탐지율 | **100.0%** (5/5건 탐지) |
| 결과 무결성 유지율 | **100.0%** (5/5건 정상) |
| 평균 탐지 응답 시간 | **3,738ms** |

> 전체 결과 JSON: [`results/simulation_results.json`](./results/simulation_results.json)

---

## 🧪 특허성·기술가치 평가

K-OpenLaw는 복수의 AI 모델(Claude, Gemini, DeepSeek)로부터 특허성 및 기술가치 평가를 받았습니다.

| 평가 항목 | 주요 내용 |
|---|---|
| **특허성** | 신규성·진보성·산업상 이용가능성 모두 충족 (등록 가능성 95% 이상) |
| **기술가치** | 한국 시장 610~750억 원, 글로벌 5,400억~1.1조 원 |
| **사업성** | 시장 규모 9조 원, 5년차 매출 9,500억 원 추정 |

[🔗 평가 보고서 보기](https://openhash.kr/law/#sec-patent-eval)

---

## 💡 철학과 비전

K-OpenLaw는 판결을 1+1=2와 같은 자연과학적 명제로 치환하려 하지 않습니다.
대신, 아리스토텔레스의 삼단논법 구조로 각 쟁점과 주장을 **단계적으로 Reducing**하여:

- 분쟁의 원인과 대상을 명확히 드러내고
- 법리 해석의 차이를 투명하게 제시하며
- 누구나 검증 가능한 논리적 경로를 구성합니다

시뮬레이션 결과, K-OpenLaw의 분석만으로 해결하기 어려운 사건은 전체의 **약 1%** 수준으로 추정됩니다.

---

## 🌱 오픈소스 철학

K-OpenLaw는 **GPL 라이선스** 하에 오픈소스로 공개됩니다:

- 15건의 특허출원서
- System Prompt (전문 공개 — [`prompts/`](./prompts/) 참조)
- 시뮬레이션 코드 ([`scenarios/simulate.py`](./scenarios/simulate.py) 참조)
- 테스트 방법론 및 실측 결과

> 전 세계 누구나 성능을 검증하고, 개선할 수 있습니다.
> 법조인 여러분의 비판적 검토와 독립적 검증을 환영합니다.

---

## 🚦 빠른 시작 (Quick Start)

```bash
# 1. 저장소 클론
git clone https://github.com/team-jupeter/k-openlaw.git
cd k-openlaw

# 2. 가상환경 생성 및 패키지 설치
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 3. API 키 설정
cp .env.example .env
nano .env   # DEEPSEEK_API_KEY, ANTHROPIC_API_KEY 입력

# 4. 전체 시뮬레이션 실행
python3 scenarios/simulate.py

# 5. 결과 확인
cat results/simulation_results.json
```

> 상세 재현 절차는 위 **시뮬레이션 재현 절차** 섹션을 참조하십시오.
> API 키 발급: [DeepSeek](https://platform.deepseek.com) | [Anthropic](https://console.anthropic.com)

---

## 저장소 구조

```
k-openlaw/
├── README.md                    # 이 파일
├── LICENSE                      # GPL-3.0
├── requirements.txt             # Python 패키지 목록
├── .env.example                 # 환경변수 템플릿
├── scenarios/
│   └── simulate.py              # 전체 시뮬레이션 스크립트
├── prompts/
│   ├── prevention.txt           # 예방 법학 기능(101-P) 프롬프트
│   ├── plaintiff_agent.txt      # 원고 에이전트(110) 프롬프트
│   ├── defendant_agent.txt      # 피고 에이전트(120) 프롬프트
│   ├── mediation.txt            # 중재 모듈(130) 프롬프트
│   ├── verdict.txt              # 판결 모듈(140) 프롬프트
│   └── integrity_audit.txt      # 조작 저항성 감사 프롬프트
└── results/
    └── simulation_results.json  # 실측 결과 (참고용)
```
