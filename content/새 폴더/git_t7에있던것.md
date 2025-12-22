# git

git
abort
0107 merge 에러 발생

- abort 시킴

discard

- 삭제하는 것?
- 소스 코드에서 변경된 부분만을 버리고, 변경 되기 전 상태의 소스로 되돌리는 것
- commit 하기 전에 unstaged 소스가 존재한 상태에서 commit 했다면 Uncommitted Changed가 바로 존재하게 되는데 해당 소스를 살펴보고 변경된 부분이 필요가 없다면 discard해서 원래 상태로 간편히 돌리기 위해 사용

Remove : 소스 파일 제차 삭제하는것

amend의 옵션
-스테이징에 추가된 내용을 반영해주는 동시에 커밋 메시지도 변경해줍니다. 따라서 변경할 내용이 없을 때도 커밋메시지를 변경하고 싶을 때 자주 사용합니다.

git pull 이후 build 시간 오래 걸리네

amend

- 가장 최근 commit 수정

cherry pick\하나만 가져옴

rebase base 기준 여러개

git fork

git flow
stash : 임시저장
discharge .- > 삭제

브런치 종류
master  고객사에 나가있는 형상
develop - feater

- 개발용 브런치
- 여러명이 사용가능
- 내용이 다르면 충돌 발생

hotfix

- 패치 낼때...?

release

폴더 추가는 반영안됨
파일 추가는 반영됨

finish 하면 자동 merge

gitlab vs git

대략 말한것과 실제 있는것

- 수정 필요
수정 요구
pgyvlcx'g nts'rx

# git branch

1. Master Branch
제품으로 출시될 수 있는 브랜치
배포(Release) 이력을 관리하기 위해 사용. 즉, 배포 가능한 상태만을 관리
2. Develop Branch
다음 출시 버전을 개발하는 브랜치
기능 개발을 위한 브랜치들을 병합하기 위해 사용. 즉, 모든 기능이 추가되고 버그가 수정되어 배포 가능한 안정적인 상태라면 develop 브랜치를 ‘master’ 브랜치에 병합(merge)한다.
평소에는 이 브랜치를 기반으로 개발을 진행한다.
3. Feature branch
기능을 개발하는 브랜치
feature 브랜치는 새로운 기능 개발 및 버그 수정이 필요할 때마다 ‘develop’ 브랜치로부터 분기한다. feature 브랜치에서의 작업은 기본적으로 공유할 필요가 없기 때문에, 자신의 로컬 저장소에서 관리한다.
개발이 완료되면 ‘develop’ 브랜치로 병합(merge)하여 다른 사람들과 공유한다.

‘develop’ 브랜치에서 새로운 기능에 대한 feature 브랜치를 분기한다.
새로운 기능에 대한 작업 수행한다.
작업이 끝나면 ‘develop’ 브랜치로 병합(merge)한다.
더 이상 필요하지 않은 feature 브랜치는 삭제한다.
새로운 기능에 대한 ‘feature’ 브랜치를 중앙 원격 저장소에 올린다.(push)
feature 브랜치 이름 정하기
master, develop, release-(RB_), or hotfix- 제외

- -no-ff 옵션
새로운 커밋 객체를 만들어 ‘develop’ 브랜치에 merge 한다.
이것은 ‘feature’ 브랜치에 존재하는 커밋 이력을 모두 합쳐서 하나의 새로운 커밋 객체를 만들어 ‘develop’ 브랜치로 병합(merge)하는 것이다.
1. Release Branch
이번 출시 버전을 준비하는 브랜치
배포를 위한 전용 브랜치를 사용함으로써 한 팀이 해당 배포를 준비하는 동안 다른 팀은 다음 배포를 위한 기능 개발을 계속할 수 있다. 즉, 딱딱 끊어지는 개발 단계를 정의하기에 아주 좋다.
예를 들어, ‘이번 주에 버전 1.3 배포를 목표로 한다!’라고 팀 구성원들과 쉽게 소통하고 합의할 수 있다는 말이다.

‘develop’ 브랜치에서 배포할 수 있는 수준의 기능이 모이면 또는 정해진 배포 일정이 되면, release 브랜치를 분기한다.
release 브랜치를 만드는 순간부터 배포 사이클이 시작된다.
release 브랜치에서는 배포를 위한 최종적인 버그 수정, 문서 추가 등 릴리스와 직접적으로 관련된 작업을 수행한다.
직접적으로 관련된 작업들을 제외하고는 release 브랜치에 새로운 기능을 추가로 병합(merge)하지 않는다.
‘release’ 브랜치에서 배포 가능한 상태가 되면(배포 준비가 완료되면),
배포 가능한 상태: 새로운 기능을 포함한 상태로 모든 기능이 정상적으로 동작 하는 상태
‘master’ 브랜치에 병합한다. (이때, 병합한 커밋에 Release 버전 태그를 부여!)
배포를 준비하는 동안 release 브랜치가 변경되었을 수 있으므로 배포 완료 후 ‘develop’ 브랜치에도 병합한다.
이때, 다음 번 배포(Release)를 위한 개발 작업은 ‘develop’ 브랜치에서 계속 진행해 나간다.

release 브랜치 이름 정하기
release-RB_* 또는 release-* 또는 release/* 처럼 이름 짓는 것이 일반적인 관례
[release-* ] 형식을 추천 EX) release-1.2

release 브랜치 생성 및 종료 과정
// release 브랜치(release-1.2)를 'develop' 브랜치('master' 브랜치에서 따는 것이 아니다!)에서 분기
$ git checkout -b release-1.2 develop

/* ~ 배포 사이클이 시작 ~ */

