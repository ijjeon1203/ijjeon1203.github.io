---
id: {{ replace (upper .Name) "-" "-" }}
title: "{{ replace .Name "-" " " | title }}"
module: ""
type: feature        # feature / non_feature / gui / user_scenario
priority: medium      # low / medium / high
status: todo          # todo / in_progress / review / done
tags: []
created: {{ .Date.Format "2006-01-02" }}
updated: []           # ["2026-06-25","2026-06-24"] 형태로 이력 누적
decisions: []
---

## 내용

## 조건
- [ ]

## 이슈
- [ ] 이슈 내용

## 결정
- 결정 내용 (날짜)

## 변경 사항
- 최초 생성

## 관련 티켓
-
