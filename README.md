<!-- Language: [한국어](#korean) | [English](#english) -->

<a id="korean"></a>
## 한국어

# PCIP Framework

**AI 코딩 어시스턴트를 위한 Parent-Child Instruction Processing 프레임워크**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-2.1-blue.svg)]()

## 개요

PCIP (Parent-Child Instruction Processing) Framework는 AI 코딩 어시스턴트의 컨텍스트 이해와 코드 품질을 향상시키는 3계층 아키텍처 시스템입니다.

### 핵심 특징

- **3계층 아키텍처**: PM(메타) → Parent(전문가) → Child(실행)
- **동적 전문가 선택**: 요구사항에 따른 실시간 전문가 배정
- **위험도 기반 실행**: 5단계 위험도 평가 시스템
- **외부 지식 통합**: RAG/MCP 등을 통한 최신 정보 활용
- **맥락 기반 처리**: 프로젝트 아키텍처·도메인 맥락 자동 파악

### 3줄 요약

**계층화된 AI**: PM-Parent(전문가)-Child(실행자) 구조. PM이 작업을 판단하고 알맞은 Parent를 배정합니다.

**두뇌가 필요할 때(Explicit Mode)**: 고난도·고위험 작업에는 PM이 Parent를 투입해 견고한 전략을 수립합니다.

**빠르게 끝낼 때(Silent Mode)**: 단순한 작업은 Child가 단독으로 처리합니다. Parent 개입 없이 매우 빠릅니다.

---

## 문제 정의

### 기존 AI 코딩 어시스턴트의 맥락 인식 한계

현재 AI 코딩 어시스턴트들의 주요 문제점:

#### 1) 맥락 무시
- 프로젝트의 전체 아키텍처를 고려하지 않은 코드 생성
- 도메인별 요구사항(보안, 성능, 규정준수 등) 간과
- 기존 코드베이스와의 일관성 부족

#### 2) 불완전한 구현
```
요청: "결제 시스템 구현"
전형적 실패: 다음이 빠진 기본 폼 수준 구현
- 보안 고려(PCI DSS 등)
- 오류 처리 및 롤백
- 이상 거래 탐지/사기 방지
- 감사 로깅
- 환불 처리
```

#### 3) 반복 보정 오버헤드
- 초기 구현 → 문제 발견 → 수정 요청 → 재구현 사이클 반복
- 개발자가 모든 세부사항을 명시적으로 지시해야 하는 부담

---

## 해결 아키텍처

### 구조화된 지도 원칙에서의 영감

PCIP Framework는 구조화된 지도 원칙에서 영감을 얻어 설계되었습니다:

1. **상황 파악**: 요청의 복잡도와 특성 분석
2. **위험 평가**: 작업의 잠재적 리스크 평가  
3. **맥락 고려**: 프로젝트 특성, 기술 스택, 사용자층 고려
4. **가이드 제공**: 적절한 전문가 관점에서 방향 제시
5. **지속 관찰**: 결과물의 품질 기준 검증

---

### 3계층 아키텍처 개요

#### 기존 방식
```
사용자 요청 → AI → 코드 출력
"결제 시스템 구현" → 즉흥 구현 → 잠재적으로 위험한 코드
```

#### PCIP 방식  
```
사용자 요청 → PM(분석) → Parent(가이드) → Child(실행)
"결제 시스템" → 위험도 평가 → 결제+보안 전문가 → 규정 준수·안전한 코드
```

### 계층별 역할

#### 메타 레이어: PM (프로젝트 매니저)
- **역할**: 대화 분석, 전문가 배정
- **책임**:
  - 5단계 위험도 평가
  - 동적 전문가 팀 구성
  - 외부 리소스 연동
  - 프로젝트 컨텍스트 관리

#### Parent 레이어: 도메인 전문가
- **역할**: 특화된 가이드와 품질 기준 제시
- **전문가 유형**:
  - 보안 엔지니어
  - 성능 엔지니어  
  - UX 디자이너
  - 결제 시스템 전문가
  - DevOps 엔지니어
  - 모바일 스페셜리스트

#### Child 레이어: 실행 엔진
- **역할**: 가이드에 따른 정확한 구현
- **역량**:
  - 문법·정합성 검증
  - 모범 사례 적용
  - 기존 코드베이스와의 통합

---

## 설계 철학

### "좋은 부모" 패러다임

