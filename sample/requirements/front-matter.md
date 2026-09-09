---
id: SC-F-050
title: Content Front Matter
module: content
type: feature
priority: high
status: todo
tags: [markdown, frontmatter, metadata]
created: 2026-09-09
updated:
decisions:
---

## 내용

모든 콘텐츠의 metadata를 일관되게 관리한다.

## 기본 양식

```yaml
---
id: SC-F-001
title: 제목
module: scheduler
type: feature
priority: high
status: todo
tags: [issue, decision]
created: 2026-06-25
updated:
decisions:
---
```

## 조건

- [ ] 모든 관리 대상 문서에 id를 부여한다.
- [ ] title을 정의한다.
- [ ] module을 정의한다.
- [ ] type을 정의한다.
- [ ] priority를 정의한다.
- [ ] status를 정의한다.
- [ ] tags를 정의한다.
- [ ] created를 정의한다.
- [ ] updated를 관리한다.
- [ ] decisions를 기록한다.

## 이슈

- [ ] `updated`를 배열로 저장할지 Hugo의 lastmod 단일 값으로 관리할지 결정 필요
- [ ] Portfolio 전용 metadata 추가 필요

## 결정

- 기존 요구사항 문서 양식을 기본 메타데이터 규칙으로 사용한다.
- Hugo에서 실제 페이지 렌더링에 필요한 표준 Front Matter와 프로젝트 관리용 metadata를 필요에 따라 구분한다.

## 변경 사항

- 최초 생성

## 관련 티켓

-
