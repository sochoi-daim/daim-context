# dev-context-guide

> 개발자가 새 프로젝트를 빠르게 파악하고, 토큰 효율적인 Context Document를 생성하는 Claude Code 플러그인

## 무엇을 하는 플러그인인가요?

새 프로젝트나 낯선 코드베이스를 맡았을 때, 커맨드 하나로 업무 맥락을 정리하고  
이후 Claude와의 대화에서 **매번 설명 없이 바로 작업**에 들어갈 수 있는  
압축된 참고 문서(Context Document)를 생성하고 저장합니다.

## 지원 프로젝트 타입

- **웹**: React, Next.js, Vue
- **유니티**: Unity (URP/HDRP/Built-in), REST API / WebSocket / Photon / Mirror 서버 연동 포함
- **백엔드**: Node.js (Express / NestJS)

## 설치

```bash
npx claude-plugins install @[username]/dev-context-guide
```

설치 후 Claude Code에서 리로드:
```
/reload-plugins
```

## 커맨드

| 커맨드 | 설명 |
|--------|------|
| `/dev-context-guide:context` | 인터뷰 기반으로 맥락 파악 시작 |
| `/dev-context-guide:context web` | 웹 프로젝트 특화 인터뷰 |
| `/dev-context-guide:context unity` | 유니티 프로젝트 특화 인터뷰 |
| `/dev-context-guide:context fast` | 파일만 첨부하면 즉시 문서 생성 (질문 없음) |
| `/dev-context-guide:update` | 기존 문서 업데이트 |
| `/dev-context-guide:save [경로]` | 문서를 파일로 저장 |
| `/dev-context-guide:show` | 현재 문서 출력 |

## 사용 흐름

### 꼼꼼하게 파악하고 싶을 때
```
/dev-context-guide:context
→ 질문-답변 진행
→ Context Document 생성
→ /dev-context-guide:save ./docs/
```

### 빠르게 시작하고 싶을 때
```
/dev-context-guide:context fast
[파일 첨부]
→ 즉시 문서 생성 + [확인 필요] 항목 안내
→ /dev-context-guide:save ./docs/
```

### 다음 작업 시작할 때
```
# 저장된 문서를 붙여넣고 바로 작업 지시
```

## 특징

- **가정 금지 원칙**: 스택을 안다고 임의로 채우지 않음
- **신뢰도 태그**: 확인된 내용 / `[추론됨]` / `[확인 필요]` 구분
- **토큰 최적화**: 구조화된 형식으로 최소 토큰, 최대 맥락 전달
- **React / Vue 분기**: 프레임워크별 템플릿 자동 선택
- **유니티 서버 지원**: REST, WebSocket, Photon/Mirror 구조 포함
