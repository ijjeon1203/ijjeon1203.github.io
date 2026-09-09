---
id: SC-F-040
title: Content Architecture
module: architecture
type: feature
priority: high
status: todo
tags: [architecture, content, hugo]
created: 2026-09-09
updated:
decisions:
---

## 내용

Knowledge Base와 Portfolio 콘텐츠의 물리적/논리적 구조를 정의한다.

## 조건

- [ ] Knowledge는 기술/주제 중심으로 분류한다.
- [ ] Notes는 시간순 기록으로 관리한다.
- [ ] Projects는 프로젝트 단위로 관리한다.
- [ ] About은 프로필 정보로 관리한다.
- [ ] 프로젝트 상세 페이지는 Page Bundle을 사용할 수 있다.
- [ ] 이미지와 문서 관련 파일은 가능한 경우 해당 Page Bundle과 함께 관리한다.
- [ ] taxonomy를 통해 tags/topics를 제공한다.

## 권장 구조

```text
content/
├── knowledge/
│   ├── programming/
│   ├── linux/
│   ├── embedded/
│   ├── robotics/
│   ├── ai/
│   └── tools/
│
├── notes/
│
├── projects/
│   ├── heartos/
│   │   ├── index.md
│   │   ├── architecture.png
│   │   └── ...
│   ├── sena/
│   │   └── index.md
│   └── ...
│
└── about/
    └── index.md
```

## 이슈

- [ ] 기존 Markdown 파일을 Knowledge와 Notes 중 어디에 배치할지 정리 필요

## 결정

- `Knowledge = 정리된 지식`
- `Notes = 개발 과정의 기록`
- `Projects = Portfolio`
- `About = Profile`

## 변경 사항

- 최초 생성

## 관련 티켓

-
