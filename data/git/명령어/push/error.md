git 에러 


원격 저장소를 remote로 설정하고 바로 push를 하면 몇가지 오류가 발생할 수도 있다.

예를 들어 아래와 같은 오류 메시지이다.

1
2
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/huusz/test.git'

rejected : push가 거부되었다.

master -> master : 로컬 저장소의 master 브랜치의 변경 사항을 원격 저장소의 master 브랜치에 반영하려 했는데

non-fast-forward : 원격 저장소의 master 브랜치가 로컬 저장소의 버전보다 이전 버전이 아니다. 라는 의미이다.



즉, 오류가 발생한 원인은 github에서 새로운 프로젝트를 생성하면서 만들어진 원격 저장소의 readme.md

파일때문 일 것이다. 더 정확히 말하면 readme.md 파일의 존재가 문제가 되는 것이 아니고, 원격 저장소에서

이루어진 readme.md를 추가하는 커밋이 로컬 저장소의 커밋 로그에는 없기 때문이다.



push 명령은 로컬 저장소의 commit 목록과 원격 저장소의 commit 목록을 비교한다.

그런 다음 원격 저장소의 마지막 commit id와 동일한 commit id를 가진 로컬 저장소의 commit 시점을

찾아낸 뒤, 원격 저장소의 마지막 커밋과 연결한다.

원격 저장소의 첫번째 commit이자 마지막 commit인 readme를 추가하는 commit이 원격 저장소에는

존재하지 않고, 따라서 현 상태에서는 둘을 연결할 수 없다.



이 상황을 해결하는 방법에는

원격 저장소를 삭제하고 다시 만든다. (readme.md 파일을 없애고 다시 저장소를 만든다.)
fetch나 pull 명령어로 원격 저장소의 마지막 commit을 로컬 저장소의 commit로그의 맨 앞으로 받아온다.


두번째 방법으로 해결해본다.



하지만 pull 명령어를 실행하면 아래와 같은 오류가 발생한다.

>> git pull origin master

-- fatal: refusing to merge unrelated histories



에러 내용은 원격 저장소의 master 브랜치에서 로컬 저장소의 FETCH_HEAD를 merge하는 것이 거부되었다.

commit 히스토리가 서로 관련이 없다는 뜻이다. 즉, 서로 관련성이 없기 때문에 merge할 수 없다는 것이다.



pull 명령어는 fetch + merge 작업을 한번에 처리하는 명령어이다. 현 상황은 fetch는 되었지만, merge가

되지 않은 상태이다.

기본적으로 merge는 원격 저장소와 로컬 저장소가 공통으로 가지고 있는 commit지점이 존재해야 한다.

그 지점부터 병합을 시도하기 때문이다. 애초에 공통되는 commit이 없기때문에 pull 명령어를 사용할 수

없는 것이다.



해결하기 앞서 상황을 이해하기 위해 pull과 fetch의 개념을 살펴보자.

fetch는 원격 저장소에 있는 내용을 가져오지만 자동으로 내 로컬 저장소에 merge하지 않는다.

원격 저장소의 내용을 확인만 하고 로컬에 merge하고 싶지 않을 때는 fetch를 사용한다.



HEAD에는 가장 마지막에 행해진 commit정보가 담긴다. 마찬가지로 FETCH_HEAD는 원격 저장소의

가장 최신 commit 이력이 담기게 된다.

FETCH_HEAD는 이름 없는 브랜치로 로컬에 가져오게 된다. 이 브랜치는 FETCH_HEAD로 checkout도

가능하다.



pull 명령어는 원격 저장소에 있는 내용을 가져올 뿐만 아니라, 자동으로 로컬 저장소에 merge한다.

즉, git pull 명령어는 git fetch + merge FETCH_HEAD인 셈이다.



복잡하고 긴 설명 끝에 결론은 어쨌든 연결되는 공통된 커밋 포인트가 없다는 것이다.

이 상황을 해결하기 위한 방법에도 2가지 방법이 존재하는데,

git clone 명령어를 통해 원격 저장소를 복제해온다.

pull 명령어에 옵션을 추가해 강제로 pull 한다.



두번째 방법을 택해 pull 명령어에 옵션을 줘서 가져오면 간단하게 해결된다.

git pull origin (branchname) --allow-unrelated-histories