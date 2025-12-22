# Git

Git
Git 은 분산형 버전 관리 시스템으로 많은 오픈 소스 프로젝트가 git을 이용하여 소스 코드의 버전 관리를 하고 있다. 특히 SVN과 달리 분산형이기 때문에 네트워크에 접속되지 않아도 commit을 작성할 수 있는 점과 branch를 이용하여 작업 영역의 분리와 merge를 통한 통합을 이용할 수 있다.
참고할 만한 자료
git 은 나온지 2005 년에 배포되기 시작해서 인터넷에 많은 자료들이 존재한다.
Git 프로젝트 자체에서 배포하고 있는 Pro Git 한글, Pro Git 영문은 git 사용에 대한 상세한 내용을 다루고 있다. GitHub Guides 는 git을 GitHub에 맞게 사용하는 방법과 작업 흐름에 대한 기본적인 설명을 하고 있다. git - 간편 안내서은 git 사용법에 대해서 간략하고 빠르게 설명하고 있다. A successful Git branching model 은 브랜치의 효과적인 운용 방법에 대해서 설명하고 있으며, 이와 유사하게 GitHub Flow 나 GitLab Flow 도 존재한다. 지옥에서 온 Git 와 같이 동영상 강의도 확인해 볼만 하다.
Pro Git의 경우 너무 자세한 내용 까지 서술 되어 있어 보는데 시간이 걸릴 수 있다. 따라서 git - 간편 안내서, GitHub Guides, GitHub Flow을 미리 읽을 것을 추천한다. 특히 Git Tutorial - Try Git 에서 git 명령어의 사용 방법을 공부해 볼 것을 권장한다.
GUI 클라이언트
git 은 기본적으로 CUI 를 제공하기 때문에 명령어의 숙지가 필요하며, 작업을 위한 모든 사항을 직접 입력해 사용에 불편함이 있다. 이를 해결하기 위해서 많은 Git GUI 클라이언트가 존재하며, https://git-scm.com/downloads/guis 에 목록이 있다. 이 중 무료 이면서 사용에 편리한 GitKraken, Egit 을 추천한다.


용어
repository :저장소
fetch?



Branch 이름 규칙
branch 는 작업 별로 생성하면 되며, 로컬에서만 사용하는 branch의 경우 push 할 필요가 없다. branch 이름은 master, develop, release 를 제외한 겹치지 않는 이름으로 작성하고, 이름에서 어떤 작업을 하고 있는지 연상 되도록 영어로 작성한다. 또한 이름에 공백이 들어갈 경우 되도록 _ 가 아닌 -으로 입력한다.
Commit 규칙
Commit 작성
commit 은 날자별로 작성하는 것이 아닌 기능 혹은 작업 단위로 작성한다. commit 은 되도록 분리 될 수 있는 형태로 작성하며, 의존 관계가 있을 경우 작업한 내용을 하나로 묶어 commit 하면 된다. 또한 해당 기능 또는 작업이 하나의 파일만 수정하는 독립적인 commit 이 아닌 이상 수정할 때 마다 매번 commit 을 남겨서는 안된다.
만약 작업이 완료되지 않았지만 작업의 중간 단계를 보존하고 싶을 경우가 있을 수 있다. 이는 현재 까지 작성한 내용을 commit하고 amend 기능을 사용하여 commit 내용을 점진적으로 수정하면 된다. 또는 rebase의 squash 기능을 이용하여 작성해 둔 commit 들을 하나로 합치면된다. 단, amend 나 squash 를 사용할 때는 해당 commit 이 완성 될 때까지 원격 저장소에 push 해서는 안된다. 원격 저장소로 push 된 commit 이 강제로 변경될 경우 충돌이 발생할 수 있기 때문에, 여럿이서 사용하는 branch 가 아닌 이상 사용에 주의해야한다.
Commit 메시지 양식
commit 메시지는 다음과 같이 작업 사항에 대한 간략한 제목을 한 줄로 작성하거나
작업 사항에 대한 간략한 제목

다음 처럼 간략한 제목 작성 후 두 줄 아래에 추가한 내용은 +, 제거한 내용은 -, 수정한 내용은 * 을 붙여 작업 사항을 한 줄 단위로 작성한다.
작업 사항에 대한 간략한 제목

+ 간략하게 추가한 기능 또는 내용 서술
- 간략하게 제거한 기능 또는 내용 서술
* 간략하게 수정한 기능 또는 내용 서술

