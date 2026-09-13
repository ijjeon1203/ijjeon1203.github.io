# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 개요

Hugo(Extended)로 만든 개인 기술 블로그 "JJunney's Blog" (리눅스 · 임베디드 · MLOps · Python 공부 기록).
GitHub Pages 사용자 사이트(`https://ijjeon1203.github.io/`)로, **`master` 브랜치의 저장소 루트가 그대로 서빙된다.**
글·커밋 메시지·주석은 모두 한국어로 작성한다.

## 명령어

```bash
hugo server -D --port 1313 --disableFastRender   # 로컬 미리보기 (.claude/launch.json의 "hugo" 설정과 동일)
hugo                                              # public/ 에 빌드
hugo new <섹션>/<파일명>.md                        # archetypes/default.md 기반 새 글 (draft = true로 생성됨)
git submodule update --init                       # 테마(themes/ananke) 서브모듈 받기
```

테스트·린트 도구는 없다. 변경 확인은 `hugo` 빌드가 에러 없이 끝나는지와 로컬 서버 화면으로 한다.

## 배포 방식 (중요)

별도 CI나 `gh-pages` 브랜치가 없다(README의 gh-pages 절차는 옛날 내용). 배포 흐름:

1. `hugo`로 `public/`에 빌드
2. `public/`의 결과물을 **저장소 루트로 복사** (`cp -r public/* .`)
3. 소스 변경과 함께 루트의 빌드 산출물(`index.html`, `index.xml`, `sitemap.xml`, `404.html`, `css/`, `mlflow/`, `리눅스/` 등)을 커밋 후 `master`에 push

따라서 루트에는 소스(`content/`, `layouts/`, `static/`, `config.toml` …)와 빌드 산출물이 섞여 있다.
- 산출물 디렉토리를 직접 수정하지 말고, 소스를 고친 뒤 재빌드해서 반영한다.
- 레이아웃/CSS/콘텐츠를 바꿨다면 루트 산출물도 갱신해야 실제 사이트에 반영된다.
- `posts/`, `temmis/`, `tags/`, git에 추적 중인 `public/`·`resources/_gen/` 일부는 과거 빌드의 잔재다(`.gitignore`에는 `/public/`, `/resources/_gen/`이 있지만 이전에 커밋된 파일이 남아 있음). 정리 여부는 사용자와 상의한다.
- 이 저장소는 SvelteKit/Sveltepress에서 Hugo로 전환된 이력이 있으며, 관련 작업 기록은 `content/개발일지/`에 남긴다.

## 아키텍처

### 테마와 레이아웃
- `config.toml`에 `theme = "ananke"`(git 서브모듈)가 지정되어 있지만, **실제 화면은 거의 전부 `layouts/`의 커스텀 템플릿이 덮어쓴다** (`baseof`, `index`, `list`, `single`, `terms`, `404`). UI를 바꿀 때는 테마가 아니라 `layouts/`를 수정한다.
- 스타일은 Hugo 파이프라인 없이 `static/css/site.css` 한 파일(블랙 & 레드 테마)이며 `baseof.html`에서 직접 링크한다. 폰트는 CDN(Pretendard, JetBrains Mono).
- 코드 하이라이트 스타일은 `config.toml`의 `markup.highlight.style = "github-dark"`.

### 콘텐츠 규칙
- `content/` 아래 최상위 디렉토리가 곧 섹션이다(`MLFlow`, `리눅스`, `python`, `정규표현식`, `여행`, `개발일지` …). 상단 메뉴(`partials/site-header.html`)와 홈의 섹션 카드는 `site.Sections`에서 **자동 생성**되므로 메뉴 설정이 따로 없다. 섹션 URL은 소문자로 변환된다(`MLFlow` → `/mlflow/`).
- 대부분의 글에 front matter가 없다. 이를 전제로 설계되어 있다:
  - 제목: `partials/func/title.html`이 `.Title`이 비어 있으면 파일명(`ContentBaseName`)을 쓴다. 템플릿에서 제목을 출력할 때는 `.Title` 대신 항상 `partial "func/title.html" .`을 사용한다.
  - 날짜: `config.toml`의 `[frontmatter]` 설정으로 `date`가 없으면 git 커밋 날짜를 쓴다(`enableGitInfo = true`). 커밋되지 않은 글은 날짜가 정확하지 않을 수 있다.
- `developer.md`, `tennis.md`, `book.md`, `movie.md`는 홈의 "Life" 칩으로 `layouts/index.html`에 이름이 하드코딩되어 있다.
- `content/_index.md`가 `draft: true`면 홈 페이지가 빌드에서 빠진다(과거에 실제로 발생).
- 홈의 GitHub 저장소 카드(`partials/github-repos.html`)는 빌드 시점이 아니라 브라우저에서 GitHub API를 호출한다(`site.Params.github` 사용).
