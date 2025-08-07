# PCIP Framework

**Parent-Child Instruction Processing Framework for AI Coding Assistants**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-2.0-blue.svg)]()

## Overview

PCIP (Parent-Child Instruction Processing) Framework는 AI 코딩 어시스턴트의 컨텍스트 이해와 코드 품질을 향상시키는 3계층 아키텍처 시스템입니다.

### Key Features

- **3-Layer Architecture**: PM(Meta) → Expert(Parent) → Child(Execution)
- **Dynamic Expert Selection**: 프로젝트 요구사항에 따른 실시간 전문가 배정
- **Risk-Based Execution**: 5단계 위험도 평가 시스템
- **External Knowledge Integration**: RAG/MCP 도구를 통한 최신 정보 활용
- **Context-Aware Processing**: 프로젝트 아키텍처와 도메인 맥락 자동 파악

---

## Problem Statement

### Context Awareness Issues in Current AI Coding Assistants

현재 AI 코딩 어시스턴트들의 주요 문제점:

#### 1. Context Ignorance
- 프로젝트의 전체 아키텍처를 고려하지 않은 코드 생성
- 도메인별 요구사항(보안, 성능, 규정준수 등) 간과
- 기존 코드베이스와의 일관성 부족

#### 2. Incomplete Implementation
```
User Request: "Build payment system"
Typical AI Response: Basic payment form without:
- Security considerations (PCI DSS compliance)
- Error handling and rollback mechanisms
- Fraud prevention
- Audit logging
- Refund processing
```

#### 3. Iterative Correction Overhead
- 초기 구현 → 문제 발견 → 수정 요청 → 재구현 사이클 반복
- 개발자가 모든 세부사항을 명시적으로 지시해야 하는 부담

---

## Solution Architecture

### Inspiration from Structured Guidance Principles

PCIP Framework는 구조화된 지도 원칙에서 영감을 얻어 설계되었습니다:

1. **상황 파악 (Situation Analysis)**: 요청의 복잡도와 특성 분석
2. **위험 평가 (Risk Assessment)**: 작업의 잠재적 리스크 평가  
3. **맥락 고려 (Context Consideration)**: 프로젝트 특성, 기술 스택, 사용자층 고려
4. **가이드 제공 (Guidance Provision)**: 적절한 전문가 관점에서 방향 제시
5. **지속 관찰 (Continuous Monitoring)**: 결과물의 품질 기준 검증

---

### 3-Layer Architecture Overview

#### Traditional Approach
```
User Request → AI → Code Output
"Build payment system" → Direct implementation → Potentially unsafe code
```

#### PCIP Approach  
```
User Request → PM(Analysis) → Expert(Guidance) → Child(Execution)
"Build payment system" → Risk assessment → Payment + Security experts → Compliant, secure code
```

### Layer Specifications

#### Meta Layer: Project Manager (PM)
- **Role**: Conversational analysis and expert selection
- **Responsibilities**:
  - Risk level assessment (5-level system)
  - Dynamic expert team composition
  - External resource coordination
  - Project context management

#### Parent Layer: Domain Expert
- **Role**: Specialized guidance and quality standards
- **Expert Types**:
  - Security Engineer
  - Performance Engineer  
  - UX Designer
  - Payment Systems Expert
  - DevOps Engineer
  - Mobile Specialist

#### Child Layer: Execution Engine
- **Role**: Precise implementation following expert guidance
- **Capabilities**:
  - Syntactic correctness verification
  - Best practices application
  - Integration with existing codebase

---

## Risk Assessment System

### 5-Level Risk Classification

| Level | Risk     | Criteria                    | Examples                                  | Execution Mode |
| ----- | -------- | --------------------------- | ----------------------------------------- | -------------- |
| 5     | Very Low | Single file, minimal impact | CSS styling, console logs                 | Silent         |
| 4     | Low      | 2-3 files, single domain    | Component updates, simple validation      | Silent         |
| 3     | Moderate | Multi-file or cross-domain  | New features, API changes                 | Conditional    |
| 2     | High     | Major system changes        | Database schema, payment integration      | Explicit       |
| 1     | Critical | System-wide overhaul        | Architecture migration, framework changes | Explicit       |

### Execution Modes

#### Silent Mode (Levels 5, 4)
- Immediate execution with minimal user interaction
- Brief implementation summary provided
- Optimized for development speed

