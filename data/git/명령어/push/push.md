

git push 취소

reset: 되돌리고 싶은 시점의 commit이력으로 돌아가는 것(시간여행)
revert: 현재까지 남긴 이력들을 유지한 채 되돌리고 싶은 commit을 원상복귀시키는 것(복구commit이 추가됨)

혼자 사용하는 원격 저장소 - reset을 사용

누군가와 공유를 하고 있다면, 다른 사람이 그 사이에 pull을 받았을 수도 있기 때문에 그러면 내가 되돌리기를 했을 때 문제가 생일 수 있으므로, reset 하기 전에 충분한 커뮤니케이션이 필요하다고 합니다. -  revert를 많이 사용한다고 합니다.

1. commit 이력 조회하기

git log --oneline

HEAD가 있는 곳이 현재 브랜치(마스터)를 가리키는 포인터입니다.

그리고 이 브랜치는 가장 최근의 commit을 가리킵니다.

1. 돌아가고 싶은 commit 이후의 commit 삭제하기

여기에서 돌아가고 싶은 commit을 찾아서 git reset를 실행합니다.

reset hard를 쓰면 돌아가려는 이력 이후의 모든 내용은 지워버리겠다는 것입니다.

과거 이력만 지우고 이후에 무대에 올려놓은 것으로 바로 commit 하고 싶다면, reset soft를 쓰면 됩니다.

git reset --hard "해당commit"

그러면
좀 전의 commit이 사라지고 되돌리고 싶은 commit으로 돌아왔습니다.
이제 이 commit에는 그 당시 제가 무대에 올라온 파일들을 묶어서 제 로컬에 저장해 놓은 '기억'이 있습니다.

1. github 원래대로 돌려놓기

따라서 아래 명령어로 push를 해주면,

git push -f origin master

status a
push b
status b

b에다 내용 추가

- b'
- a로 이동하고 다시 커밋 후 push
- 이경우 a상태면 b로 push한 내용 사라지는지?

이 파일 저장전에 어떤건지 몰라서..