만약 별도의 GUI 클라이언트를 사용한다면, 해당 클라이언트가 제목과 상세 내용 사이에 자동으로 한 줄을 추가해 줄 것이기 때문에 크게 신경쓸 필요가 없다. 단, egit 같은 경우 제목입력 항목이 따로 없기 때문에 직접 제목과 내용사이에 한 줄을 추가해야한다. 또한 egit 은 commit 메시지의 한 줄의 길이에 따라 자동 줄 내림을 하니 이 부분은 옵션을 주어 자동 줄내림을 해지해야한다.
추가로 위 메시지 작성 규칙을 CUI 환경에서 작성하고 싶을 경우, Windows 는 아래와 같이 메시지를 입력하면 된다.
git commit -m "제목" -m ^
More?
More? "+ 추가 내용"^
More?
More? "- 제거 내용"^
More?
More? "* 수정 내용"

Linux 는 아래와 같이 메시지를 입력하면 된다.
git commit -m "제목

+ 추가 내용
- 제거 내용
* 수정 내용"

Push 규칙
master, develop, release branch는 저장소의 매우 중요한 브랜치로 함부로 제거하거 수정되어 서는 안되기 때문에, 기본적으로 push 와 merge 기능을 막는다. 해당 branch 들은 Merge Requests 기능을 통해서만 작성한 commit 들을 입력할 수 있다.
또한 이미 원격 저장소에 push 된 branch 를 force push 할 경우 충돌이 발생할 수 있으므로, 여럿이서 사용하는 branch 가 아닌 이상 사용에 주의해야한다.
Merge 및 Merge Requests 규칙
Merge Requst는 merge 권한이 없는 개발자가 권한자에게 branch 간 merge를 요청하는 기능이다. master, develop, release는 push 기능이 막혀 있기 때문에 Merge Requst를 통해 작업한 branch 를 반영해야한다. 그 외의 branch 들은 Merge Request를 사용하거나, 로컬에서 merge를 하고 push를 하는 방법을 자유롭게 이용하면된다.
master와 release 는 배포용 branch로 실제 두 branch에서 개발 작업을 진행 하지 않으며, develop branch에서 개발작업을 진행한다. 작업 사항은 develop branch 로 Merge Request 를 요청하면 된다.
Merge Request 를 요청할 때 아래와 같은 양식의 내용을 작성하여 요청한다.
Merge Requst 양식
# 목적

해당 merge request에 대해 목적을 기술한다.

# 작업 사항

- [x] 세부 작업의 개략적 내용을 작성, 작업이 완료된 경우 대괄호에 x를 채움
- [] 세부 작업의 개략적 내용을 작성, 작업이 완료되지 않았을 경우 대괄호를 비움

# 상세 내용

## 위에서 작성한 세부 작업 내용을 동일하게 작성

세부 작업에 대한 상세 내용을 기술한다.

## 위에서 작성한 세부 작업 내용을 동일하게 작성

세부 작업에 대한 상세 내용을 기술한다.

예시
기본 작업 흐름
프로그램이 실행 되면 Hello World! 가 출력되는 기능을 추가 하기 위한 작업을 해야 한다고 생각해보자. 이러한 기능을 작성하기 위한 작업 흐름은 다음과 같다.
일단 저장소에 있는 소스 코드를 clone 하고 해당 디렉토리로 이동한다.
git clone --recursive http://git.kangwon.ac.kr/iic/indurop.git
cd indurop

새로운 기능 추가를 위해 작업할 boot-echo branch 를 생성한다.
git checkout -b boot-echo

Hello World! 를 출력할 소스 코드를 echo.cpp에 작성한다.
// echo.cpp
#include <iostream>
intecho(){
    std::cout<<"Hello World!";
    return0;
}
staticintisCalled=echo();

작업한 파일을 commit 에 추가히기 위해 staged 상태로 만든다.
git add echo.cpp

commit 을 작성한다.
git commit -m "프로그램 실행시 메시지 출력 기능 작성"

작성한 commit 있는 boot-echo branch를 원격 저장소로 push
git push origin boot-echo

develop branch 에 작업 사항을 반영하기 위해서 Merge Request 작성
1. https://git.kangwon.ac.kr/iic/indurop 의 Merge Requests 로 이동
1. New Merge Request 클릭


reset으로 할경우 다 날아감
commit

동시에 땡기는건 ㄴㄴ
경로 git이 프로젝트를 잡는것 경로가 같아야함


git  /git hub for windows

# 문법

git
정보확인
git config --global --list

remote: Permission to anroniogi/SLAM.git denied to hengzizng.

처음 사용자가 있을경우 사용자 추가하면 덮어쓰기가 되네
그리고 push하면 생기는 에러

다른컴터에서 push한거 반영하기
git clone --recursive http://git.kangwon.ac.kr/iic/indurop.git
cd indurop
//git clone 사용자명@호스트:/원격/저장소/경로
git checkout -b background