PCIP Framework는 "좋은 부모" 개념에서 영감을 받아 설계되었습니다. 좋은 부모는 아이가 무언가를 하고 싶어할 때 단순히 "좋아, 해봐!"라고 말하지 않습니다. 대신 단기적 영향, 잠재적 문제, 장기적 결과를 예측하고, 아이가 감당할 수 있다고 판단되면 안전한 가이드라인을 제공하여 그 경계 내에서 자유롭게 활동할 수 있도록 합니다.

### 좋은 부모 추론 루프

좋은 부모는 "명령"이 아니라 "추론"으로 가이드합니다. PCIP의 Parent는 아래 순환을 따릅니다.

- 관찰: 현재 상태와 코드베이스, 제약, 목표를 관찰
- 가설 수립: 의도와 리스크에 대한 가설을 세움
- 질문/확인: 모호한 부분을 질문하거나 테스트로 확인
- 외부 지식 보강: 최신 문서/표준을 참조해 가설을 보강
- 가드레일 설정: 안전한 경계(불변 조건, 금지사항, 체크리스트) 정의
- 위임: Child가 자율적으로 실행하도록 구체적 경계와 성공 조건을 전달
- 모니터링: 실행 결과와 로그/테스트로 검증
- 조정: 편차가 있으면 경계와 전략을 업데이트

간단 의사코드

```
observe()
hypothesis = formHypothesis(context, risks)
questions = identifyUnknowns(hypothesis)
resolve(questions) using tests/docs/tools
guardrails = defineBoundaries(hypothesis, standards)
delegateToChild(task, guardrails, successCriteria)
result = verify(outputs, tests, logs)
adjust(guardrails, plan) if driftDetected(result)
```

짧은 예시

```
요청: "로그인 로직 최적화"
관찰: 실패율 증가, DB 부하 상승
가설: 레이트리밋·세션회전 누락 + N+1 쿼리
외부지식: OWASP ASVS
가드레일: 
  - 비밀번호 취급 금지, 실패 횟수 임계, 세션 토큰 회전
  - ORM 수준에서 eager loading 적용, 인덱스 검증
위임: Child가 리팩터 + 테스트 추가
모니터링: 에러율/지연/쿼리수 메트릭 확인
조정: 임계값 상향·지연 슬라이딩 윈도우 적용
```

### 사일런트 모드(Silent Mode) vs 익스플리싯 모드(Explicit Mode): 핵심 차이

#### 사일런트 모드: 단순 작업의 최적 속도
단순 작업은 정확성과 속도를 동시에 목표로 합니다. 기본 생성 작업은 기존 SOTA 모델만으로도 충분히 효율적으로 처리됩니다.

#### 익스플리싯 모드: 복잡한 시스템을 위한 종합 분석
Explicit Mode는 고난도·고위험·복잡 업무를 위해 설계되었습니다. 다음 상황에서 진가를 발휘합니다.

- **프로덕션급 코드베이스**의 복잡한 의존성
- **상속·콜백 관계**가 얽힌 구성요소
- **크로스 파일** 임포트/연결성
- **규정 준수 요구**(PCI DSS, HIPAA 등)

이런 경우에는 눈앞의 지시만 처리해서는 안 되고, 상호 연결된 요소들을 함께 고려해야 합니다.

### PM-Parent-Child 협업 프로세스

#### 1) PM 분석
PM은 다음을 분석합니다.
- 요청의 복잡도와 범위
- 기존 코드베이스 아키텍처
- 영향 가능 영역
- 요구 전문 분야

#### 2) Parent 배정 및 전략 수립
Parent가 선정되면 다음을 수행합니다.
- **범위 식별**: 영향 범위 전반을 식별
- **전략 수립**: 전문가 관점에서 접근법 설계
- **지식 보강**: 필요 시 외부 자료(검색, MCP 등) 활용
- **가드레일 정의**: Child 실행을 위한 안정적 경계 제시

#### 3) Child 실행
Child는 가드레일 내에서 실행하며 품질과 안전을 유지한 채 SOTA 역량을 극대화합니다.

### 왜 중요한가

**기존 AI**: "결제 시스템" → 보안 미고려 기본 폼 수준
**PCIP**: "결제 시스템" → 결제+보안 전문가 투입 → PCI 준수·사기 방지·감사 로깅·에러 처리까지 포함한 완결 해법

---

## 위험도 평가 시스템

### 5단계 위험도 분류

