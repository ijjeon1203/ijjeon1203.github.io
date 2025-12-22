* 그 전에 원격 저장소와 로컬 저장소의 폴더 구성이 다르다면, 즉 갱신 

  상태가 다르다면 먼저 pull, 그러니까 둘의 상태를 같게 해줘야 한다.

- 'git pull'로 하면 된다!



* error: failed to push some refs to 'https://github.com/pj6563/Online-Glasses.git'

hint: Updates were rejected because the tip of your current branch is behind

hint: its remote counterpart. Integrate the remote changes (e.g.

hint: 'git pull ...') before pushing again.

hint: See the 'Note about fast-forwards' in 'git push --help' for details.


혹시 push할 때  다음과 같은 오류가 났다면 아마 위에서 말한 원격 저장소와 로컬 저장소의 상태가 달라서 나는 오류일 것이다.
그러니 pull을 먼저 해주어 둘의 상태를 같게 한 다음 push를 해준다

그리고 'git status'를 통해서 현재 git의 상태를 알 수 있으니 오류 해결에 적극 이용
하기 바란다!