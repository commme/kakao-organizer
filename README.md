# 카카오톡 채팅방 정리기

카카오톡 "나에게 보내기" TXT/CSV를 한 화면에서 AI 요약·카테고리 분류·프롬프트 추출·엑셀 내보내기로 정리하는 단일 HTML 도구.

🔗 **라이브 데모**: https://commme.github.io/kakao-organizer/

## 결과물

- **`index.html`** — 단일 HTML 파일 (서버 불필요, GitHub Pages 호스팅)

## 핵심 기능

- **한 화면 워크플로우**: 입력 → 보관함에서 AI 알잘딱 처리
- **3단 분류기**: 도메인 매핑 → 키워드 → Gemini 2.5 Flash
- **AI 요약 원클릭**: URL은 30자, 텍스트 메모는 50자로 요약 (길이 강제 제한)
- **프롬프트 자동 추출**: 이미지/영상/개발소스/가이드 4종 자동 분류 (키워드 편집 가능)
- **카테고리 = 1차 / 프롬프트 = 2차 (sub)**: 위계 있는 필터 UI
- **자동 학습**: 카테고리를 바꾸면 도메인→카테고리 매핑을 저장, 다음 import에 반영
- **4종 엑셀/MD 내보내기**: 전체 / AI 요약만 / 프롬프트 .md / 프롬프트 .xlsx
- **KakaoTalk 옐로우 테마**: 카카오톡 브랜드 컬러 (#FEE500) + 따뜻한 다크 UI

## 사용법

### 1) 카톡에서 데이터 내보내기

카카오톡 → 채팅방(나와의 채팅 포함) → 메뉴 → 대화 내보내기 → 텍스트 파일(.txt) 저장

### 2) 도구 실행

```
index.html을 더블클릭 → 텍스트 파일 드래그
```

또는 https://commme.github.io/kakao-organizer/ 접속

### 3) 분류 → AI 요약 → 엑셀 다운로드

- AI 분류·요약은 옵션 (설정에서 Gemini API 키 입력). 키 없어도 도메인/키워드 매핑으로 80% 분류
- **⚡ AI 요약** 버튼 한 번으로 현재 보이는 모든 항목 요약 + 엑셀 다운로드 동시 실행
- **📂** 버튼으로 개별 카테고리 변경 시 도메인 자동 학습

## 기본 카테고리 (16종, AI 사용자 + 라이프 밸런스)

| 영역 | 카테고리 |
|------|----------|
| 일/생산성 | AI/툴 · 개발 · 디자인 · 업무 · 커리어 |
| 정보/학습 | 학습 · 뉴스 · 블로그 |
| 관계/라이프 | SNS · 음식 · 여행 · 건강 · 취미 |
| 자산/소비 | 쇼핑 · 금융 |
| 기타 | 미분류 |

## 사용된 도구

| 영역 | 라이브러리/도구 |
|------|-----------------|
| AI 분류/요약 | Google Gemini 2.5 Flash (사용자 API 키) + urlContext tool |
| 엑셀 내보내기 | SheetJS 0.20.3 |
| UI 폰트 | Pretendard |
| 저장 | localStorage (`kk2_` 네임스페이스) |

## 보안

- 모든 데이터는 **브라우저 로컬에서만 저장** — 외부 서버 전송 없음
- API 키도 localStorage에만 저장
- CSP 메타 태그로 외부 스크립트 차단 (cdnjs, generativelanguage.googleapis.com만 허용)
- 모든 URL은 `isSafeUrl()` 검사 (http/https만 허용, javascript:/data: 차단)
- 모든 동적 사용자 입력은 `textContent` / `createElement`로 처리 (XSS 방지)
- 외부 링크는 `rel="noopener"` + `target="_blank"`

## 라이선스

© 2026 COMMME. All rights reserved.
