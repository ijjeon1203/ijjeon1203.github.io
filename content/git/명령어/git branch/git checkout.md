git branch생성

git checkout -b test

git push origin test
이렇게되면 local과 저장소의 remote branch가 생성됩니다.
생성된 branch는 각자가 local 및 저장소 기준이므로, local의 branch를 retmoe branch와 연동하는 작업을 수행하는 것이 좋습니다.
branch 연동은 다음을 통해 수행합니


git branch --set-upstream-to origin/feature-01

branch 삭제하기
작업이 끝나고, 기준 branch로 pull request가 종료되어서 merge까지 완료 되었다면, 해당 branch를 삭제 해줍니다.
merge 작업이 끝난 local의 feature-01 branch를 삭제하기 위해서는, 다른 branch로 checkout 후, feature-01 branch를 삭제해 주어야 합니다.
여기서는 develop branch로 이동해서 feature-01 branch를 삭제해 보겠습니다.

git checkout develop
git branch --delete feature-01
그러나, 작업된 사항이나 commit 한 이력이 남아있는 경우, 해당 command로 branch가 삭제되지 않는 경우가 있습니다.
이러한 경우에는 강제로 branch를 삭제할 수 있습니다.

git branch -D feature-01
-D(대문자) option을 통해서 local branch를 강제로 삭제할 수 있습니다.

이 경우, local의 branch는 삭제 되었으나, remote branch는 삭제가 아직 되지 않았습니다. remote branch를 삭제하기 위해서는, 다음과 같은 command를 수행합니다.

git push origin :feature-01
해당 command를 통해서 원격 remote branch를 삭제할 수 있습니다.





git checkout branch

git checkout 이름^

git checkout 이름~n    n은커밋개수

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




git pull한뒤에 프로젝트를 새로 로드해서 새로운 파일을 추가해야함
- 파일하나만 새로 추가
- 전체 다 refresh 하고 추가 (시도 안해봄)

git checkout master ~1

- 1단계 전 커밋 해당하는 숫자만큼 과거로

특 정 커밋 돌아가기
git checkout 고유번호

git merge B
B를 현재 브랜치로 병합 한다


git log -- branches --graph --decorate -- oneline





