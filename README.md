# Jeon In Jun


---
# 기본 베이스 
Sveltepress 


# 개발환경 세팀 

npm 설치(공식사이트)
- v22.18.0
 - 기본설정 npm 같이 설정됨
 - window에서 path 추가 안하면 동작하지 않음


npm install   # 처음 실행 시 한 번
- node_modules 폴더 및 vite 생성됨 
에러발생
- 해결 : npm audit fix


npm run dev   # 개발 서버 실행


npm run build

결과물은 dist/ 폴더에 생성


'''
GitHub Pages에 맞게 vite 설정 수정
svelte.config.js나 vite.config.js에 base 경로 추가해야 합니다.

// vite.config.js
import { defineConfig } from 'vite';
import { svelte } from '@sveltejs/vite-plugin-svelte';

export default defineConfig({
  plugins: [svelte()],
  base: '/레포지토리이름/', // 꼭 본인 repo 이름으로
});

'''

# GitHub Pages에 업로드

- dist/를 gh-pages 브랜치에 올리거나
- gh-pages npm 패키지 사용해서 자동 배포 가능:


npm install --save-dev gh-pages

# package.json

"scripts": {
  "dev": "vite",
  "build": "vite build",
  "preview": "vite preview",
  "deploy": "gh-pages -d dist"
}


# 배포 

npm run deploy 




---

git

go

hugo 

설치
# scoop 
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
iwr -useb get.scoop.sh | iex


scoop --version
---
title: Welcome to Sveltepress
heroImage: /dog.png
tagline: Persenal Projects


features:
  - title: Git 분석 
    description: About Git 
    to: https://github.com/ijjeon1203

  - title: PythonProject
    description: Python
    to: https://github.com/ijjeon1203


  - title: Application
    description: flutter 
    to: https://github.com/ijjeon1203





# 1. 작업 디렉토리 생성 및 이동
cd D:\workspace
hugo new site ijjeon1203.github.io
cd ijjeon1203.github.io

# 2. Git 초기화
git init
git remote add origin https://github.com/<USERNAME>/ijjeon1203.github.io.git

# 3. 테마 설치 (예: Ananke 테마)
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke

# 4. hugo.toml에 테마 설정
# PowerShell에서 간단히 echo로 설정 가능
echo 'theme = "ananke"' > hugo.toml

# 5. 새 컨텐츠 생성 (예: 첫 번째 포스트)
hugo new posts/my-first-post.md

# 6. 로컬 서버 실행 (초안 포함)
hugo server --buildDrafts

# 7. 배포 준비: 정적 파일 생성
hugo -D

# 8. 배포용 branch로 이동 (GitHub Pages용)
git checkout -b gh-pages
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

##  테스트
hugo server --buildDrafts

새 테마 적용 후 로컬 미리보기 확인
🔹 주의 사항

테마 변경만으로는 기존 content/ 구조가 자동으로 새 테마와 호환되지 않을 수 있음

일부 테마는 SCSS 빌드가 필요하므로 Hugo Extended 필요

테마 내부 static/과 layouts/ 파일이 새 테마 스타일로 덮어쓰기 됨