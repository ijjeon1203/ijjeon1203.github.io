# 구조 

| 폴더                | 설명                                    |
| ----------------- | ------------------------------------- |
| `archetypes/`     | 새 글 작성 시 기본 템플릿                       |
| `assets/`         | SCSS, JS 등 Hugo가 처리해야 하는 리소스          |
| `content/`        | **마크다운 글 위치** (ex. posts, categories) |
| `data/`           | JSON/YAML 데이터 파일                      |
| `layouts/`        | HTML 템플릿 (커스텀 페이지용)                   |
| `public/`         | **빌드 결과물 (출력용 HTML)**                 |
| `resources/_gen/` | 빌드시 생성된 중간 결과                         |
| `static/`         | 이미지, CSS 등 그대로 복사되는 파일                |
| `themes/ananke/`  | Ananke 테마 파일들                         |
| `config.toml`     | 사이트 설정 파일                             |

data 대신 contents에 넣어야함 




# Setting
## 테마 설치 (예: Ananke 테마)
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke

## hugo.toml에 테마 설정
PowerShell에서 간단히 echo로 설정 가능
- echo 'theme = "ananke"' > hugo.toml

## 새 컨텐츠 생성 (예: 첫 번째 포스트)
- hugo new posts/my-first-post.md

# public 폴더 내용 추가
cp -r public/* .
git add .
git commit -m "Deploy Hugo site"
git push origin gh-pages --force

# 테마 변경방법

## 기존 테마 삭제

기존 테마가 themes/<OLD_THEME>에 있다면 그냥 삭제하면 됩니다:
rm -rf themes/OLD_THEME

## 새 테마 설치

테마 저장소를 themes/<NEW_THEME>로 클론:
git clone https://github.com/themename/newtheme.git themes/NEW_THEME
또는 Hugo Modules 사용 시:
hugo mod get github.com/themename/newtheme

## config.toml 수정

새 테마를 사용하려면 config.toml에서 테마 이름을 바꿔야 합니다:
theme = "NEW_THEME"
기존 설정(params, menu, baseURL 등)이 새 테마와 호환되는지 확인 필요
테마별로 요구하는 SCSS, shortcodes, layouts 등이 다를 수 있음

# 배포 

배포 준비: 정적 파일 생성
- hugo -D
- publish 폴더 생성 

배포용 branch로 이동 (GitHub Pages용)
- git checkout -b gh-pages

cd publish
- 생성된 publish 폴더로 접근

git add .
- 전체 사항 add

git commit -m "msg"
- 커밋하고 메시지 등록 

git push --set-upstream origin master
- 저장소 올리기

# How to use hugo 

# 테스트
hugo server --buildDrafts

새 테마 적용 후 로컬 미리보기 확인
🔹 주의 사항

테마 변경만으로는 기존 content/ 구조가 자동으로 새 테마와 호환되지 않을 수 있음

일부 테마는 SCSS 빌드가 필요하므로 Hugo Extended 필요

테마 내부 static/과 layouts/ 파일이 새 테마 스타일로 덮어쓰기 됨

public 폴더는 빌드 산출물 
- 추후 cicd or public 있는 브랜치 

즉, hugo.toml 대신 config.toml로 두어도 Hugo는 똑같이 읽습니다.
단, 동시에 두 개 이상 있으면 우선순위가 있어서 hugo.toml이 config.toml보다 먼저 읽힙
