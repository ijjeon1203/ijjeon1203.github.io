

revert는 reset과 다르게 커밋을 삭제하는 것이 아닌 커밋을 추가합니다.

그러나 이전 커밋과 정반대의 데이터를 추가하는 방식으로 코드를 되돌립니다.

revert 명령어는 `reset --soft`, `mixed`와 동일한 결과를 가져오지만 이력은 `Revert "..."`라는 메세지가 추가됩니다.

```
git commit -m "1번 커밋"
git commit -m "2번 커밋"
git commit -m "3번 커밋"

git revert [1번commit hash]
```

위처럼 명령어를 실행하면 `1번 커밋` 이후의 커밋들이 삭제되는 것이 아니라, **`1번 커밋`에 해당하는 내용만 삭제**됩니다. 그리고 `Revert "1번 커밋"`이라는 커밋에는 1번 커밋이 삭제된 이력이 남게 되죠.

`git log`에는 아래와 같이 찍힙니다.

```
Revert "1번 커밋"
3번 커밋
2번 커밋
1번 커밋
```

### [#](https://kyounghwan01.github.io/etc/git/git-reset-revert/#%EB%B0%94%EB%A1%9C-%EC%BB%A4%EB%B0%8B%EB%90%98%EA%B2%8C-%ED%95%98%EC%A7%80-%EC%95%8A%EC%9C%BC%EB%A0%A4%EB%A9%B4)바로 커밋되게 하지 않으려면?

만약 revert한 결과를 stage 상태만 유지하고, commit 하지 않으려면 `--no-commit` 옵션을 추가합니다.

```
git revert --no-commit [커밋 해쉬]

// 이후
git commit -m "어떤 커밋을 왜 리버트했니?"

git push
```

### [#](https://kyounghwan01.github.io/etc/git/git-reset-revert/#%EC%97%AC%EB%9F%AC%EA%B0%9C-%EC%BB%A4%EB%B0%8B%EC%9D%84-%EB%90%98%EB%8F%8C%EB%A6%AC%EB%A0%A4%EB%A9%B4)여러개 커밋을 되돌리려면?

```
git revert [커밋해쉬]..[커밋해쉬]
```

git log에는

```
git revert [1번커밋해쉬]..[2번커밋해쉬]
git log

Revert "2번커밋해쉬"
Revert "1번커밋해쉬"
```

revert는 되돌리는 커밋이 중간에 있을때 커밋 해쉬를 넣어서 중간 커밋만 삭제할 수 있고, 어떤 커밋이 왜 revert 됬는지 commit message를 통해 관찰 가능함으로 더욱 유용합니다.

또는 revert는 커밋은 삭제되는 것보다 이전으로 되돌리는 이력마저 남기는 것이 history 유지 차원에서 더 좋습니다.

그래서 `revert` 씁시다!
# revert

- 현재까지 남긴 이력들을 유지한 채 되돌리고 싶은 commit을 원상복귀시키는 것(복구commit이 추가됨)

cherry pick 한것 git finish 하면 이상한가 merge나 rebase 했어야하나?

- 고 하나만 수정할거라서...

master 이전에 땀
- hotfix 에 내용 추가하고 싶을때는... rebase가 맞았던듯

git은 같은 파일인거 어떻게 아는거지?
- 철자비교?

git config --add gitflow.multi-hotfix true
- unstage로 갔음 force push해서 추가해버림

