# 카카오톡 채팅방 정리기 — Release Notes

**최종 버전**: 2026-04-19
**라이브 데모**: https://commme.github.io/kakao-organizer/
**저장소**: https://github.com/commme/kakao-organizer

---

## 한 줄 요약

카카오톡 "나에게 보내기"에 쌓인 수백 개 메모/링크를 한 화면에서 AI 요약·자동 분류·프롬프트 추출·엑셀 내보내기로 정리하는 단일 HTML 도구. 카카오톡 옐로우 테마.

---

## 무엇이 바뀌었나 (vs v1)

### 기능
- **AI 요약 원클릭**: ⚡ 버튼 하나로 현재 보이는 모든 항목 요약 + 엑셀 자동 다운로드
- **URL/메모 분기 요약**: URL은 30자 이내(urlContext), 텍스트 메모는 50자 이내. 길이 강제 제한.
- **프롬프트 자동 추출**: 이미지/영상/개발소스/가이드 4종 자동 분류 (설정에서 키워드 편집 가능)
- **카테고리 = 1차 / 프롬프트 = 2차 (sub)**: 위계 있는 필터 UI
- **개별 카테고리 변경 → 도메인 자동 학습**: 📂 버튼으로 1건 변경하면 다음 import에 즉시 반영
- **4종 내보내기 드롭다운**: 보관함 전체 .xlsx / AI 요약만 .xlsx / 프롬프트 .md / 프롬프트 .xlsx
- **누적 import 지원**: 마지막 import 날짜 + 1일로 date-from 자동 채움 (중복 방지)

### 카테고리 (재정의)
SAP 제거, AI 사용자 + 라이프 밸런스 16종으로 재구성:
- **일/생산성**: AI/툴, 개발, 디자인, 업무, 커리어
- **정보/학습**: 학습, 뉴스, 블로그
- **관계/라이프**: SNS, 음식, 여행, 건강, 취미
- **자산/소비**: 쇼핑, 금융
- 미분류

기존 항목은 자동 마이그레이션 (AI→AI/툴, 마케팅→업무, SAP→업무, 러닝/라이프→건강).

### UI
- **카카오톡 옐로우 테마** (#FEE500) + 따뜻한 다크 톤
- 툴바 단순화: `☑ 선택` / `⚡ AI 요약` / `📤 내보내기 ▾` / `🗑`
- URL 카드에 직접 표시 (도메인 chip + 잘린 URL 박스)

### 보안
- CSP `script-src` 화이트리스트 (cdn.sheetjs.com, cdn.jsdelivr.net), `connect-src` Gemini만 허용
- 모든 URL `isSafeUrl()` 검사 (http/https만, javascript:/data: 차단)
- 모든 동적 사용자 입력은 `textContent` / `createElement` (XSS 방지)
- 외부 링크 `rel="noopener"` + `target="_blank"`
- API 키 + 모든 데이터 localStorage 전용 (외부 서버 전송 없음)

---

## 사용법

1. 카톡 채팅방 → 메뉴 → 대화 내보내기 → `.txt` 저장
2. https://commme.github.io/kakao-organizer/ 접속 → 파일 드래그
3. (선택) 설정에서 Gemini API 키 입력 → ⚡ AI 요약 클릭
4. 📤 내보내기 → 원하는 형식으로 다운로드

---

## 핵심 가치

> "쌓아만 두던 카톡 메모를 5분 안에 다 처리하고 비울 수 있다"
> 디지털 Inbox Zero를 카카오톡에 적용

| Perspective | Content |
|-------------|---------|
| **Problem** | 카톡 누적 메모/링크/프롬프트가 분류·검색·재방문 모두 막힘 |
| **Solution** | 한 화면 보관함 + AI 알잘딱 요약 + 프롬프트 sub-카테고리 + 4종 export |
| **Function/UX Effect** | 툴바 단순화, 카테고리 1차 / 프롬프트 2차 위계로 인지 부하 감소, 자동 학습으로 정확도↑ |
| **Core Value** | "내 카톡을 내 라이프 밸런스 카테고리에 자동 정리하고, 프롬프트만 따로 뽑아 재사용한다" |

---

## 사용된 기술

| 영역 | 도구 |
|------|------|
| AI | Google Gemini 2.5 Flash + urlContext tool |
| 엑셀 | SheetJS 0.20.3 |
| UI | Pretendard, Vanilla JS, CSS Variables |
| 저장 | localStorage (`kk2_` 네임스페이스) |
| 호스팅 | GitHub Pages |

---

© 2026 COMMME · eunhwanyu87@gmail.com
