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
