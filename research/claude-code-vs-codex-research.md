# Claude Code vs OpenAI Codex: Research & Information Gathering

**Phase 0 Research Results**
**Date**: 2026-03-25
**Issue**: #68 — Claude Code vs Codex: AI 코딩 에이전트 방법론 비교 블로그 포스트

## 연구 개요

Claude Code와 OpenAI Codex의 AI 코딩 에이전트 방법론 차이를 체계적으로 분석하기 위한 정보 수집 결과입니다.

## Claude Code (Anthropic)

### 핵심 특징

**출시 및 업데이트**
- 2026년 2월 6일 Opus 4.6와 함께 Agent Teams 출시
- 터미널, IDE, 데스크톱 앱, 브라우저에서 사용 가능

**방법론적 접근**
- **"Vibe Coding" 접근법**: 개발자는 더 이상 코더가 아닌 "Outcome Engineer" 역할
- 의도, 사용자 경험, 비즈니스 로직("vibe")을 설명하면 AI가 실행을 담당
- 상호작용적 워크플로우: 추론 과정을 보여주고 결정 시점에서 입력 요청

### 아키텍처

**단일 스레드 마스터 루프**
- 복잡한 멀티 에이전트 시스템 대신 단순하고 통제 가능한 설계
- 체계적인 도구와 계획을 결합한 확장 가능한 자율성

**멀티 에이전트 오케스트레이션**
- Agent Teams: 하나의 리드 에이전트가 전체 작업을 조율
- 각 팀원 에이전트는 독립적인 컨텍스트 윈도우와 Git 워크트리에서 작업
- TeammateTool과 Swarm Mode를 통한 협업

### 개발 도구

**프로젝트 구성**
- **CLAUDE.md**: 프로젝트 루트에 추가하는 마크다운 파일로 코딩 표준, 아키텍처 결정, 선호 라이브러리 설정
- **Skills 시스템**: SKILL.md 파일을 통해 특화된 작업 플레이북 제공

**인터페이스**
- VS Code 확장: 인라인 diff, @-멘션, 계획 검토, 대화 히스토리
- CLI: 터미널에서 직접 파일 편집, 명령 실행, 프로젝트 관리
- Agent SDK: 커스텀 에이전트 구축

## OpenAI Codex

### 핵심 특징

**아키텍처 발전**
- App Server 아키텍처로 모든 클라이언트 표면(CLI, VS Code 확장, 웹 앱) 통합
- 양방향 프로토콜로 코어 로직과 클라이언트 분리

### 실행 모드

**이중 환경 지원**
- **클라우드 샌드박스**: 저장소가 사전 로드된 병렬 백그라운드 작업용
- **로컬 CLI**: 세밀한 승인 제어가 있는 터미널 우선 실행

**보안 및 격리**
- 클라우드의 보안 격리 컨테이너에서 완전히 운영
- 작업 실행 중 인터넷 액세스 비활성화
- GitHub 저장소와 사전 설치된 의존성에만 제한적 접근

### 에이전트 루프 설계

**토큰 효율성**
- Claude Code 대비 2-3배 더 효율적인 토큰 사용
- 컴팩션 기술을 통한 수백만 토큰 처리 (GPT-5.1-Codex-Max)
- 선형 성능을 위한 전략적 프롬프트 캐싱 최적화

**최신 발전사항 (2026)**
- GPT-5.1-Codex-Max: 컴팩션 과정을 통해 다중 컨텍스트 윈도우에서 네이티브 훈련
- 프로젝트 규모의 리팩터링, 심층 디버깅, 멀티 시간 에이전트 루프 지원

### 멀티 에이전트 지원

**macOS 앱**
- 다중 에이전트를 쉽게 관리하고 병렬 작업 실행
- 워크트리 내장 지원으로 충돌 없이 동일 저장소에서 작업
- 각 에이전트는 코드의 격리된 사본에서 작업

## 방법론 차이 비교

### 실행 환경
- **Codex**: OpenAI 관리 클라우드 컨테이너에서 작업 실행
- **Claude Code**: 실제 파일과 환경을 사용하여 터미널에서 직접 실행

### 워크플로우 스타일
- **Codex**: 샌드박스 환경에서 자율적으로 작업하고 검토용 결과 제공
- **Claude Code**: 터미널에서 대화형으로 작업하며 추론 과정 표시

### 토큰 소비 및 효율성
- **Codex**: 동일 작업에 대해 Claude Code보다 2-3배 적은 토큰 사용
- **Claude Code**: 진행 과정을 설명하면서 작업하여 정확도 향상하지만 더 많은 토큰 소모

### 출력 품질 차이
- **Claude Code**: 원본 레이아웃을 더 정밀하게 보존, 포괄적인 문서화 제공
- **Codex**: 시각적으로 다르지만 작동하는 결과 생성, 최소한의 설명

