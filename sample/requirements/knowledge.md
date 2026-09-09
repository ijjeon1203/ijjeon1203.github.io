---
id: SC-F-001
title: Markdown Knowledge Base
module: knowledge
type: feature
priority: high
status: todo
tags: [markdown, knowledge, documentation]
created: 2026-09-09
updated:
decisions:
---

## 내용

개인이 작성한 Markdown 파일을 장기적인 개인 지식베이스로 축적하고 웹에서 언제든 참조할 수 있어야 한다.

## 조건

- [ ] `.md` 파일을 원본 콘텐츠로 유지한다.
- [ ] Markdown을 HTML로 자동 변환한다.
- [ ] 코드 블록을 지원한다.
- [ ] C, C++, Python, Bash, YAML, JSON 등의 syntax highlighting을 지원한다.
- [ ] 이미지와 첨부 파일을 문서와 함께 관리한다.
- [ ] 문서 내부 목차(TOC)를 제공한다.
- [ ] 문서 간 cross reference를 지원한다.
- [ ] 상위/하위 문서 navigation을 제공한다.
- [ ] Breadcrumb을 제공한다.
- [ ] 카테고리와 태그를 제공한다.
- [ ] 문서별 생성일/수정일을 표시할 수 있다.
- [ ] 장문 문서를 읽기 편한 typography로 제공한다.

## 이슈

- [ ] 기존 Markdown 파일의 Front Matter 표준화 필요
- [ ] 이미지 저장 위치 표준화 필요

## 결정

- Hugo Content와 Page Bundle 구조를 기본으로 사용한다.

## 변경 사항

- 최초 생성

## 관련 티켓

-