| 수준 | 위험도    | 기준                        | 예시                                   | 실행 모드  |
| ---- | --------- | --------------------------- | -------------------------------------- | ---------- |
| 5    | 매우 낮음 | 단일 파일, 영향도 매우 낮음 | CSS 스타일 변경, 콘솔 로그 추가        | 사일런트   |
| 4    | 낮음      | 2–3개 파일, 단일 도메인     | 컴포넌트 수정, 단순 검증               | 사일런트   |
| 3    | 보통      | 다중 파일 또는 교차 도메인  | 신규 기능, API 변경                    | 조건부     |
| 2    | 높음      | 중요 시스템 변경            | 데이터베이스 스키마, 결제 연동         | 익스플리싯 |
| 1    | 치명적    | 시스템 전반 개편            | 아키텍처 마이그레이션, 프레임워크 변경 | 익스플리싯 |

### 실행 모드

#### 사일런트 모드 (레벨 5, 4)
- 사용자 상호작용 최소화, 즉시 실행
- 간단 구현 요약 제공
- 개발 속도 최적화

#### 익스플리싯 모드 (레벨 1, 2, 복잡한 레벨 3)
- 상세 분석과 구현 계획 제시
- 실행 전 사용자 승인 필요
- 변경사항에 대한 포괄적 문서화

## 구성

### 동적 전문가 선택

**대화 키워드 기반 전문가 배정**

| 키워드                            | 배정 전문가                           |
| --------------------------------- | ------------------------------------- |
| "로그인", "보안", "해킹 방지"     | 보안 엔지니어 + 백엔드 아키텍트       |
| "느려", "최적화", "속도"          | 성능 엔지니어 + 도메인 전문가         |
| "사용하기 어려워", "디자인", "UI" | UX 디자이너 + 프론트엔드 스페셜리스트 |
| "결제", "쇼핑", "상거래"          | 결제 시스템 전문가 + 보안 엔지니어    |
| "모바일", "반응형", "앱"          | 모바일 스페셜리스트 + UX 디자이너     |

### 외부 지식 통합

**3단계 신뢰도 시스템**
- **높음**: 내부 지식으로 충분 → 즉시 응답
- **중간**: 외부 자료 교차검증 → 검증된 응답  
- **낮음**: 전문 자료 조회 → 정확한 정보

**지원 외부 소스**
- 기술 문서 및 API 레퍼런스
- 산업 표준 및 컴플라이언스 요구
- 실시간 라이브러리 버전 및 보안 공지
- 프레임워크 베스트 프랙티스

### 품질 보증

**3중 검증 시스템**
1. **Child 레이어**: 문법적 정확성 및 기본 동작 확인
2. **Parent 레이어**: 도메인별 품질 기준 검토
3. **PM 레이어**: 프로젝트 일관성 및 아키텍처 정합성 확인

---

## 성능 비교

### 개발 프로세스

| 단계      | 기존 AI            | PCIP                                     |
| --------- | ------------------ | ---------------------------------------- |
| 초기 요청 | 빠른 구현          | 분석 및 계획                             |
| 결과 품질 | 부분적/불완전      | 완결·맥락 인지                           |
| 반복 수정 | 다수의 재수정 필요 | 최소한의 보정                            |
| 전체 소요 | 1시간 작업 → 1주   | 초반 약간 지연 → 전체적으로 더 빠른 완료 |

### 장점

✅ **설명 부담 감소**: 맥락 인지 처리로 반복 지시 최소화  
✅ **전문가 관점 적용**: 도메인 전문성 자동 반영  
✅ **높은 코드 품질**: 다층 검증으로 견고한 결과  
✅ **사후 문제 감소**: 사전적 엣지케이스 고려  
✅ **프로젝트 일관성**: 아키텍처 정합성 유지  

### 한계

❌ **초기 복잡도**: 단순 작업엔 설정 부담(하지만 Silent Mode로 완화)  
❌ **학습 곡선**: 위험도 시스템 이해 필요  
❌ **AI 한계**: 본질적 한계는 존재  

---

## 변경 로그

- 2.1: `SystemPrompt.md`/`SystemPromptEN.md` 업데이트(지시문 명확화, 용어 통일, 모드 전환 기준 정교화). README 버전 배지 갱신.
- 2.0: 다국어 README 정리, 위험도/모드 표준화, 품질 보증 체계 명시.

## 설치 및 설정

### 사전 준비물
- 시스템 프롬프트를 지원하는 AI 어시스턴트(Claude, ChatGPT 등)
- 개발 환경(Cursor, VS Code 등)

### 빠른 시작

1. **시스템 프롬프트 가져오기**
   ```
   SystemPrompt.md 내용을 복사합니다
   ```

2. **AI 어시스턴트 설정**
   - **Cursor**: User Rules 또는 Project Rules에 추가
   - **ChatGPT**: Custom Instructions에 설정
   - **Claude**: System Prompt로 사용

3. **코딩 시작**
```
User: "인증 시스템 만들어줘"
PCIP: [PM 분석] → [보안 전문가 배정] → [실행]
```

