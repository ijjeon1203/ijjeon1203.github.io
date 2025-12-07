
# 기능
- 되돌리고 싶은 시점의 commit이력으로 돌아가는 것(시간여행)
- 메인을 이전 커밋으로 다시 되돌릴 수 있습니다. 기록이 실수로 변경된 경우를 대비한 안전망을 제공합니다.
  


git reset을 진행했을 때 ORIG_HEAD라는 파일이 생성
- reset 하기 전 커밋의 해시값을 따로 저장
- git reset --hard ORIG_HEAD를 통해서 reset을 복구 가능
- 직접 기존 커밋의 해시값으로 reset을 해도 마찬가지로 동작

# 종류

- hard
	- hard 옵션을 사용하면 돌아간 커밋 이후의 변경 이력은 모두 삭제


```
git reset HEAD^
```

- commit을 바로 이전 상황으로 돌림

 --mixed
	- 변경 이력은 모두 삭제하지만 변경 내용은 남아있습니다.

--soft
- 변경 이력은 모두 삭제하지만 변경 내용은 남아있습니다. 그러나 stage 되어있습니다.



# git reset --soft HEAD@{1}

- amend 취소되고 amend 된건 unstage 에 생김

git reset이 실행되면, 현재 HEAD가 가르키고 있는 브랜치의 커밋 해시값이 reset 위치의 커밋의 해시값으로 수정된다.


# 의문,사용기
reset 하고 복원 가능?
- 가능

  

- git은 reset을 하는 그 시점에 objects의 파일을 삭제하지 않음

  

- 가비지 컬렉션의 방식으로 데이터가 많아졌을 때, 참조값이 없는 것의 삭제를 진행