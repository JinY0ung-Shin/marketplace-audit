# Marketplace Audit

Claude 스타일 marketplace와 plugin을 종합 평가하는 재사용 가능한 스킬입니다. 특히 **Agent·Skill·MCP의 책임 경계와 규칙 소유권**을 근거 중심으로 검토합니다.

## 설치

Claude Code에서 실행합니다. 이 저장소를 marketplace로 추가한 뒤 plugin을 설치합니다.

```text
/plugin marketplace add JinY0ung-Shin/marketplace-audit
/plugin install marketplace-audit@marketplace-audit
```

설치 후 활성화 안내가 나오면 그 안내를 따릅니다. 감사할 저장소를 작업 디렉터리로 열고 다음처럼 실행합니다.

```text
/marketplace-audit:marketplace-audit 이 저장소를 종합 평가해줘. 특히 agent·skill·MCP의 책임 경계와 중복을 집중적으로 봐줘.
```

특정 경로도 지정할 수 있습니다.

```text
/marketplace-audit:marketplace-audit /path/to/target-marketplace를 읽기 전용으로 평가해줘. 점수와 검토 커버리지도 알려줘.
```

### 다른 Agent Skills 지원 도구에서 사용

`plugins/marketplace-audit/skills/marketplace-audit/` 폴더 전체를 대상 도구의 skill 경로에 복사합니다. `SKILL.md`와 `references/`를 함께 유지하세요. 설치 경로·호출 구문·실행 권한은 해당 도구의 문서를 따릅니다. Claude 전용 CLI 검증을 사용할 수 없어도 정적 검토를 진행하며 미검증 범위를 명시합니다.

## 평가 범위

| 영역 | 주요 확인 내용 |
| --- | --- |
| 구조·호환성 | Manifest, 경로, namespace, runtime 지원 |
| 책임 경계·규칙 소유권 | Agent/Skill/MCP의 중복 절차, 상충 기준, 결과 책임 |
| 호출·라우팅 | Description 모호성, 오선택·누락 위험, 중단 조건 |
| 계약·의존성 | 입력·출력·오류, 참조 파일·tool, 외부 의존성 |
| 권한·부작용 | 권한 강제 지점, 읽기·쓰기 계약, 재시도 부작용 |
| 배포·유지보수 | Plugin 결합도, 공통 MCP, 이식성과 변경 범위 |
| 컨텍스트·효율 | 중복 로드·조회, 과도한 위임, 큰 결과 전달 |
| 실행·평가 가능성 | 완료 기준, trace, 대표·경계·실패 시나리오 |

기본 경계는 Agent=목표와 판단, Skill=방법론과 지식, MCP=서비스 계약입니다. 이는 설계 휴리스틱이며 강제 규칙이 아닙니다. MCP의 묶음 조회, LLM을 사용하는 서비스, fork로 실행하는 skill 등을 그 자체만으로 결함으로 판단하지 않습니다.

## 결과 형식

문제별로 **위치 → 근거 → 영향 → 최소 수정안 → 검증 방법**을 제시합니다.

- 확인된 결함, 설계 위험, 개선 제안, 미확인을 구분합니다.
- 검토 범위와 누락 자료를 공개하고 표본 감사로 전체 통과를 선언하지 않습니다.
- 점수는 요청할 때만 제공합니다. 정적 설계 점수와 실행 성능은 구분합니다.
- 읽기 전용 감사가 기본입니다. 수정·설치·서버 실행을 자동으로 승인하지 않습니다.
- 새 행동 평가가 요청되지 않았다면 제공 trace 분석 또는 시나리오 제안까지만 수행합니다.

예시: Agent는 비교군에 10 lot, Skill은 30 lot을 요구한다면 규칙 충돌로 보고합니다. 어느 숫자가 맞는지는 업무 근거 없이 결정하지 않습니다. 반면 MCP가 일관된 snapshot을 위해 API 세 개를 묶어 조회하는 것은 정상 설계일 수 있습니다.

## 파일 구성

| 경로 | 역할 |
| --- | --- |
| `.claude-plugin/marketplace.json` | Marketplace 등록 목록 |
| `plugins/marketplace-audit/.claude-plugin/plugin.json` | Plugin metadata와 버전 |
| `plugins/marketplace-audit/skills/marketplace-audit/SKILL.md` | 감사 절차와 8개 평가 차원 |
| `plugins/marketplace-audit/skills/marketplace-audit/references/boundary-cases.md` | 경계 판정 사례와 오탐 방지 기준 |
| `plugins/marketplace-audit/skills/marketplace-audit/references/evaluation-report.md` | 보고 형식, 점수, 행동 평가 지표 |

별도의 MCP 서버, runtime agent, hook, API key를 요구하지 않습니다. 실제 감사 대상에 접근할 수 있는 환경은 필요합니다.

## 검증과 한계

배포 파일의 JSON, skill frontmatter, 로컬 참조 경로를 검사했습니다. 원본 스킬은 상충 기준과 정상적인 MCP 집계를 포함한 가상 사례로 별도 평가했습니다. Claude Code에서 실제 설치·실행한 결과는 아직 없습니다.

Claude CLI가 있는 환경에서는 저장소 루트에서 다음을 실행할 수 있습니다. Marketplace와 개별 plugin을 각각 검사합니다.

```bash
claude plugin validate .
claude plugin validate ./plugins/marketplace-audit
```

이 검사는 설계 품질이나 실제 라우팅 성공률을 보증하지 않습니다. 지원 항목은 설치된 Claude Code 버전에 따라 달라집니다.

## 업데이트

Plugin을 변경해 배포할 때 `plugins/marketplace-audit/.claude-plugin/plugin.json`의 버전을 올립니다. 사용자는 marketplace 목록을 갱신하고 설치한 plugin의 업데이트를 적용합니다.

## 공식 문서

- [Claude Code marketplace](https://code.claude.com/docs/en/plugin-marketplaces)
- [Claude Code plugins](https://code.claude.com/docs/en/plugins)
- [Claude Code skills](https://code.claude.com/docs/en/skills)
- [Claude Code subagents](https://code.claude.com/docs/en/sub-agents)
- [MCP server concepts](https://modelcontextprotocol.io/docs/learn/server-concepts)

## 제한된 네트워크 환경

`SKILL.md`는 외부 사이트 대신 번들된 [오프라인 reference pack](plugins/marketplace-audit/skills/marketplace-audit/references/offline-reference-index.md)을 참조합니다. 기존 공식 문서 5개의 감사 관련 내용을 영어 요약으로 포함했습니다. 전체 원문 미러는 아니며 기준일은 2026-09-11입니다. 출처 URL은 기록용입니다. 기본 감사 중 외부 문서 접속이나 자동 다운로드를 시도하지 않습니다.

저장소 전체를 서버로 옮긴 뒤 로컬 경로로 등록할 수 있습니다.

```text
/plugin marketplace add /absolute/path/to/marketplace-audit
/plugin install marketplace-audit@marketplace-audit
```

설치한 모델·호스트와 감사 대상 MCP 자체의 네트워크 요구사항은 별개입니다. 로컬 버전의 문서나 schema가 번들 요약과 다르면 로컬 증거를 우선하며, 확인할 수 없는 부분만 미확인으로 보고합니다.
