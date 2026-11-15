# AItutor21 MindMap

단일 HTML 파일로 동작하는 마인드맵 편집기입니다. 설치 없이 `index.html`을 브라우저에서 열면 됩니다.

## 화면

마인드맵 편집 화면

![마인드맵 편집 화면](screenshots/01-mindmap.png)

온톨로지 지식 그래프

![온톨로지 지식 그래프](screenshots/02-ontology-graph.png)

트리플(S-P-O) 표

![트리플 표](screenshots/03-ontology-triples.png)

컨텍스트 그래프

![컨텍스트 그래프](screenshots/04-context-graph.png)

AI 비주얼 요약 (Claude·Gemini를 쓸 수 없을 때 나오는 요약 포스터)

![요약 포스터](screenshots/05-summary-poster.png)

## 파일

- `index.html` — 수정본 (아래 "원본 대비 수정 내역" 반영)
- `original/aitutor21_mindmap.html` — 원본 그대로
- `screenshots/` — 위 화면 캡처 (기본 예시 맵, 1440×810 창 기준)

## 기능

- 마인드맵 편집: Tab(하위 노드), Enter(동급 노드), Space/더블클릭(텍스트 편집), 방향키(이동), Delete(삭제), Ctrl+Z/Y(실행 취소/다시 실행)
- 자동 정렬, 확대/축소, 드래그 이동
- 온톨로지 패널: 트리플(S-P-O) 표, Turtle / JSON-LD / Neo4j Cypher 내보내기
- 컨텍스트 그래프 패널: 도메인별 분석, GraphRAG 청크 / Mermaid / JSON 내보내기
- JSON 저장·불러오기, PNG 내보내기
- Google Drive 저장·열기 (본인 OAuth Client ID 입력 필요)
- AI 비주얼 요약: 마인드맵 내용으로 그림 한 장 생성

## AI 비주얼 요약 동작 순서

1. Claude 게시 페이지에서 열린 경우: Claude가 마인드맵 내용으로 SVG 일러스트를 그립니다.
2. 그 외 환경에서 Gemini API 키를 입력한 경우: Gemini 이미지 모델을 호출합니다.
3. 둘 다 없으면: 마인드맵 내용을 좌우 카드로 정리한 요약 포스터를 캔버스로 그립니다.

API 키와 OAuth Client ID는 코드에 들어 있지 않으며, 사용자가 입력하면 브라우저 localStorage에만 저장됩니다.

## 원본 대비 수정 내역

- 요약 포스터가 마인드맵과 무관한 고정 도면을 그리던 문제 수정 → 마인드맵 내용만 그림
- Gemini 프롬프트의 고정 주제 문구 제거 → 마인드맵 내용만 사용하도록 지시
- Tailwind CDN 스크립트 제거 → Tailwind CLI 3.4.17로 미리 빌드한 CSS를 `<style>`로 포함 (CDN 경고 제거)
- 파일 저장(JSON, PNG, 포스터)을 공통 함수로 정리
- 파비콘 404 제거

## 알려진 문제

- Google Drive "열기"가 참조하는 `modal-gdrive-files`, `drive-files-list` 요소가 HTML에 없어, 로그인 후 열기를 누르면 오류가 납니다 (원본부터 있던 문제, 미수정).
- Tailwind 클래스를 새로 추가하면 CSS를 다시 빌드해야 적용됩니다.
- Gemini 호출 경로와 Google Drive 연동은 실제 키로 시험하지 않았습니다.
