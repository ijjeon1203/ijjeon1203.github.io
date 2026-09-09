---
id: SC-F-010
title: Engineering Portfolio
module: portfolio
type: feature
priority: high
status: todo
tags: [portfolio, projects, engineering]
created: 2026-09-09
updated:
decisions:
---

## 내용

개발 프로젝트와 기술적 문제 해결 경험을 정리하여 Engineering Portfolio로 제공한다.

## 조건

- [ ] Projects 목록 페이지 제공
- [ ] Featured Projects 제공
- [ ] 프로젝트별 상세 페이지 제공
- [ ] 프로젝트 개요 표시
- [ ] 프로젝트 목표 표시
- [ ] 문제 정의 표시
- [ ] 역할 표시
- [ ] 기술 스택 표시
- [ ] Architecture 표시
- [ ] 주요 구현 내용 표시
- [ ] 기술적 이슈와 해결 과정 표시
- [ ] 결과 및 성과 표시
- [ ] 프로젝트 상태 표시
- [ ] GitHub Repository 링크 제공
- [ ] Demo 링크 제공 가능
- [ ] 관련 Knowledge 문서 링크 제공
- [ ] 프로젝트별 이미지/다이어그램 제공 가능
- [ ] 프로젝트를 태그 또는 기술 기준으로 분류

## 이슈

- [ ] 프로젝트 카드에 표시할 기본 정보 결정 필요
- [ ] 성과를 수치화할 수 없는 프로젝트의 표현 방법 결정 필요

## 결정

- Portfolio는 별도의 기술 스택을 갖는 애플리케이션이 아니라 Hugo의 Projects content type으로 구현한다.
- 프로젝트 상세 문서는 Markdown으로 관리한다.
- Portfolio에서 관련 Knowledge 문서로 이동할 수 있도록 한다.

## 변경 사항

- 최초 생성

## 관련 티켓

-
