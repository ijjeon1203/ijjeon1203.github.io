---
title: "Jetson 멀티 레포 CI/CD 구조 설계"
date: 2026-09-01
draft: false
summary: "Jetson BSP/커널 모듈을 다수의 종속 프로젝트가 소비하는 GitLab 멀티 레포 구조 설계"
stack: ["GitLab CI", "Git Submodule", "L4T", "Jetson"]
role: "임베디드 빌드/배포 구조 설계"
period: "2026.06 - 진행중"
repo_url: ""
cover: ""
featured: true
---

## 개요
커널, BSP, PCIe 공통 코드를 포함한 코어 모듈 레포와 이를 소비하는 다수의 종속 프로젝트를 GitLab 그룹/서브그룹 구조로 관리.

## 담당 역할
- Git Submodule vs `repo` 툴 비교 및 채택
- GitLab 그룹/서브그룹 및 CI 변수 스코핑 설계

## 기술 스택
GitLab CI, Git Submodule, L4T/BSP

## 주요 성과 / 트러블슈팅
- 레포 규모(2~5개) 기준 Submodule 채택, 확장 시 `repo` 전환 기준 수립

## 관련 링크
