---
id: SC-N-001
title: Non Functional Requirements
module: platform
type: non_feature
priority: high
status: todo
tags: [performance, accessibility, maintainability]
created: 2026-09-09
updated:
decisions:
---

## 내용

사이트의 품질, 유지보수성, 성능 및 접근성 요구사항을 정의한다.

## 조건

- [ ] 정적 사이트로 배포 가능해야 한다.
- [ ] GitHub Pages에서 동작해야 한다.
- [ ] GitHub Actions로 자동 배포할 수 있어야 한다.
- [ ] Markdown과 layout을 분리해야 한다.
- [ ] 콘텐츠 수정 시 HTML을 직접 수정하지 않아도 되어야 한다.
- [ ] 빌드 결과가 재현 가능해야 한다.
- [ ] 외부 서버/DB 의존성을 최소화한다.
- [ ] 모바일에서 읽을 수 있어야 한다.
- [ ] 일반적인 접근성 기준을 고려한다.
- [ ] 페이지 로딩을 가볍게 유지한다.
- [ ] SEO 기본 요소를 제공한다.
- [ ] RSS/Atom 등 피드 제공을 검토한다.
- [ ] 깨진 내부 링크를 주기적으로 확인할 수 있어야 한다.

## 이슈

- [ ] Pagefind 등 외부 JS 의존성 관리
- [ ] Analytics 사용 여부

## 결정

- Backend/Database 없는 정적 사이트를 기본으로 한다.
- Hugo를 정적 사이트 생성기로 사용한다.
- GitHub Actions를 배포 자동화에 사용한다.

## 변경 사항

- 최초 생성

## 관련 티켓

-