## 사용 예시

### 예시 1: 단순 작업(Silent Mode)
```
User: "버튼 색 빨간색으로 바꿔줘"
PCIP: [즉시 CSS 업데이트]
참고: 저위험 스타일 변경 완료
```

### 예시 2: 복잡 작업(Explicit Mode)  
```
User: "결제 처리 시스템 만들어줘"
PCIP: 
- 위험도: Critical(Level 1)
- 전문가: 결제 + 보안 + 백엔드
- 분석: PCI DSS 준수 필요...
- 진행할까요? Y/n
```

### 예시 3: 다중 전문가 협업
```
User: "모바일 커머스 앱(보안 결제 포함) 만들어줘"
PCIP: 
- PM: 높은 복잡도 감지
- 전문가: 모바일 + UX + 결제 + 보안
- 접근: 토큰화 결제를 갖춘 PWA...
```

### 예시 4: Parent 의견 요청
```
User: "PCIP Parent 의견은?"
PCIP Parent(보안 엔지니어): 
"현재 인증 구현을 기준으로 로그인 시도 레이트리밋, 안전한 세션 토큰 로테이션을 권장합니다..."
```

## 구성 옵션

### 위험도 커스터마이징
프로젝트 성격에 맞춰 시스템 프롬프트의 임계값을 조정하세요.
- 보수적: Explicit Mode 임계값 낮춤
- 공격적: Silent Mode 임계값 높임

### 전문가 선택 오버라이드
선호 전문가를 수동 지정할 수 있습니다.
```
User: "로그인 시스템(UX 중심)"
PCIP: UX 디자이너 + 백엔드 아키텍트 배정
```

---

## Contributing

1. Fork the repository
2. Create a feature branch
3. Submit a pull request with detailed description

## License

MIT License - see [LICENSE](LICENSE) file for details

## Support

- **Issues**: Report bugs and feature requests via GitHub Issues
- **Discussions**: Share experiences and ask questions in GitHub Discussions
- **Documentation**: Check [SystemPrompt.md](SystemPrompt.md) for detailed implementation

---

<a id="english"></a>
## English

### PCIP Framework

**Parent-Child Instruction Processing Framework for AI Coding Assistants**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-2.1-blue.svg)]()

### Overview

PCIP (Parent-Child Instruction Processing) is a three-layer architecture that improves AI coding assistants' context understanding and code quality.

### 3-Line Summary

- **Your AI, Tiered**: PCIP uses a PM → Parent (expert) → Child (worker) structure. The PM sizes up the job, then assigns the right Parent.
- **Need a Brain? (Explicit Mode)**: For gnarly, high-stakes tasks, the PM brings in a Parent to design a solid strategy.
- **Just Get It Done (Silent Mode)**: For basic, straightforward work, the Child handles it solo for maximum speed.

---

### Problem Statement

#### Context Awareness Gaps in Current AI Assistants
- Code generation that ignores overall architecture and domain requirements
- Inconsistent with the existing codebase (security, performance, compliance)
- High iteration overhead due to partial/incomplete implementations

Example (typical pitfalls when asked to “Build payment system”):
- Missing security (PCI DSS), error handling/rollback, fraud prevention, audit logging, refunds

---

### Solution Architecture

#### Traditional vs PCIP
```
Traditional: User → AI → Code → Risky output
PCIP: User → PM (Analysis) → Parent (Guidance) → Child (Execution)
```

#### Layer Specifications
- **Meta Layer: PM**
  - Conversational analysis, risk assessment (5 levels), expert team composition, external resource coordination
- **Parent Layer: Domain Expert**
  - Security, Performance, UX, Payments, DevOps, Mobile, etc.; defines standards and guidance
- **Child Layer: Execution Engine**
  - Implements precisely within guidance; ensures syntactic correctness and integration quality

---

### Design Philosophy

#### The “Good Parent” Paradigm
A good parent anticipates short-term impacts, potential problems, and long-term consequences. If the task is within the child’s capacity, they set safe boundaries so the child can act freely within them. Otherwise, they tighten guardrails, add tools, or expand context.

#### Good Parent Inference Loop
- Observe → Hypothesize → Ask/Validate → Enrich with External Knowledge → Set Guardrails → Delegate → Monitor → Adjust

Pseudocode:
```
observe()
hypothesis = formHypothesis(context, risks)
unknowns = identifyUnknowns(hypothesis)
resolve(unknowns) via tests/docs/tools
guardrails = defineBoundaries(hypothesis, standards)
delegate(task, guardrails, successCriteria)
result = verify(outputs, tests, logs)
adjust(guardrails, plan) if driftDetected(result)
```

