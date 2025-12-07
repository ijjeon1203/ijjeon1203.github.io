git ignore

네, `.gitignore`는 Git에서 버전 관리에서 제외할 파일이나 디렉터리를 지정하는 데 사용되는 파일이에요. 예를 들어, 빌드 결과물, 임시 파일, 설정 파일 등을 Git에 올리고 싶지 않을 때 `.gitignore` 파일을 설정하여 제외할 수 있어요.

`.gitignore` 파일은 보통 프로젝트 루트 디렉터리에 위치하며, 여기에 제외할 파일이나 디렉터리의 패턴을 적어두면 됩니다. 예를 들어:

- `.log` : `.log` 확장자를 가진 모든 파일을 무시
- `node_modules/` : `node_modules` 폴더를 무시
- `.env` : `.env` 파일을 무시

혹시 `.gitignore` 설정에 대해 더 궁금한 점 있으면 알려줘요!

Git에서 `.gitignore`에 의해 무시된 항목을 확인하는 방법은 몇 가지가 있어요. 가장 흔히 사용하는 방법은 `git status` 명령어와 `git check-ignore` 명령어입니다.

### 1. `git status` 명령어

`git status`는 현재 Git 상태를 확인할 때 사용되며, 무시된 파일들도 `git status`에서 확인할 수 있어요. 무시된 파일들은 기본적으로 "untracked files" 목록에 표시되지 않지만, `git status --ignored` 명령어를 사용하면 무시된 파일들을 포함한 모든 파일 목록을 볼 수 있습니다.

```bash
git status --ignored

```

이 명령어를 실행하면 `.gitignore`에 의해 무시된 파일들도 볼 수 있어요.

### 2. `git check-ignore` 명령어

특정 파일이나 디렉터리가 `.gitignore`에 의해 무시되는지 확인하려면 `git check-ignore` 명령어를 사용할 수 있습니다.

```bash
git check-ignore -v <파일_경로>

```

`<파일_경로>` 부분에 확인하고 싶은 파일을 넣으면, 그 파일이 무시되는지 여부를 알려줍니다. 예를 들어, `node_modules/`가 `.gitignore`에 의해 무시되는지 확인하고 싶다면:

```bash
git check-ignore -v node_modules/

```

이렇게 하면 해당 파일이나 디렉터리가 `.gitignore`에 의해 무시되는 이유와 경로를 알 수 있어요.

이 방법들로 무시된 항목을 쉽게 확인할 수 있어요!