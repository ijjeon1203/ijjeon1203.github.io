---
title: "Git Submodule vs Google repo 정리"
date: 2026-09-01
draft: false
tags: [gitlab, jetson, multi-repo]
categories: [embedded]
summary: "멀티 레포 관리 전략 비교 및 선택 기준"
---

## 요약
Submodule과 `repo`는 멀티 레포 통합 전략으로서 경쟁 관계이며, Worktree는 로컬 개발 보완 도구다.

## 본문
- 레포 2~5개 규모: Submodule
- 레포 10개 이상: `repo` + `manifest.xml`
- NVIDIA L4T/BSP 생태계는 이미 `repo`에 익숙 → Jetson 컨텍스트에서 진입장벽 낮음

## 참고 자료