#### Explicit Mode (Levels 1, 2, complex Level 3)  
- Detailed analysis and implementation plan presentation
- User approval required before execution
- Comprehensive documentation of changes

## Configuration

### Dynamic Expert Selection

**Conversational Cue-Based Expert Assignment:**

| Keywords                          | Selected Experts                           |
| --------------------------------- | ------------------------------------------ |
| "로그인", "보안", "해킹 방지"     | Security Engineer + Backend Architect      |
| "느려", "최적화", "속도"          | Performance Engineer + Domain Expert       |
| "사용하기 어려워", "디자인", "UI" | UX Designer + Frontend Specialist          |
| "결제", "쇼핑", "상거래"          | Payment Systems Expert + Security Engineer |
| "모바일", "반응형", "앱"          | Mobile Specialist + UX Designer            |

### External Knowledge Integration

**3-Level Confidence System:**
- **High Confidence**: Internal knowledge sufficient → Direct response
- **Medium Confidence**: Cross-reference external sources → Verified response  
- **Low Confidence**: "Consulting specialized resources" → Accurate information

**Supported External Sources:**
- Technical documentation and API references
- Industry standards and compliance requirements
- Real-time library versions and security advisories
- Framework-specific best practices

### Quality Assurance

**Triple Verification System:**
1. **Child Layer**: Syntactic correctness and basic functionality
2. **Parent Layer**: Domain-specific quality standards
3. **PM Layer**: Overall project consistency and architecture alignment

---

## Performance Comparison

### Development Process

| Phase            | Traditional AI          | PCIP Framework                            |
| ---------------- | ----------------------- | ----------------------------------------- |
| Initial Request  | Quick implementation    | Analysis & Planning                       |
| Result Quality   | Partial/Incomplete      | Complete & Context-aware                  |
| Iteration Cycles | Multiple fixes required | Minimal revisions needed                  |
| Overall Time     | 1-hour task → 1 week    | Slightly slower start → Faster completion |

### Benefits

✅ **Reduced Explanation Overhead**: Context-aware processing eliminates repetitive instructions  
✅ **Expert Perspective**: Domain expertise automatically applied  
✅ **Higher Code Quality**: Multi-layer verification ensures robust output  
✅ **Fewer Post-Implementation Issues**: Proactive consideration of edge cases  
✅ **Project Consistency**: Maintained architectural coherence  

### Limitations

❌ **Initial Complexity**: Longer setup time for simple tasks (mitigated by Silent Mode)  
❌ **Learning Curve**: Requires understanding of risk assessment system  
❌ **AI Constraints**: Still subject to inherent AI limitations  

---

## Installation & Setup

### Prerequisites
- AI coding assistant that supports system prompts (Claude, ChatGPT, etc.)
- Development environment (Cursor, VS Code, etc.)

### Quick Start

1. **Download the System Prompt**
   ```
   Copy the contents of SystemPrompt.md
   ```

2. **Configure Your AI Assistant**
   - **Cursor**: Add to User Rules or Project Rules
   - **ChatGPT**: Set as Custom Instructions
   - **Claude**: Use as System Prompt

3. **Start Coding**
   ```
   User: "Build a user authentication system"
   PCIP: [PM analyzes] → [Security Expert assigned] → [Implementation]
   ```

## Usage Examples

### Example 1: Simple Task (Silent Mode)
```
User: "Change button color to red"
PCIP: [CSS update applied immediately]
Note: Low risk styling change completed
```

### Example 2: Complex Task (Explicit Mode)  
```
User: "Build payment processing system"
PCIP: 
- Risk Level: Critical (Level 1)
- Experts Assigned: Payment Systems + Security + Backend
- Analysis: PCI DSS compliance required...
- Proceed with implementation? Y/n
```

### Example 3: Multi-Expert Coordination
```
User: "Create mobile e-commerce app with secure payments"
PCIP: 
- PM: High complexity detected
- Experts: Mobile Specialist + UX Designer + Payment Expert + Security Engineer
- Approach: Progressive Web App with tokenized payments...
```

## Configuration Options

### Risk Level Customization
Adjust risk thresholds in the system prompt based on your project needs:
- Conservative: Lower thresholds for Explicit Mode
- Aggressive: Higher thresholds for Silent Mode

### Expert Selection Override
Manually specify expert preferences:
```
User: "Build login system (focus on UX)"
PCIP: UX Designer + Backend Architect assigned
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

*Transforming AI coding assistants from simple tools into skilled development team members*