#include <iostrem>

int background()
{
 std::cout<<"Hellow world"
 return 0;
}


static int isCalled =echo();

git add echo.cpp
git commit -m

git push origin boot-echo


working directory-real file
index staging area
head

최종확정본

변경된 파일 index에 추가
git add <파일 이름>
git add*
변경 내용 확정
git commit –m“이번 확정본에 대한 설명”

git push origin master  
다른 가지 발행하려면
git push origin name



add라는 이름의 가지
git checkout –b add

master 가지로 돌아옴
git checkout master

가지 삭제
git branch –d add

병합전 비교
git diff <원래><비교 대상가지>

원격서버 주소 git에게 알려주가
git remote add origin <원격 서버주소>

식별자 얻기 명령어
git log

얻은 결과로 1.00을 달수있음
git tag 1.0.0

새로만든 가지 원격 저장소로 전송하기전까지 다른 사람들이 접근할수 없음
git push origin 가지이름

변경내용을 변경 전 상태로 되돌려줌 이미 인덱스에 추가된 변경 내용과 새로 생성한 파일은 그대로 남음
git checkout 파일이름

로컬에 있는 모든 변경 내용과 확정본을 포기
git fetch origin
git reset —hard origin/master


브런치 삭제

git branch -d 이름




git pull 변경내용이 로컬 작업 디렉토리에 받아지고 병합 fetch & merge
다른 가지에 잇는 변경내용을 현재 가지에 병합하려면
git merge 가지이름






git init
읽어와서 32비트인즈64비트인



Subversion과 Subversion 비슷한 놈들과 Git의 가장 큰 차이점은 데이터를 다루는 방법에 있다.
큰 틀에서 봤을 때 VCS 시스템 대부분은 관리하는 정보가 파일들의 목록이다.
CVS, Subversion, Perforce, Bazaar 등의 시스템은 각 파일의 변화를 시간순으로 관리하면서 파일들의 집합을 관리한다.


Git은 데이터를 파일 시스템 스냅샷으로 취급!하고 크기가 아주 작다
파일이 존재하는 그 순간을 중요하게 여김
파일이 달라지지 않앗으면 이전상태의 파일에 대한 링크만 저장


오픈소스라서 보완해주는걸로 돈받기 많이 쓰이니까

ssh 프로토콜

GUI git hub
CLI Command line interface 손코딩????????

git github
인터페이스가 다름


git config --global user.name "name" 최초 한번은 사용자이름을 지정해줘야 한다
git config --global user.email "user@email.com" 최초 한번은 사용자 이메일을 지정해줘야 한다
git config --global alias.co checkout co 라는 별명(단축글자)으로 checkout 을 사용한다 git config --global core.editor emacs git 편집기로 emacs 를 사용한다
git config --golbal merge.tool vimdiff 머지툴로 vimdiff 를 사용한다발ㅅ
git config --list 글로벌 설정을 확인한다
git clone url 원격저장소 로컬에 복사
git init 원격관리 시작(로컬저장소를 만든다)
git add filename 파일 추적하기(staging area 에 추가한다)
git commit -m 'commit message' 커밋하고 메시지 입력(작업내용을 저장소로 보낸다)
git pull 원격저장소에서 다운로드하면서 합치기
git push 원격저장소로 업로드
git status 현재 상태 알아보기

출처: http://demun.tistory.com/2433 [demun(대문블로그)]
그레이스?

#Git bash
git 최초 설정
```git
git config --global user.name "JJune"
git config --global user.email idwn1203@gmail.comm
```

git remote
git remote rename a b
git remote rm
git remote -v

리모트 저장소를 Pull하거나 Fetch하기
git fetch [remote-name]


Error
returned error: 403
원인
권한이 없어서 push가 안됨
시도(색깔 별로 실패와 성공으로 나누기)
1. git init 부터 다시
  - ssh 로 리모트 시도
    - git remote rm origin명령어로 삭제
    - git remote -v 로 확인
2. git user name 변경
  - 폴더와 repository 이름 동기화
3. git repository 자체를 다시 만듬
4. ssh 주소를 받아옴
  (기존에 있던거 지우고)
  - ssh-keygen 입력
    - Overwrite(y/n) 을 y로
    - 암호입력
cat ~/.ssh/id_rsa.pub
공개키를 setting 에서 만들어서 Ready Only아닌 Overwirte로 해주기




#Egit
Egit 삭제는 쉽네 그냥 delete ....
서버 상에서 삭제는 settings에서 delete


git push,clone 에서의 permission denied Error

