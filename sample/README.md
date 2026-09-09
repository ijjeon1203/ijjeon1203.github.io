# PKB + Requirements + Portfolio (Hugo)

# 목적

개인이 작성·축적한 Markdown 지식을 언제 어디서든 참조할 수 있는 Personal Knowledge Base(PKB)를 제공하고, 동시에 개발 프로젝트와 기술 역량을 보여주는 Engineering Portfolio를 제공한다.


# 핵심 방향

- Markdown을 원본 콘텐츠로 유지한다.
- Hugo를 정적 사이트 생성기로 사용한다.
- GitHub Pages를 배포 플랫폼으로 사용한다.
- Knowledge / Notes / Projects / About의 4개 축으로 구성한다.
- Projects는 Portfolio의 핵심이며 프로젝트 상세 정보와 관련 기술 문서를 연결한다.
- 검색, 태그, 분류, 상호 링크를 통해 장기적인 지식 탐색을 지원한다.
- 모바일과 PC에서 모두 사용할 수 있어야 한다.



# Repository

```text
username.github.io/
├── .github/          # push 시 GitHub Pages 자동 배포
│   └── workflows/
│       └── hugo.yml
├── archetypes/
│   └── workflows/
├── assets/
├── content/
├── data/
├── layouts/
├── static/
├── hugo.toml           # taxonomy(module/type/priority/status/tags) 설정 포함
└── README.md
```

# 구조
```
content/
├── requirements/   # 요구사항/이슈/결정 기록 (제공하신 양식 기반)
├── projects/       # 포트폴리오
├── posts/          # 학습 노트 (PKB)
└── about.md
archetypes/
├── requirement.md  # `hugo new requirements/xxx.md` 시 자동으로 양식 채워짐
├── project.md      # `hugo new projects/xxx.md`
└── post.md         # `hugo new posts/xxx.md`
hugo.toml           
```

## Content 역할

| 영역 | 목적 | 원본 |
|---|---|---|
| Knowledge | 정리된 기술 지식 | Markdown |
| Notes | 개발 과정/시행착오 | Markdown |
| Projects | Portfolio | Markdown + assets |
| About | Profile | Markdown |

## 기술 구조

```text
Markdown
   ↓
Hugo
   ↓
HTML / CSS / JS
   ↓
GitHub Pages
```



# 문서 ID 규칙

요구사항 ID: SC-F-001
- SC: Sena/Crypt 계열 프로젝트 식별자
- F: Functional Requirement
- N: Non-Functional Requirement
- G: GUI
- U: User Scenario
- D: Decision

ID는 문서 전체에서 유일해야 한다.

# 상태

- todo
- in_progress
- done
- blocked
- archived

# 우선순위

- high
- medium
- low

# 요구사항 문서 작성 원칙

모든 요구사항은 `requirements/` 아래 Markdown으로 관리한다.
각 요구사항에는 id, title, module, type, priority, status, tags, created, updated, decisions를 기록한다.
변경 이력은 `변경 사항`, 논의 내용은 `이슈`, 확정 근거는 `결정`에 기록한다.



# 시작하기

1. 테마 설치 (PaperMod 예시, 이미 다른 테마 쓰고 계시면 생략)
```bash
git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod --depth=1
```

2. 로컬 확인
```bash
hugo server -D
```

3. 새 요구사항 문서 만들기 (아키타입이 자동으로 양식 채워줌)
```bash
hugo new requirements/sc-f-002.md
```

4. 새 포트폴리오 항목 만들기
```bash
hugo new projects/새프로젝트명.md
```

5. `hugo.toml`의 `baseURL`을 본인 `https://아이디.github.io/`로 수정

6. GitHub 저장소 Settings → Pages → Source를 **GitHub Actions**로 설정하면
   `main` 브랜치에 push할 때마다 `.github/workflows/hugo.yml`이 자동 빌드/배포합니다.

# 요구사항 문서(id/module/type/priority/status) 활용 팁

- `module`, `type`, `priority`, `status`는 `hugo.toml`에 커스텀 taxonomy로 등록해뒀습니다.
  즉 `/modules/scheduler/`, `/statuses/todo/`, `/priorities/high/` 같은 URL로
  **자동 목록 페이지**가 생성됩니다 (레이아웃만 있으면 필터링된 리스트로 바로 보임).
- `updated` 필드는 배열로 두고, 문서 수정할 때마다 날짜를 append 하면
  "변경 이력"을 front matter만으로 추적할 수 있습니다.
- `status`별 대시보드(칸반 형태)가 필요하면 나중에
  `layouts/requirements/list.html`을 커스텀해서 status별로 그룹핑하는 템플릿을
  추가하면 됩니다 (지금은 기본 리스트만 뜨는 상태).

## 다음에 추가하면 좋은 것
- [ ] `layouts/requirements/list.html` — status별 칸반 뷰
- [ ] 검색 기능 (PaperMod 기본 지원, `[outputs] home = ["HTML","RSS","JSON"]` 이미 설정해둠)
- [ ] `static/images/projects/`에 포트폴리오 스크린샷 추가 후 `cover` 필드 연결
