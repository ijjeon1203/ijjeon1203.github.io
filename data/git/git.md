git checkout branch

git checkout 이름^

git checkout 이름~n    n은커밋개수

브런치 강제로 옮기기


git branch name

git revert
 - 이미 push한경우에는 이걸해야함
git reset


c87e1945b5fc0e48c2b84f2c382d85d21fe62883


git conflict문제해결하기위해
git status 치고
작업한뒤 add
그후 작업이어하기
ex) git convert --continue

이전커밋상태로 돌아가기

commit 이후에 작업해서 사라지면 브랜치를 새로만들어서 푸쉬한다음에
Checkout해서 돌아가기

Q)
Commit하고 작업내용 바꼇을때 다시 Commit한 상태로 돌리기?



Git Clone 할때


clone하면 Repository 이름의 폴더안에 생김





브랜치가 여러개 있을 경우
 - 마스터만 클론되고 브런치는 클론이 안됨
	- Master 하나만 Clone
	- 특정 브랜치 Clone
 - git push --force 로 github에 강제로 덮어씌워버리기
	- branch간의 관계 깨짐

git clone 중에 ctrl + c 로 강제 종료해버리면




git checkout HEAD~1
일단 이렇게 하면 working directory 와 staging area를 모두 1단계 전 커밋으로 돌려 준다.
사실 브랜치 변경 용도로만 사용했던 명령어였고, 복원 명령어 리스트에도 있는 걸 봤지만
딱히 활용도를 알기 힘들었었다.
그런데 이렇게 쓰이는구나..
당연하겠지만 HEAD~ 뒤의 숫자는 몇단계로 돌아갈지의 개수다.
git checkout HEAD~10
10단계 전 커밋으로 돌아간다.
다시 돌아오는 방법은
git checkout master
마스터 브랜치로 돌아오는 명령인데, 마스터 브랜치가 아닌 다른 브랜치명을 적어도 상관없댄다.
해당 브랜치로 복귀하게 된다. 신비롭다.

git 생성 --> commit

서버에 올린 게 아님


find . -name  '.git' git 들어간 내용찾기


git 저장소 삭제

클론해서 새로 만들기

git은 만들어짐 새 저장소에 등록?

git config --list
git config

git log
git status


https://github.com/anroniogi/opros_knu.git

master 와 develop가 url 똑같은데 master에서 commit 해버리기
클론 도중에 취소한다면?
develop삭제한 담에 다시시도


git branch develop



이름이 바뀐다면?


새로운 git 추가 새로운  git repository



	로컬 	서버
	ㅇ       ㅇ

1) 서버에서 clone 해온다음에 그 하위 에다가 집어 넣기 경로가 바뀜
2) 로컬에서 시작해서 새로운 repository 만들기
3) 로컬에 있는 걸 서버의 마스터에 올릴 수가 있나?


용량이 너무 커서 느림;;;