ssh-keygen -t rsa -C "git이메일"
Press Enter
Copy the Public key
/User/~~/id.rsa.pub 복사
cat /User/~~/id.rsa.pub
ssh-rsa 로 시작하고 이메일로 끝나는 부분 복사해서 github에 복사


cat ~/.ssh/id_rsa.pub

Error git add readme.md returns "fetal:path spec'readme.md didnot match anyfiles"
- 새로만들기

#  Permission Error
## window

## Linux
없으면 ssh-keygen으로 생성
passphrase
- 비번 입력

.ssh/id_rsa

cat ~/.ssh/id_rsa.pub

만들어서 키입력하면 완료됨


폴더 만드는 걸로는 commit이 안되고 내용 수정해야 commit 이 됨


ssh_key 하나당 한 계정만 연동 가능


# 다중계정 생성 방법


git pull 로 땡겨오는데 local 에서 commit 바뀌면 git stash save 파일이름
하고 다시 pull 하면 됨
git clone 하고 브런치 따면 바뀜

게임개발 이외ㅐㅏ

game 서버 플랫폼


#cmd

윈도우 명렁어만 cmd

# gitbash

LInux 명령어도됨



#git hub  
- hub역할ㅏㅐㅏ


페어프로그램
- 한컴터로 같이 코딩하는 것

코드 난독화
- 보안
- java script


working directory stage git directory
- stage area 에 장바구니 담듯이
commit 이 결제

Local Remote

fork
- 소스 찍어서 가져오기
- 개인적으로 사용..? 바꾼내용이 원래주인한테 가나..?
- 주인이 누가 가져갔는지 알 수 있음




branch rule
- master 는 merge용
- 개발은 branch 에서하고 merge


#git init


client
- just tool
server
-


cd c..? directory

Read me 대문자 이유



와일드
- 특수문자를 사용해서 다수의 파일 설정하게하는 명령어

ㅡ git add *

git add 취소 하고 싶을때
git rm --cached hello.txt
git reset readme.md


셸 스크립트(shell script)는 셸이나 명령 줄 인터프리터에서 돌아가도록 작성되었거나 한 운영 체제를 위해 쓰인 스크립트이다. 단순한 도메인 고유 언어로 여기기도 한다. 셸 스크립트가 수행하는 일반 기능으로는 파일 이용, 프로그램 실행, 문자열 출력 등이 있다.

셸 스크립트라는 말은 유닉스 셸을 위해 쓰인 스크립트를 말하는 반면, COMMAND.COM(도스)과 cmd.exe (윈도) 명령 줄 스크립트는 보통 배치 파일이라고 불리지만 이 글에는 두 개의 속성 모두를 논한다.

.sh라는 파일 확장자를 가진 파일이 특정 종류의 셸 스크립트를 가리키는 것이 보통이지만, 대부분의 셸 스크립트는 파일 확장자를 지니지 않는다.[1][2]




편집기에서 commit 하는 방법
- git commit



제목 뽑아서 편하게 정리해주는 프로그램 있음


git diff


git log
- commit 명령만 확인할 수 있음

.gitignore 사용하여 git 관리대상에서 제외하기


rm 으로 지운거만 됨


git checkout 파일명
- 커밋안하면 동작이 안되나

git

git rm 으로 지우거나 날라갔으면
- 안됨 - git 저장소에서 지운것


git memory

svn 다 저장하기때문에 무거움
git 일부 필요한파일 코어만가지고있어야
- jpg 도 전부 jpeg?는 일부 정보만 가지고 있는것



merge 시점
- 어느정도 작업이 됬을때


pull 할때 같은 계정인데 다른 컴퓨터일 경우
- loal이 따로 존재


합칠때 내용이 다르면 자동으로 추가..?


https
- url로 다운
ssh
- id password필요 없이 통신하겠다는 규약 정해놓은 것

origin 원격지를 얘기함

git remote -v
여기랑 연동된다는 걸 알수 있음

pr
- pull request



# Q
왜 윈도우에서는 되는거지?
- 애초에 http로 할껄 ssh로 하면 다중계정생성해야함

Linux 에서 Commit 하고 지우면 서버에는 올라가지 않을꺼고 그냥사라짐?
-> 그런가봄 ㅇㅇ
ssh
- 공개키방식
Windwo는 처음 한게만 하면 나머지는되는거?
ssh와상관없이 http로하면 그냥되는거?

컴터 user이름과 노트북 user이름 다를 경우

config 작성법

git 동시에 master브랜치로
- error

# error
노트북에서 push 중에 절전모드 가면 push반영안됨

pull개념?
- 딴 컴터에서 푸쉬하면 언제 동기화가 되는거지?
