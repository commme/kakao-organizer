# kakao-organizer

카카오톡 "나에게 보내기" CSV/TXT를 Inbox Zero 방식으로 빠르게 분류·처리·아카이빙하는 단일 HTML 도구.

🔗 **라이브 데모**: https://commme.github.io/kakao-organizer/

## 결과물

- **`index.html`** — 단일 HTML 파일 (서버 불필요, GitHub Pages 호스팅)

## 핵심 기능

- **3단계 워크플로우**: 입력 → 검토(Inbox Zero) → 보관함
- **3단 분류기**: 도메인 매핑 → 키워드 → AI(Gemini Flash) + 신뢰도 표시
- **키보드 Inbox Zero**: ← 삭제, → 보관, ↑ 카테고리 변경, ↓ 건너뛰기
- **자동 학습**: 사용자가 카테고리 수정 시 도메인→카테고리 매핑 저장
- **엑셀 내보내기**: 카테고리별 시트 분리 (SheetJS)
- **다크 모드 UI**: 카카오 노란색 → 보라/핑크 그라디언트로 정리감 부여

## 사용법

### 1) 카톡에서 데이터 내보내기

카카오톡 → 나와의 채팅 → 메뉴 → 대화 내보내기 → 텍스트 파일(.txt) 저장

### 2) 도구 실행

```
index.html을 더블클릭 → 텍스트 파일 드래그
```

(또는 https://commme.github.io/kakao-organizer/ 접속)

### 3) 분류 → 검토 → 보관/삭제 → 엑셀 다운로드

- AI 분류는 옵션 (설정에서 Gemini API 키 입력). 키 없어도 도메인 매핑만으로 80% 분류
- 검토 모드는 키보드만으로 처리 가능 (마우스 불필요)

## 사용된 도구

| 영역 | 라이브러리/도구 |
|------|-----------------|
| AI 분류 | Google Gemini 2.5 Flash (사용자 API 키) |
| 엑셀 내보내기 | SheetJS 0.20.3 |
| UI 폰트 | Pretendard |
| 저장 | localStorage (`kk2_` 네임스페이스) |

## 보안

- 모든 데이터는 **브라우저 로컬에서만 저장** — 외부 서버 전송 없음
- API 키도 localStorage에만 저장
- CSP 메타 태그로 외부 스크립트 차단 (cdnjs, generativelanguage.googleapis.com만 허용)
- 모든 사용자 입력은 DOM `textContent`로 처리 (XSS 방지)

## 라이선스

© 2026 COMMME. All rights reserved.
