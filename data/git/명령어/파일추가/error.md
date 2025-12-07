27

Git에서 `git add`와 `git commit` 명령이 오래 걸리는 경우, 원인은 다양할 수 있습니다. 주로 다음과 같은 이유와 해결 방법이 있습니다:

---

## 1. **추적 중인 파일의 크기가 크거나 개수가 많음**

### 원인

- 프로젝트 디렉토리에 큰 파일(예: 로그 파일, 빌드 산출물, 이미지 등)이 포함되어 있거나 너무 많은 파일이 추가되었을 경우, Git이 변경 내용을 추적하는 데 시간이 오래 걸립니다.

### 해결 방법

1. **`.gitignore` 설정**
    
    추적이 필요 없는 파일(예: `node_modules`, `*.log`, 빌드 파일 등)을 `.gitignore`에 추가합니다.
    
    ```bash
    echo "node_modules/" >> .gitignore
    echo "*.log" >> .gitignore
    echo "build/" >> .gitignore
    
    ```
    
    그런 다음 `.gitignore`를 적용:
    
    ```bash
    git rm -r --cached .
    git add .
    git commit -m "Apply .gitignore"
    
    ```
    
2. **크거나 불필요한 파일 제거**
    
    저장소에 이미 커밋된 큰 파일을 제거하려면 다음 명령어를 사용합니다:
    
    ```bash
    git filter-repo --path path/to/large-file --invert-paths
    
    ```
    
    **참고**: `git filter-repo` 사용 전 데이터를 백업하세요.
    

---

## 2. **파일 시스템 I/O 병목 현상**

### 원인

- Git이 변경 사항을 스캔할 때, 디스크 속도가 느리거나, SSD가 아닌 HDD를 사용하는 경우 시간이 오래 걸릴 수 있습니다.

### 해결 방법

- **빠른 스캔 옵션 사용**:`git add`에 `u` 또는 `A` 플래그를 사용하면 Git이 파일을 추가하거나 업데이트하는 속도가 빨라질 수 있습니다:
    
    ```bash
    git add -A
    
    ```
    
- **변경된 파일만 추가**:
변경된 파일만 스테이징하려면:
    
    ```bash
    git add -u
    
    ```
    

---

## 3. **대규모 이진 파일 사용**

### 원인

- Git은 텍스트 기반 변경 사항 추적에 최적화되어 있으며, 대규모 이진 파일(예: 이미지, 비디오, 데이터 파일 등)을 관리할 때 성능 저하가 발생할 수 있습니다.

### 해결 방법

1. **Git LFS(Git Large File Storage)** 사용:
    
    Git LFS를 설치하고 대규모 파일을 처리하도록 설정합니다.
    
    ```bash
    git lfs install
    git lfs track "*.bin"
    git add .gitattributes
    git add large-file.bin
    git commit -m "Add large file with LFS"
    
    ```
    
2. **대규모 파일 관리 도구로 이동**:
    
    대규모 데이터를 Git 외부 스토리지(예: AWS S3, Google Drive 등)로 옮기고, 코드만 Git에서 관리하세요.
    

---

## 4. **네트워크 연결 문제 (원격 저장소 관련)**

### 원인

- `git commit` 자체는 로컬 작업이지만, 사용 중인 Git 설정에 따라 커밋 후 자동으로 `git push`를 실행하도록 설정된 경우 네트워크 지연 문제가 발생할 수 있습니다.

### 해결 방법

1. **`git commit`과 `git push` 분리**:
커밋과 푸시를 별도로 실행합니다:
    
    ```bash
    git commit -m "Message"
    git push origin branch-name
    
    ```
    
2. **원격 저장소 연결 확인**:
네트워크 속도 문제를 확인하거나 원격 저장소 연결 상태를 점검하세요:
    
    ```bash
    git remote -v
    
    ```
    

---

## 5. **Git 저장소가 비효율적으로 관리됨**

### 원인

- Git 저장소에 오래된, 불필요한 파일이나 참조가 많아져 저장소가 비대해질 수 있습니다.

### 해결 방법

1. **저장소 정리**:
Git 저장소를 정리하여 불필요한 데이터를 제거합니다.
    
    ```bash
    git gc --prune=now --aggressive
    
    ```
    
2. **로컬 브랜치 정리**:
사용하지 않는 로컬 브랜치를 삭제합니다:
    
    ```bash
    git branch -d old-branch
    
    ```
    
3. **리포지토리 클린업**:
오래된 히스토리를 정리하여 저장소 크기를 줄입니다:
    
    ```bash
    git filter-repo --path-glob "*.log"
    
    ```
    

---

## 6. **기타 성능 문제**

### 원인

- `.git` 디렉토리 내부의 구조나 설정 문제로 인해 Git의 성능이 저하될 수 있습니다.

### 해결 방법

1. **인덱스 파일 재생성**:
Git 인덱스가 손상되었거나 너무 커졌다면, 재생성합니다:
    
    ```bash
    rm -f .git/index
    git reset
    git add .
    git commit -m "Rebuild index"
    
    ```
    
2. **최신 Git 버전 사용**:
오래된 Git 버전은 성능 저하를 유발할 수 있습니다. 최신 버전으로 업데이트하세요:
    
    ```bash
    git --version
    brew upgrade git
    
    ```
    

---

### 최적화 팁

- `.gitignore`를 정기적으로 관리.
- 대규모 파일은 Git LFS 또는 외부 스토리지로 분리.
- 필요 없는 브랜치와 데이터를 정기적으로 정리.

위 방법들을 하나씩 적용해보고 성능이 개선되는지 확인하세요! 😊