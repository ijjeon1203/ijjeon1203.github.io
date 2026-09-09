---
id: SC-D-001
title: Platform Decisions
module: platform
type: decision
priority: high
status: done
tags: [decision, hugo, github-pages]
created: 2026-09-09
updated:
decisions:
---

## 내용

플랫폼과 사이트 구조에 대한 확정 사항을 기록한다.

## 조건

- [x] Personal Knowledge Base를 사이트의 중심으로 한다.
- [x] Portfolio 기능을 포함한다.
- [x] Markdown을 원본 콘텐츠로 유지한다.
- [x] Hugo를 사용한다.
- [x] GitHub Pages를 배포 대상으로 한다.
- [x] GitHub Actions를 사용한 자동 배포를 기본으로 한다.
- [x] Knowledge / Notes / Projects / About 구조를 사용한다.
- [x] Projects를 Engineering Portfolio로 사용한다.

## 이슈

- [ ] 최종 테마 결정
- [ ] 검색 도구 결정
- [ ] 도메인 사용 여부 결정
- [ ] Analytics 사용 여부 결정

## 결정

### Hugo 선택

Personal Knowledge Base는 장기적으로 문서 수가 증가할 가능성이 높고, 계층적인 content 구조, Markdown, Page Bundle, taxonomy, cross reference 및 빠른 정적 빌드가 중요하다. 따라서 Jekyll보다 Hugo를 우선한다.

### Portfolio 통합

Portfolio를 별도 서비스로 분리하지 않고 Hugo Projects 영역으로 통합한다. 프로젝트에서 관련 Knowledge/Notes를 참조할 수 있도록 한다.

### 사이트 역할

```text
github.io
├── Knowledge  → 정리된 기술 지식
├── Notes      → 개발 과정의 기록
├── Projects   → Engineering Portfolio
└── About      → 개발자 Profile
```

## 변경 사항

- 최초 결정

## 관련 티켓

-