### 설계 철학
- **Claude Code (Opus 4.6)**: 확장된 추론과 컨텍스트 버퍼링 강조 (~100만 토큰 지원)
- **Codex (GPT-5.3)**: 생산적인 코드 완성, 대화형 편집, 터미널 환경에서의 에이전트 실행에 최적화

## 활용 사례 분석

### Claude Code 최적 활용
- 연구 및 검토: 다중 팀원이 문제의 다른 측면을 동시에 조사
- 새로운 모듈이나 기능: 팀원들이 각각 별도 부분 담당
- 경쟁 가설로 디버깅: 팀원들이 다른 이론을 병렬로 테스트
- 크로스 레이어 조정: 프론트엔드, 백엔드, 테스트에 걸친 변경사항

### Codex 최적 활용
- 토큰 효율성이 중요한 대규모 프로젝트
- 자율적 실행이 선호되는 반복적 작업
- 보안이 중요한 격리된 환경에서의 개발
- 빠른 프로토타이핑과 코드 완성

## 결론 및 향후 분석 방향

### 핵심 차이점
1. **환경**: 클라우드(Codex) vs 로컬(Claude Code)
2. **효율성**: 토큰 효율적(Codex) vs 설명적(Claude Code)
3. **철학**: 자율성(Codex) vs 협업(Claude Code)
4. **복잡성**: 통합 시스템(Codex) vs 단순 루프(Claude Code)

### 추가 연구 필요 영역
- 실제 개발 시나리오에서의 성능 벤치마크
- 개발자 경험과 학습 곡선 비교
- 보안 및 데이터 프라이버시 고려사항
- 비용 효율성 분석
- 팀 협업 워크플로우에서의 적용성

---

## 참고 문헌 (Sources)

### Claude Code 관련
- [Claude Code overview - Claude Code Docs](https://code.claude.com/docs/en/overview)
- [Everything-Claude-Code: Optimizing AI Agent Architectures | AIToolly](https://aitoolly.com/ai-news/article/2026-03-24-everything-claude-code-a-comprehensive-agentic-framework-for-optimizing-ai-coding-tools-and-performa)
- [Claude Code Agent Teams: How TeammateTool and Swarm Mode Are Redefining AI Coding — March 2026 Update - Sean Kim — Arts and Tech](https://blog.imseankim.com/claude-code-team-mode-multi-agent-orchestration-march-2026/)
- [Claude Code Is Changing How We Build Software In 2026](https://medium.com/techtrends-digest/claude-code-is-changing-how-we-build-software-in-2026-cba4a800297e)
- [GitHub - anthropics/claude-code](https://github.com/anthropics/claude-code)
- [Orchestrate teams of Claude Code sessions - Claude Code Docs](https://code.claude.com/docs/en/agent-teams)
- [Anthropic: Claude Code Agent Architecture: Single-Threaded Master Loop for Autonomous Coding - ZenML LLMOps Database](https://www.zenml.io/llmops-database/claude-code-agent-architecture-single-threaded-master-loop-for-autonomous-coding)

### OpenAI Codex 관련
- [Codex | AI Coding Partner from OpenAI | OpenAI](https://openai.com/codex/)
- [Introducing Codex | OpenAI](https://openai.com/index/introducing-codex/)
- [OpenAI Publishes Codex App Server Architecture for Unifying AI Agent Surfaces - InfoQ](https://www.infoq.com/news/2026/02/opanai-codex-app-server/)
- [Unrolling the Codex agent loop | OpenAI](https://openai.com/index/unrolling-the-codex-agent-loop/)
- [Introducing the Codex app | OpenAI](https://openai.com/index/introducing-the-codex-app/)
- [Building Production-Ready AI Agents: OpenAI Codex CLI Architecture and Agent Loop Design - ZenML LLMOps Database](https://www.zenml.io/llmops-database/building-production-ready-ai-agents-openai-codex-cli-architecture-and-agent-loop-design)

### 비교 분석
- [Codex vs. Claude Code: AI Coding Assistants Compared | DataCamp](https://www.datacamp.com/blog/codex-vs-claude-code)
- [Codex vs Claude Code: which is the better AI coding agent?](https://www.builder.io/blog/codex-vs-claude-code)
- [Codex vs Claude Code (2026): Benchmarks, Agent Teams & Limits Compared](https://www.morphllm.com/comparisons/codex-vs-claude-code)
- [Claude Code vs. OpenAI Codex | Composio](https://composio.dev/content/claude-code-vs-openai-codex)
- [Claude Code vs Codex (2026): The Most Complete Side-by-Side Comparison](https://emergent.sh/learn/claude-code-vs-codex)