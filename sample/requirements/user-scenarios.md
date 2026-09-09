---
id: SC-U-001
title: User Scenarios
module: user
type: user_scenario
priority: high
status: todo
tags: [scenario, user]
created: 2026-09-09
updated:
decisions:
---

## 내용

사이트를 사용하는 대표적인 사용자 시나리오를 정의한다.

## 조건

### 시나리오 1 — 내가 공부한 내용을 찾는다

- [ ] Home에서 Search로 이동
- [ ] 키워드 입력
- [ ] 관련 문서 확인
- [ ] 문서 열람
- [ ] 관련 문서로 이동

### 시나리오 2 — 특정 기술 문서를 찾아본다

- [ ] Knowledge 선택
- [ ] Category 선택
- [ ] 하위 문서 선택
- [ ] TOC를 이용해 원하는 섹션으로 이동

### 시나리오 3 — 프로젝트를 확인한다

- [ ] Projects 선택
- [ ] 프로젝트 카드 확인
- [ ] 프로젝트 상세 페이지 진입
- [ ] Architecture/Implementation 확인
- [ ] GitHub Repository 이동

### 시나리오 4 — 프로젝트와 공부한 내용을 연결한다

- [ ] 프로젝트 상세 페이지에서 Related Knowledge 확인
- [ ] 관련 문서 열람
- [ ] 다시 프로젝트로 돌아갈 수 있어야 한다.

### 시나리오 5 — 모바일에서 참조한다

- [ ] 스마트폰에서 사이트 접속
- [ ] 검색
- [ ] 문서 열람
- [ ] 코드 확인
- [ ] 링크 이동

### 시나리오 6 — 새로운 지식을 추가한다

- [ ] Markdown 작성
- [ ] Front Matter 작성
- [ ] content에 저장
- [ ] 로컬 Hugo build/preview
- [ ] Git commit
- [ ] Git push
- [ ] GitHub Actions 자동 배포
- [ ] 웹에서 확인

## 이슈

- [ ] 모바일 Navigation 방식 결정 필요

## 결정

- 핵심 사용 흐름을 `Search → Read → Related Document`로 설계한다.

## 변경 사항

- 최초 생성

## 관련 티켓

-
