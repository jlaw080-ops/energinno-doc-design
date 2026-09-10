---
name: energinno-doc-design
description: Use this skill to produce Energinno (주식회사 에너지노) general business documents — 기획안, 제안서, 검토서, 보고서 — as print-ready A4 HTML. Contains the grayscale document style, pt-based type scale, Word-default page geometry, table/figure/note conventions, CI usage rules, and an A4 template.
user-invocable: true
---

Read `README.md` in this skill first — it holds the content rules (문체, 개조식, 표제 체계), the visual foundations (지면, 활자, 표, 도해, 각주 박스, 목차), and the CI usage rules.

## Files

- `README.md` — the rules. Read before writing anything.
- `styles.css` → `tokens/colors.css`, `tokens/typography.css`, `tokens/layout.css` — link `styles.css` and use the `--*` tokens; never hard-code new colors or sizes.
- `template/index.html` — A4 표지 + 본문 1면. Copy this and fill in content.
- `template/doc-page.js` — page component. Copy alongside; do not edit.
- `guidelines/*.html` — rendered specimens of each document part (표, 각주 박스, 머리말·꼬리말, 목차, 활자, 색).
- `assets/energinno-logo.png` (가로형 CI), `assets/energinno-symbol.png` (심볼).

## How to build a document

1. Copy `template/index.html`, `template/doc-page.js`, `styles.css`, `tokens/`, `assets/` into the working directory, keeping the relative paths.
2. Fill the cover: 문서 종류, 제목, 문서정보표(작성일·작성·수신·구분).
3. Add one `<section class="page">` per printed page. Each 장(`1.`, `2.`…) starts a NEW page; 절(`가.`, `나.`) continues on the same page.
4. Copy the running header and the footer block into every body page; only the page number changes. 표지에는 넣지 않는다.
5. Check overflow: `.page` clips its content. For every page, verify the last non-absolute child's bottom stays above `clientHeight - paddingBottom`. If a page overflows, split it at a 절 boundary — do not shrink type.
6. Export by printing to PDF at A4.

## Rules that are easy to get wrong

- 회사명은 머리말 CI 한 곳에만 표기한다. 꼬리말은 쪽번호만.
- 가로형 CI는 높이 8mm 미만으로 줄이지 않는다 (태그라인이 뭉개진다). 더 작으면 심볼 단독을 쓴다.
- 본문·표·도해는 무채색만. 컬러는 CI 로고에서만.
- 모서리 라운딩, 그림자, 아이콘, 이모지는 쓰지 않는다.
- 크기는 pt로 지정한다. 도해 안 글자는 지면 기준 12pt 이상.