/* release 브랜치에서 배포 가능한 상태가 되면 */
// 'master' 브랜치로 이동한다.
$ git checkout master
// 'master' 브랜치에 release-1.2 브랜치 내용을 병합(merge)한다.

# -no-ff 옵션: 위의 추가 설명 참고
{
$ git merge --no-ff release-1.2
// 병합한 커밋에 Release 버전 태그를 부여한다.
$ git tag -a 1.2

/* 'release' 브랜치의 변경 사항을 'develop' 브랜치에도 적용 */
// 'develop' 브랜치로 이동한다.

$ git checkout develop
 
// 'develop' 브랜치에 release-1.2 브랜치 내용을 병합(merge)한다.

$ git merge --no-ff release-1.2 // -d 옵션: release-1.2에 해당하는 브랜치를 삭제한다.

$ git branch -d release-1.2


## Hotfix Branch
출시 버전에서 발생한 버그를 수정 하는 브랜치
배포한 버전에 긴급하게 수정을 해야 할 필요가 있을 경우, ‘master’ 브랜치에서 분기하는 브랜치이다. ‘develop’ 브랜치에서 문제가 되는 부분을 수정하여 배포 가능한 버전을 만들기에는 시간도 많이 소요되고 안정성을 보장하기도 어려우므로 바로 배포가 가능한 ‘master’ 브랜치에서 직접 브랜치를 만들어 필요한 부분만을 수정한 후 다시 ‘master’브랜치에 병합하여 이를 배포해야 하는 것이다.

배포한 버전에 긴급하게 수정을 해야 할 필요가 있을 경우,
‘master’ 브랜치에서 hotfix 브랜치를 분기한다. (‘hotfix’ 브랜치만 master에서 바로 딸 수 있다.)
문제가 되는 부분만을 빠르게 수정한다.
다시 ‘master’ 브랜치에 병합(merge)하여 이를 안정적으로 다시 배포한다.
새로운 버전 이름으로 태그를 매긴다.
hotfix 브랜치에서의 변경 사항은 ‘develop’ 브랜치에도 병합(merge)한다.

버그 수정만을 위한 ‘hotfix’ 브랜치를 따로 만들었기 때문에, 다음 배포를 위해 개발하던 작업 내용에 전혀 영향을 주지 않는다. ‘hotfix’ 브랜치는 master 브랜치를 부모로 하는 임시 브랜치라고 생각하면 된다.

hotfix 브랜치 이름 정하기
[hotfix-* ] 형식을 추천 
- EX hotfix-1.2.1

hotfix 브랜치 생성 및 종료 과정
}


# git fork

# 사용하기

# 종류 두개

bad case
위반한것
good case
위바ㅎㄴㅏ지 않는것

내부 bad case good case
바깥 bad case good case

테스트 경로

C:\Work\static\AnalysisAgent\tool\Test\Resource\Testcase


규칙 관련 모든걸 다 패치

위배 발생하지 않는다 == 다른 template을 사용해야함 or 규칙 지원하지 않는다

# 테스트 방법

git fork 해서 연결하기

- develop에서 연결해놓음

코드 수정은 notepad++를 사용

agent .sln 실행
슈어 계정 로그인?

- 아마 gitfork 접속할때?

sc.cpp ACCEption

- 일단 적고 다시 해보면서

함수 단위로 테스트

- 경로 확인하기
- 이 경로를 나중에 사용

하나씩 run
append로 하나씩 추가하고 한번에 run

- 엔진에 대해 확인하는것

notepad 작성시 여백 공백 확인하기

## 테스트 코드 만들기

## 테스트 코드 업데이트 하기

cmake vs 경로로 예측함

gui 팝업

name 룰이름
rulseset 분류한거
title  제목
description  설명

심각도에 관한정보

- 어딜까

visual studio
내부적으로 test case 하면 몇 번째 에러인지
report할 땢
수정x 확인까지만 가능
엔진에 대해서 확인하는것

# 테스트 종류가 많음

스테이시 필드






# 배울 링크

[https://gbsb.tistory.com/10](https://gbsb.tistory.com/10)
[https://git-scm.com/book/en/v2](https://git-scm.com/book/en/v2)
git 명령어 다 나와 있음

[git 명령어](git%20fd18b306db7342cdb8bbebaab571eeca/git%20%E1%84%86%E1%85%A7%E1%86%BC%E1%84%85%E1%85%A7%E1%86%BC%E1%84%8B%E1%85%A5%20daaebcc4bd794fc8a9b4372467ef7f0a.md)

# git

- branch 새로 만들기
- fork에서 알아서 추가

git

- Amend

discard 했는데 ctrl z로 살아나려나

push 기준

- 한번에 push 할 것
- description 수정해서 한번에
- testcase 수정해서 한번에

# push

템플릿 추가 안한경우

# interactive rebase

1. 전체 stash
2. 순서바꾸기
3. git push <remotename> <commit SHA>:<remotebranchname>
ex) git push origin 2e979c655df6a04ea159fa112f4d57afbd09b599:feature/KISA_C

commit 위치 옮길 때, 1->2->3 을 3->1->2 로 바꾼다고 했을 때
3번에서 수정한 파일이 1번 2번에서도 수정이 됐으면, conflict 가 2번 발생할 겁니다..
방금 건은 매우 운이 좋은 경우입니다. 옮기는 가운데 conflict 이 없어서 다행이네요
쉽게 말해서 commit 간 수정한 파일이 안 겹쳐야 쓰기 좋다는 정도로 이해





# 사용기

지웟고 저장 다시 살리고 저장 → 같은 걸로 인식하는 듯 