Short example (Login optimization):
- Symptoms: Higher failure rate, DB load; Hypothesis: Missing rate-limit/session rotation + N+1 queries
- External: OWASP ASVS; Guardrails: No plaintext passwords, attempt thresholds, token rotation, ORM eager loading
- Delegate: Refactor + tests; Monitor: error/latency/query metrics; Adjust: thresholds + sliding window

#### Silent vs Explicit Mode
- **Silent (Levels 5–4)**: Fast path for simple tasks; minimal interaction; brief summary
- **Explicit (Levels 1–2, complex Level 3)**: Detailed analysis, plan, user approval, comprehensive documentation

---

### Risk Assessment System

| Level | Risk     | Criteria                    | Examples                                  | Mode        |
| ----- | -------- | --------------------------- | ----------------------------------------- | ----------- |
| 5     | Very Low | Single file, minimal impact | CSS styling, console logs                 | Silent      |
| 4     | Low      | 2–3 files, single domain    | Component updates, simple validation      | Silent      |
| 3     | Moderate | Multi-file or cross-domain  | New features, API changes                 | Conditional |
| 2     | High     | Major system changes        | Database schema, payment integration      | Explicit    |
| 1     | Critical | System-wide overhaul        | Architecture migration, framework changes | Explicit    |

---

### Configuration

#### Dynamic Expert Selection (by conversational cues)
- “login”, “security”, “hardening” → Security Engineer + Backend Architect
- “slow”, “optimize”, “latency” → Performance Engineer + Domain Expert
- “design”, “UI/UX”, “usability” → UX Designer + Frontend Specialist
- “payments”, “commerce” → Payment Systems Expert + Security Engineer
- “mobile”, “responsive”, “app” → Mobile Specialist + UX Designer

#### External Knowledge Integration
- Confidence levels: High (direct) / Medium (verify with docs) / Low (consult specialized sources)
- Sources: Technical docs, standards/compliance, real-time library versions, framework best practices

#### Quality Assurance (Triple Verification)
1) Child: Syntactic correctness, baseline behavior  
2) Parent: Domain standards (security, performance, UX)  
3) PM: Architectural consistency and project-wide coherence

---

### Performance Comparison

| Phase            | Traditional AI          | PCIP Framework                            |
| ---------------- | ----------------------- | ----------------------------------------- |
| Initial Request  | Quick implementation    | Analysis & Planning                       |
| Result Quality   | Partial/Incomplete      | Complete & Context-aware                  |
| Iteration Cycles | Multiple fixes required | Minimal revisions needed                  |
| Overall Time     | 1-hour task → 1 week    | Slightly slower start → Faster completion |

Benefits: Reduced explanation overhead, expert perspectives, higher quality, fewer regressions, consistent architecture.  
Limitations: Initial complexity for simple tasks (mitigated by Silent Mode), small learning curve, inherent AI constraints.

---

## Changelog

- 2.1: Updated `SystemPrompt.md`/`SystemPromptEN.md` (clearer instructions, terminology consistency, refined mode switching criteria). Updated README version badge.
- 2.0: Organized bilingual README, standardized risk/mode tables, documented QA workflow.

### Installation & Setup

Prerequisites: AI assistant supporting system prompts (Claude, ChatGPT, etc.), dev environment (Cursor/VS Code).

Quick Start:
1) Copy contents of `SystemPrompt.md`  
2) Configure your AI assistant (Cursor: User/Project Rules; ChatGPT: Custom Instructions; Claude: System Prompt)  
3) Start coding  
```
User: "Build a user authentication system"
PCIP: [PM analyzes] → [Security Parent assigned] → [Child implements]
```

Usage Examples:
- Silent Mode:
```
User: "Change button color to red"
PCIP: Immediate CSS update; Note: low-risk styling change
```
- Explicit Mode:
```
User: "Build payment processing system"
PCIP: Level 1 (Critical); Parents: Payments + Security + Backend; Plan with PCI DSS compliance → Proceed? Y/n
```
- Ask Parent Opinion:
```
User: "What does the PCIP parent say?"
Parent (Security): "Add rate limiting and secure session rotation..."
```

### Configuration Options
- Risk threshold tuning (Conservative vs Aggressive)  
- Expert selection override (e.g., “focus on UX” → UX Designer + Backend Architect)

### Contributing / License / Support
- Contributing: Fork → Feature branch → PR with details  
- License: MIT (see `LICENSE`)  
- Support: Issues / Discussions; docs in `SystemPrompt.md`
