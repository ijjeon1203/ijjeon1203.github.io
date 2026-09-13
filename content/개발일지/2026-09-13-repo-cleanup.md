---
title: "저장소 정리: SvelteKit/Sveltepress 잔재 제거"
date: 2026-09-13
---

## 배경

저장소를 분석하던 중, 예전에 Sveltepress/SvelteKit으로 사이트를 만들다가 Hugo로
전환한 흔적이 정리되지 않고 그대로 커밋되어 있는 것을 발견했다.

- `node_modules/` 가 통째로 git에 커밋되어 있었음 (17,996개 파일)
- 정작 그걸 설치했을 `package.json`은 저장소 어디에도 없음 (테마 서브모듈 내부 제외)
- `.svelte-kit/`, `.sveltepress/`, `src/routes/+page.md` 도 같은 이유로 잔재로 남아있었음
- `.git` 디렉토리가 132MB까지 불어난 주 원인이었음

## 작업 내역

1. **`.gitignore` 정비**
   - 처음엔 `node_modules/`, `.svelte-kit/`, `.sveltepress/` 등을 ignore 규칙으로
     추가했으나, 이미 git에 추적(tracked)된 파일들이라 gitignore만으로는
     저장소에서 사라지지 않는다는 점을 확인함
   - 논의 후 "무시"가 아니라 "완전 삭제"로 방향을 바꿈
   - Hugo가 빌드 때마다 재생성하는 `.hugo_build.lock`, `/public/`,
     `/resources/_gen/`, `.hugo_cache/` 만 계속 ignore 대상으로 유지

2. **죽은 산출물 삭제** (`git rm -r`)
   - `node_modules/`
   - `.svelte-kit/`
   - `.sveltepress/`
   - `src/` (구 SvelteKit 라우트, `src/routes/+page.md`)
   - 총 18,011개 파일 삭제, 커밋 `cd3b59cb`

## 남은 이슈

- `git rm`은 워킹 트리/인덱스만 정리할 뿐, 과거 커밋 히스토리에는 삭제된
  파일들의 objects가 그대로 남아있어 `.git` 용량(132MB)은 줄어들지 않음
- 진짜로 저장소 용량을 줄이려면 `git filter-repo` 등으로 히스토리 자체를
  재작성해야 하는데, 이는 파괴적인 작업(강제 푸시 필요, 협업자 영향)이라
  별도로 상의 후 진행하기로 함
- 그 외 발견된 정리 후보 (아직 미착수)
  - `public/` 폴더와 루트의 빌드 산출물(`book/`, `movie/`, `temmis/` 등)이
    중복 저장되고 있음
  - `temmis/`는 `tennis/`의 오타로 보이는 중복 디렉토리
  - `config.toml`의 `title`이 공백, 메뉴 이름이 `"2"`, `"3"`, `"4"`로만 되어 있음
