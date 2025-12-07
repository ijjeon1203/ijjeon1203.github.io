

240529

git

  

작업순서

  

현재 폴더확인

빈폴더 생성

폴더 이동

로컬 저장소 생성

폴더 생성확인

폴더 내부 확인

  
  

인스타 출처

---

# devops

git

  

base command

  

pull request

branching

  

merging

  
  

git 배우기

프로그래밍 언어 배우기

- python

- go

- java script

리눅스 배우기

shell commands

file system

netwroking

virtualization

posix

  

네트워크 및 보안

osi model

dns

http

ssh

security tools

  

server manage ment

- reverse proxy

- cashing server

- firewall

- web serer

  

컨테이너 배우기

- running containers

- docker files

- networking

- docker-compose

  
  
  
  

# 필요한 것

- branch 나누기

- 당장 시험

- 전체 데이터 베이스

- 프로그램별 branch? 어차피 폴더가 다르니 각각 관리하지 않나

- merging

- 브랜치개념을 폴더 개념으로 바꿔서 합치기

  

가장 최신 받아오기 pull request

  

리눅스 배우기

shell commands

file system

netwroking

virtualization

posix

  

---

```markdown
0530
# 목적

Git을 바탕으로 그 위에 무언가를 만들어 내는 등의 아주 특수한 활용을 목표로 할 때 유용한 내용

지적호기심

Git 내부 구조를 파헤치며 지적 유희를 즐기시려거나, Git 저장소를 활용한 모종의 서비스를 개발하시려는 분들께 유용

문서를 저장하는데 Git 저장소를 쓴다면, 텍스트를 편집하며 이력을 관리하고 차이점을 확인하거나, 몇 명이서 공동 작업을 하기에도 좋을 것 같다

# 장점

가볍고 빠르죠.
'쉘환경이 윈도우보다 편한 개발자들'에게는 다른 툴보다 쉬울 지도

C언어에 char, int, long, float, double과 같은 데이터 타입이 있는 것처럼,
git은 내부적으로 commit, tree, blob, tag의 4가지 오브젝트 타입을 관리

.git/objects에 개별적인 파일들로 존재합니다.
하나의 commit, 하나의 tree, 하나의 blob 그리고 하나의 tag는 각각 하나의 파일

git에 "hello.txt"라는 파일을 하나 추가하면,
"hello.txt"라는 이름의 오브젝트를 생성하는 것이 아닙니다.
"hello.txt"의 내용 전부를 해시테이블에 넣어,
40자리의 해시값을 뽑아내어 오브젝트 파일 이름으로 사용

"hello.txt"를 위한 오브젝트인 blob에는 파일이름인 "hello.txt"라는 문자열이 저장되지 않습니다.
대신 디렉토리 구조를 나타내는 tree 오브젝트에서 "hello.txt"라는 문자열을 찾을 수 있습니다.
이는 리눅스 파일시스템에서 흔히 사용하는 inode - dentry의 관계와 동일

리눅스를 개발한 리누즈가 git에도 동일한 개념을 차용했다는 점은 쉽게 유추할 수 있습니다.
 
이러한 오브젝트들은 하나의 파일로 .git/objects에 차곡차곡 쌓이게 되는데,
한 디렉토리에 너무 많은 파일이 있으면 파일 시스템의 성능이 저하될 수 있기 때문에,
오브젝트의 파일이름 중 앞 2글자는 디렉토리 이름으로 사용하고,
나머지 38글자를 파일이름으로 사용

blob(binary large object)

- 타입 : "blob" 타입- 사이즈 : 컨텐츠의 용량을 bytes로 표시- 컨텐츠 : blob의 컨텐츠에는 텍스트, 이미지, 음악 혹은 단순 이진 파일처럼 다양한 형식의 파일이 저장될 수 있다. 파일이름이나 파일형식은 blob에 저장되지 않는다. 파일의 메타정보를 제외한 파일의 내용 전체를 품는다.

tree

- 타입 : "tree" 타입
- 사이즈 : 트리 오브젝트의 용량을 bytes로 표시
- tree 객체 : 하위 디렉토리의 트리 객체를 재귀적으로 참조할 수 있다.
- blob 객체 : 한 디렉토리에 있는 모든 blob을 담고 있다.
객체에 대한 접근권한, 파일이름은 여기서 관리한다.

commit

- 작성자
- 커밋 실행자
- 커밋 날짜
- 로그 메시지
- tree
- 객체 : 해당 커밋에서의 dir/file의 상태를 알 수 있다.

tag

- 객체종류
- 태그이름
- tagger
- 태그메시지
- PGP 서명정보

git cat-file (-t|-s|-e|-p|<type>|--textconv) <object>

git cat-file (--batch|--batch-check) < <list_of_objects>

# 참고자료

참고 자료
.git 내부 구조 파헤치기

git의 기본 파일 단위인 blob 과 hashing 의 관계에 대해 알아보자

Content-addressable storage

버전관리 시스템이란?

git 버전 관리 정보

시작하기 - Git 기초

Git의 기초 - 수정하고 저장소에 저장하기

ProGit 10장: https://git-scm.com/book/en/v2/Git-Internals-Git-Objects
한글 번역본: [https://git-scm.com/book/ko/v2/Git의-내부-Plumbing-명령과-Porcelain-명령](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EB%82%B4%EB%B6%80-Plumbing-%EB%AA%85%EB%A0%B9%EA%B3%BC-Porcelain-%EB%AA%85%EB%A0%B9)

10장에 Git 내부 구조에 대한 설명

- 한권인건가

프로 git 2판
JGit

# 동작방식

git commit

- index를 바탕으로 사진을 한 장 찍어서 트리구슬을 하나 만든
- 구슬에 대한 커밋구슬을 만듬

# 내용

## 트리

- git commit 은 '스냅 샷'에 자주 비유
- 여럿이서 찍은 사진을 보면 그 순간의 모든 상황들이 그려지는 것처럼
- 커밋하는 순간에 스테이지에 있던 작업파일들의 ID뿐 아니라 실제 파일이름, 어느 디렉토리에 속하는지 같은 전체 관계도가 담겨 있음

## 커밋

- 메모의 역할
- 이 메모가 어떤 사진에 대한 건지 즉
- 트리의 ID, 저자와 커미터, 부모커밋의 ID, 그리고 우리가 git commit -m 의 커밋메시지

# 명령어

init
add
commit

책은 42서울 집현전에 여러 권이 비치되어 있습니다.
저수준 명령어로 직접 Git 내부 확인하기: p.277~301
Git의 각 공간에 대한 정확한 의미 정리: p.222

blob
tree
commit
tag

git은 4개의 object로 관리

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/3466804d-000f-4e11-8044-e2efd8bbeb4f/a092ce47-e03a-47cd-aead-36c5152abfb3/Untitled.png)

object 관리

# 예시

test 디렉터리에 git init를 한 뒤에, hello.txt를 만들고 "안녕 나는 공부중이야" 를 저장한다. 그 뒤 git add하고 git commit한다. 마지막으로 git tag를 한다. 이 과정중에서 생성되는 object들을 보자.

1. blob
git add할 때 생성된다. 파일 내용이 들어 있다
2. tree
git commit할 때 생성된다. 타입과 객체명, 파일명이 기록된다.
3. commit
git commit할 때 생성된다. tree객체명, 부모commit객체명, author, committer, message를 기록한다. 이는 commit할때 git config에 있는 name과 email이 찍히는 거다.
4. tag
git tag할 때 생성된다. commit 객체명, tag이름, tagger, message가 기록된다.

# 아이디어

이름 jgit

수동으로 업데이트 한번

자동저장?

메모 입력 commit 은 있으면 좋고 아니어도

무엇이든임베드

별개의 프로그램으로 관리하기?

프로그램에 삽입해서 관리하기?

.fm

- fileManager

# 작업

캡처파일로 가지고 있기? 저장을 해야함? ctrl c 만안하면

저장안하고 다시 그냥 캡처하는게빠를듯

질문

서점에서 책보기?

https://maintainhoon.vercel.app/blog/post/git_internal_behavior

https://medium.com/happyprogrammer-in-jeju/git-내부-구조를-알아보자-1-기본-오브젝트-81b34f85fe53

https://medium.com/happyprogrammer-in-jeju/git-%EB%82%B4%EB%B6%80-%EA%B5%AC%EC%A1%B0%EB%A5%BC-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90-1-%EA%B8%B0%EB%B3%B8-%EC%98%A4%EB%B8%8C%EC%A0%9D%ED%8A%B8-81b34f85fe53

- 둘다같은 주제 같은데 걍 다삭제?
- 이전 주소 책 활용 먼저 찾기?

위 주소 두개 [] 랑 () 잇엇음 
이거삭제하는법?

gpt 한테 물어보기?

```

# 0531

트리 체리픽등의기능알기 위한 구매?

- 디테일이 더잇음
- 책 잘샀네

프로젝트 이력추가

분산 아키텍처 장점

- 항상 인터넷 연결x
- 브랜치 항상합치기 아니 쉽게

버전관리 기본

- 파일복사본 파일이름 변경

# 기능

변경한 모든내용추적
언제누가변경내용

중앙저장소방식

- 사용자 최신 버전코드만정보 요청해먀함

동기화 이슈
내가 수정한내용 제대로 가지고있는지

무엇저장

- 프로젝트. 구성 전부

# 아이디어

## 최종본

# 폰

에 다 들고 있을라면?
꼭 필요한정보들?

중복될 필요 없으니?

스케줄 프로그램

일지

- 매일 작성 할듯?
- 안해도 되지만?

# 넣을 내용

- 작성한 데이터 내용
- 추가 주석내용 이건기능
그외 정보들
- 용량을?
    - 용량생각해야지
- 고민은 업데이트 되겠지
    - 해결한목록들

## 동기화이슈

넘 자주 동기화해도 안좋음

# 개선

더좋은방식?스냅샷보다

- 오히려 순서바꾸면깔끔해질?

아이디어

 새로울수도 기존에 있는거에 추가할수도

# 파일병합

컴터작업 폰작업 출처만 밝히고 합치기

# 자동커밋

떠오른당시 

수정

확인

git init

readme, 등의 실험 파일 추가 

- 해시 생성됨

add 하고 cat으로 열어보기 

- blob 생성
- 

커밋

- 트리오브젝트

푸시

Git은 데이터를 저장하기 전에 항상 체크섬을 구하고 그 기준으로 데이터를 관리합니다. 그 체크섬을 구하는데 SHA-1 해시를 사용하고, 그러면 체크섬은 160 bit가 되고, 이를 16진수로 표현하면 40자

저장소에 보관하는 파일도 이 체크섬을 키로 해서 보관하고, 전체 트리(디렉터리)도 이 체크섬으로 보관하며, 커밋에 대한 데이터도 이 체크섬 기준으로 보관

이 40자는, 온 세상에서 “거의” 유일한 값이 나오므로, 고유키로 쓸 수 있습니다. 그리고 찾고자 하는 범위를 “한 저장소 안”으로 좁히면, 앞의 몇 글자만 써도 대부분 달리 겹치지 않아서, 여덟 자나 열 자로만 줄여서 쓸 수도

$ git show 8a8363d93e61185f6df18ed61321626be514c7f4

$ git show 8a8363d

같음

**내용을 주소로 활용 (Content-addressable Key-Value Storage)**

“Git은 내용을 주소로 활용하는 파일시스템(content-addressable filesystem)

- Git의 내부는 사실 꽤 단순한(man 페이지에 보면 stupid라는 단어를 쓰고 있습니다)
- 키-밸류 데이터베이스

. 어떤 데이터든 Git에 담을 수 있고, Git은 그 데이터의 SHA1 해시값을 키값으로 해서 저장합니다. 그러면 나중에 다시 그 SHA1 값을 기준으로 보관했던 데이터를 찾을 수 있지요. 이 단순한 키-밸류 스토리지 위에 몇 가지 방식으로 데이터를 담고, 그걸 잘 가져다 활용해서, 결국 겉으로 보기에는 버전 관리 시스템

구체적으로 말하면, SHA1 해시값을 키로 해서, .git/objects/ 디렉터리 아래에 마흔 자에서 앞 두 자로 디렉터리를 만들고 나머지 서른여덟 자를 파일명으로 해서 특정한 형태로 저장합니다. 아무래도 모든 오브젝트를 한 디렉터리에 다 담으면 불편한 점들이 있으니, 한 단계 더 나눠서 256(2⁸)개 디렉터리로 나눠 담는 것이죠. 그래서 아까 git add README.md로 추가한 내용이 8a라는 디렉터리 아래에 생긴 것

 Git을 쓰는 명령어

저수준(low-level)의 기본적인 일을 처리하는 plumbing 명령어들

고수준(high-level)에서 사용자가 일반적으로 쓰는 porcelain 명령어들

두 단어의 각 뜻은 화장실의 “plumbing: 수도 설비, 배관”과 “porcelain: 타일에 쓰이는 자기”라는 뜻인데, 우리가 화장실을 쓸 때는 겉의 타일만 보지만, 실제 복잡한(더러운) 일들은 내부의 배관들이 한다는 식의 비유

이 그림과 함께 다시 설명하자면, git은 OS의 일반 파일시스템 위에 특정 .git/ 디렉터리에 파일들을 읽고 쓰면서, 이를 키-밸류 스토리지로 활용합니다. git의 키-밸류 스토리지에 직접 접근하는 저수준 명령어를 plumbing 명령어라고 하고, 그 plumbing 명령어들을 써서 사용자에게 유용한 기능을 제공하는 고수준 명령어를 porcelain 명령어라고 합니다.

터미널에서 CLI로 바로 git을 쓰는 분들은 이 porcelain 명령어를 쓰는 것이고, 각종 git GUI이나 IDE에서 git을 쓸 때는, 그 앱들이 porcelain 명령어들을, 그리고 필요에 따라 때로는 plumbing 명령어를 써서 우리에게 버전 관리 기능을 제공하는 것이죠. (사실 GUI나 IDE들은 JGit이나 libgit2 같은 라이브러리를 쓰지만, 그 라이브러리들도 plumbing / porcelain API로 나뉘어 있어요)

![Untitled](Untitled.png)

 K-V storage 부분에 Git이 내부적으로 저장하는 오브젝트는 일반 파일의 내용을 보관하는 blob, 그 blob들이 어떤 디렉터리 위치에 어떤 속성과 이름으로 저장되는 지를 나타내는 tree, 그리고 매 커밋 순간의 스냅샷을 가리킬 수 있는 commit

그 commit을 가리키는 레퍼런스인 브랜치나 태그, 그리고 현재 작업 중인 브랜치의 최종 커밋을 가리키는 HEAD

# **Blob 추가**

BLOB(Binary Large OBject)을 하나 추가해 볼게요. Git이 우리 프로젝트에 필요한 소스 파일, 이미지 파일 등 데이터를 이 blob으로 저장하는데, 파일명 같은 메타데이터(metadata) 없이, 바이너리 데이터 자체만 저장합니다. 저장할 때 사용하는 파일명(키값)은 SHA1 해시값 40 글자이고요.

여기서 git hash-object라는 plumbing 명령어를 써서 보여드리는데요, 이는 아까 git add README.md로 porcelain 명령어를 썼을 때 내부적으로 활용되는 명령어

SHA1 해시값을 디렉터리와 파일명으로 해서 저장한 파일의 내용을 보면, 바이너리 포맷으로 알 수 없는 내용이 담겨있습니다. file에게 물어봐도, VAX COFF executable라는 엉뚱한 답을 돌려줍니다.

# **zlib으로 압축해서 저장**

문서에 따르면 .git/objects/에 저장하는 파일들은 [zlib](http://www.zlib.net/)으로 압축됩니다. 그래서 우선 zlib으로 압축을 풀어야 그다음 파악을 할 수 있어요. zlib은 무료로 공개된 압축 알고리즘이자 라이브러리로, 라이선스가 자유롭기 때문에 널리 사용되고 있습니다. 각종 프로그래밍 언어의 표준 라이브러리에도 들어있지요. 그런데, 정작 CLI로 압축을 하거나 푸는 프로그램은 마땅치 않네요. 좀 번잡해 보이지만, 루비 스크립트를 써서 zlib 압축을 풀어서 확인해 보겠습니다.

# **오브젝트 헤더**

앞서 본 blob처럼, tree와 commit 오브젝트도 같은 형태의 헤더로 시작하고, 본문은 각 나름의 형태로 저장됩니다. (blob은 단순히 원래 내용이 그대로 담깁니다)

> blob_바이트수\0
> 

각 오브젝트 헤더는, blob / tree / commit 등의 문자열로 시작하고, 오브젝트의 타입을 나타냅니다. 이어서 공백 문자가 하나 따라오고, 그다음 헤더를 제외한 본문의 바이트 수를 문자열로 표기합니다. 마지막으로 NULL(\0) 문자가 있어서, 헤더의 끝임을 알립니다.

앞서 확인한 오브젝트는 blob 타입에 본문은 총 22바이트 길이라는 뜻의 헤더였던 거고, 그 뒤에는 단순히 본문이 그대로 들어있던 것이죠.

별거 없죠?

# **트리(tree) 오브젝트**

지금껏 살펴본 blob은 그 내용만 저장되고, 메타데이터는 저장되지 않는다고 말씀드렸는데요, 이제 파일명 같은 기본적인 메타데이터를 어디에 저장하는지 알아볼 차례입니다. 파일 이름과 기본 속성, 그리고 어느 디렉터리에 속하는 지의 정보를 tree 오브젝트에 기록합니다.

한 tree 오브젝트는 특정 시점의 한 디렉터리를 표현할 수 있습니다. 디렉터리 안에는 여러 파일이나 서브 디렉터리가 들어갈 수 있는 것과 마찬가지로, tree 아래에는 여러 blob과 다른 여러 tree가 들어있을 수 있습니다.

# **tree 저장 포맷**

tree 오브젝트 파일의 내부는, blob 오브젝트와 마찬가지로 zlib으로 압축한 내용이 저장되며, 압축하기 전의 데이터는 오브젝트 헤더로 시작합니다.

> tree_바이트수\0
> 

그리고, 헤더 다음에 이어지는 본문은 tree에 포함되는 여러 아이템을 차례로 기록하며, 각각의 아이템은 아래 형태로 저장됩니다.

> 타입_파일명\0오브젝트ID
> 

맨 앞에 타입에는 문자열로 100644, 100755, 040000 등의 여섯 자리 문자열이 옵니다. 각각 차례로, 일반 파일, 실행 파일, 디렉터리를 뜻하고, 이 외에도 심볼릭 링크 등의 타입이 있을 수 있습니다. 이 정보만으로도, blob인지 tree인지 알 수 있기에 별도로 blob/tree 정보는 기록되지 않습니다. 이어서 공백 문자가 오고, 그 다음 NULL문자로 끝나는 문자열로 파일명을 표현합니다. 마지막으로 이 아이템이 가리키는 SHA1 해시값이 오는데, 기록되는 포맷이 16진수 문자열 표현이 아니라, 그냥 20바이트 바이너리 값입니다. 이렇게 한 아이템이 표현되고, 별도의 구분 문자 없이 바로 다음 레코드가 이어집니다.

 git cat-file이라는 plumbing 명령어로 쉽게 살펴볼 수 있음

t옵션으로 오브젝트의 타입이 blob인지, tree인지 commit 인지를 알아볼 수 있고, 

-p옵션을 주면, 실제 담고 있는 내용을 보기 좋게 출력

git 구조도

![d](1.png)

[http://pseudocode.fm/episodes/8](http://pseudocode.fm/episodes/8)

[정의](https://www.notion.so/7b65f72cbd404001aa0ee575a03d5c73?pvs=21)

[목적](https://www.notion.so/0cadfc68ff8d43e99ffd3b61d25bfea3?pvs=21)

[장점](https://www.notion.so/924f68d675f241ab81687001dfc5c528?pvs=21)

[확인예시](https://www.notion.so/d3a4bf5bc60e4317b27273bb2ef50b6b?pvs=21)

[명령어](https://www.notion.so/7c1394d5d43c40ea95a23793d1fbf451?pvs=21)

[고민](https://www.notion.so/e1ecac33694c4fd7bcb53b20ba46f7ad?pvs=21)

[구성](https://www.notion.so/a3c8b08c81c4493a8511c43799320b72?pvs=21)

파일 만들기 vs 이름 변경하기?

각각만들어야하니까

설계할거랑 기존것 분석 같아야?

- 둘다프로그램이니까 프로그램은 다 같아야?

### **참고 자료**

- [지옥에서 온 Git](https://opentutorials.org/module/2676)
- [Git 내부 구조를 알아보자 (1) — 기본 오브젝트](https://medium.com/happyprogrammer-in-jeju/git-%EB%82%B4%EB%B6%80-%EA%B5%AC%EC%A1%B0%EB%A5%BC-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90-1-%EA%B8%B0%EB%B3%B8-%EC%98%A4%EB%B8%8C%EC%A0%9D%ED%8A%B8-81b34f85fe53)
- [Git Manual](https://git.kernel.org/pub/scm/git/git.git/tree/README?id=e83c5163316f89bfbde7d9ab23ca2e25604af290)

240602

🌱 Additional icons- On the Desktop : 바탕화면에 바로가기 아이콘 생성
🌱 Windows Explorer integration- Git Bash Here : 폴더에서 바로 Git에 접속하는 Git Bash Here 추가- Git GUI Here :  폴더에서 바로 Git GUI에 접속하는 Git GUI Here 추가
🌱 Git LFS (Large File Support)- 대용량 파일 지원
🌱 Associate .git* configuration files with the defalut text editor- .git* 구성 파일을 기본 텍스트 편집기와 연결
🌱Associate .sh files to be run with Bash- 실행할 .sh 파일을 Bash와 연결
🌱 Check daily for git for Windows updates- 윈도우 업데이트에 대한 새로운 업데이트 매일 확인
🌱 (NEW!) Add a Git Bash Profile to Windows Terminal-  윈도우 터미널에 Git Bash 프로파일 추가

Standalone Installer과 Portable 두 가지가 있습니다.
Standalone은 실행파일을 다운 받고,
Portable은 무설치 버전 파일입니다. 즉, exe파일이 아닌 7z 압축파일이 설치


# git 설치파일 실행

🌱 Let Git decide- git이 기본 분기 이름(master)을 사용
🌱 Override the default branch name for new repositories-  새 레포지토리의 기본 분기 이름을 재정의
🌱 Use Git from git bash only- Git bash의 Git만 이용
🌱 Git from the command line and also frm 3rd-party software-  명령줄에서 Git 및 타사 소프트웨어에서도 Git 제공
 
🌱 Use git and optional unix tools from the command prompt-  명령 프롬프트에서 git 및 선택적 유닉스 도구 사용


ssh 실행 도구를 선택합니다.
 
🌱 Use bundled openssh- Git에서 제공되는 opensh 번들 사용
🌱 Use external openssh-  외부 opensh 사용
HTTP 연결을 설정합니다.
 
🌱 Use the OpenSSL library- OpenSSL 라이브러리 사용
🌱 Use the native Windows Secure Channerl library-  기본 Windows 보안 채널 라이브러리 사용
- 윈도우즈 인증서 저장소를 사용하여 검증
줄 바꿈 옵션을 선택합니다.
 
 
🌱 Checkout Windows-style, commit Unix-style line endings- Git이 저장소에서 파일을 체크아웃할 때, Windows 스타일의 줄 바꿈 문자(CRLF)를 Unix 스타일의 줄 바꿈 문자(LF)로 자동변환  
- Git이 커밋할 때, Unix 스타일의 줄바꿈 문자(LF)를 사용하여 커밋
🌱 Checkout as-is, commit Unix-xtyle line endings
- Git이 체크아웃할 때 줄바꿈 문자를 변환하지 않음
- Git이 커밋할 때 Unix 스타일의 줄 바꿈 문자(LF)를 사용하여 커밋 
 
🌱 Checkout as-is, commit as-is
- Git이 체크아웃할 때 줄 바꿈 문자를 변환하지 않음
- Git이 커밋할 때 줄바꿈 문자 그대로 커밋
 
 
이 옵션은 저장소에서 이미 다른 줄 바꿈 문자 처리방식으로 커밋된 파일들이 함께 있을 때, 파일의 줄 바꿈 문자를 변경하지 않고, 그대로 유지하고자 할 때 사용됩니다. 
🌱 Use MinTTY(the default terminal of MSYS2)- Git Bash를 실행할 때, MSYS2 프로젝트에서 개발한 MinTTY 터미널 애뮬레이터를 사용
- MinTTY는 리눅스와 유사한 터미널 환경 제공
🌱 Use Windows' default console window
- Git Bash를 실행할 때, 윈도우 기본 콘솔 창을 사용
 

git pull의 기본 동작을 선택합니다.
git pull 은 원격 저장소에서 변경 사항을 가져와 로컬 브랜치에 병합하는 명령어입니다.
 
 
🌱 Default(fast-forward or merge)- fast-forward가 가능한 경우, fast-forward 병합을 수행하고, 그렇지 않은 경우 merge 병합 수행
🌱 Rebase
- 'git pull --rebase'를 실행할 때, Git은 원격 저장소에서 변경 사항을 가져온 후, 
로컬 브랜치의 이력을 원격 브랜치의 이력 위에 쌓아 올리는 작업(rebase) 수행
 
🌱 Only ever fast-forward
- 'git pull --ff-only'를 실행할 때, Git은 fast-forward 가능한 경우에만 fast-forward 병합 수행
- 그렇지 않은 경우, 병합 수행 x, 오류 발생
 
fast-forward는 Git에서 브랜치 병합을 수행할 때, 브랜치 이력을 간단히 이동시키는 방법
merge는 두 개 이상의 브랜치를 병합하는 작업
 자격 증명 도우미를 선택합니다.
 
자격 증명 도우미는 Git을 사용할 때 인증 정보를 관리하는 도구입니다.
 
 
🌱 Git Credential Manager
- 자격 증명 도우미 사용
- 인증 정보를 한 번 입력하면 그 이후로 자동으로 인증 정보를 사용하여 Git 저장소에 접근
 
🌱 None
- 자격 증명 도우미 사용 x
- Git에서 인증 정보를 입력할 때마다 매번 사용자 이름과 비밀번호를 입력
 🌱 Enable file system caching
- Git이 파일 시스템 캐시를 사용하는 옵션
- Git이 파일을 읽고 쓰는 속도가 더 향상
 
🌱 Enable symbolic links
- Git이 심볼릭 링크를 지원하는 옵션
- 심볼릭 링크는 파일이나 디렉토리를 가리키는 포인터
- 사용하지 않으면 Git이 심볼릭 링크를 저장소에 저장하지 않고 대신 링크 대상 파일의 내용 저장
- 링크 대상 파일이 변경되었을 때 Git에서 적절하게 대처할 수 없으므로, 
심볼릭 링크를 사용하는 경우 이 옵션 활성화
 실험적 기능 사용 여부를 선택합니다.
 
🌱 Enable experimental support for pseudo consoles 
- Git이 윈도우 환경에서 가상 콘솔(pseudo console) 지원
- 가상 콘솔은 프로그램과 터미널 간의 인터페이스로,
커맨드 라인 애플리케이션과 터미널 간의 상호작용이 가능
 
🌱 Enable experimental built-in file system monitor
- Git이 내장 파일 시스템 모니터(experimental build-in file system monitor) 지원
- 파일 시스템 모니터는 파일 시스템의 변경 사항을 감지하여
 Git 작업을 자동으로 업데이트할 수 있는 기능 제공
   
  

# git 정리

  

- commit 내용 가져가기

- 커밋정보확인하기

  

python 프로젝트 다 올렸으니 로컬에서 삭제하기

  

git repository 열지 않으면 처음 열면 다시 최상위경로

  

# git repository 정리

  

## 오픈소스인것

  

**Subtitle Edit**

  

[**Interview_Question_for_Beginner](https://github.com/idwn1203/Interview_Question_for_Beginner)** 

  

[**tesseract](https://github.com/idwn1203/tesseract)**

  
  

# github io

  

# github 블로그

  

## 화면구성

  

리모컨

  

본문

  

메인테두리?

  

[블로그 테마를 고를때 고려해야 할 점 5가](https://isme2n.github.io/jekyll/2017/03/09/Blog-Jekyll/)지

  

- 첫째, 반응형이어야 한다.

- 둘째, 리니어 레이아웃.

- 셋째, 공유하기 버튼.

- 넷째, 서체.

- 다섯째, 댓글.

  

https://long-haul.netlify.app/

  
  

git 나무위키

  

- https://namu.wiki/w/Git

  

git install 다운 페이지

  

- https://github.com/git/git/blob/master/INSTALL

- https://git.kernel.org/pub/scm/git/git.git/log/

  
  

https://code-boki.tistory.com/105

  

https://github.com/egoing/gistory?tab=readme-ov-file

  

https://tecoble.techcourse.co.kr/post/2021-07-08-dot-git/

  

# github 블로그

  

https://github.blog/2022-02-14-include-diagrams-markdown-files-mermaid/

  

240602

# 버전관리시스템

- 파일의 변경사항을 추적할 수 있도록 돕는 방법론 혹은 도구

  
  
  
  

## 버전관리 시스템과 은행 금고 비교

소스코드 은행금고돈

변경한내용 기록

- 검토하여 이력 확인가능

  

거래내역입금 커밋

  
  

# 발전과정

  

변경내역을 저장한컴퓨터에 직접로그인

- 이게 불편하니까 cvs 나 서브비전 도구만들어짐

- 원격에서 작업한 후 네트워크 연결을 통해 저장소에 변경 사항을 전송 할 수 있음

  

## 중앙집중식 저장소 모델

하나의 중앙 저장소 에 변경사항 전송

- 최신버전 복사해서 가지고있음

- 병경이후 다시 전송

  

- 변경이력을 보려면 저장소에 정보요청

- 원격저장소로 접근

  
  

모든팀원이 변경 사항을 전송하는 중앙 저장소 대신 각자가 프로젝트의 전체 이력이 있는 자신만의 저장소를 가짐

  

커밋할 때 원격 저장소에 연결할 필요 없이 변경사항을 지역저장소에 기록

  
  
  

# 구성

저장소

- 사용자가 변경한 모든 내용 추적

- 언제변경

- 누가

- 변경사항 설명

  

소스코드

  

빌드 파일

makefiel

rakefile

ant의 build.xml 파일등

  

설정 파일 예제

문서 어플리케이션에서 사용하는 이미지

  
  
  

# 그외

progmatic bookshelf 의 starter kit 시작도구

  

## 그외 분산버전관리 시스템

  

바자

머큐리얼

  
  

# git의 역사

리눅스 토르발즈가 개발

간단한 스크립트 모음에서 강력한도구로 성장

  
  

# git의 장점

  

네트워크와 분리되어 작업할 수 있음

원하는 내용을 공유할수있음

프로젝트 이력 추적 가능

  
  

브랜치

- 생성하기 쉬움

- 비용 적음

- 속도 빠름

- 브랜치 여러번 나눈 경우라도 간단히 합칠 수 있다.

  

서브 버전과 통신

- 서브버전 저장소의 모든 이력 가져 올 수 있음

- 변경사항 다시 보낼 수 있음

  

# 구성

저장소

저장대상 결정

파일조작,동기화

  

작업트리

- 작업 복사본

- 저장소를 바라보는 자신의 현재시점

  

.git 디렉터리 에 저장

checkout

git이 사용자의 작업트리를 특정 시점과 일치하도록 하는 작업

  
  
  
  
  

태그를 이용한 마일스톤

branch

- 합치기

파일잠금

  
  
  
  
  

개발 - 단위테스트 - 커밋

  

무엇변경했는지 설명

- 언제버그가 발생했는지 추적 가능

  
  

바뀐 내용을 다른 개발자가 이용하게 하려면 변경사항을 공유해야함

상위저장소(upstream repository) 에 변경 사항을 푸싱하면 바뀐내용 공유 가능

  

pushing 다른 개발자들과 공유하려고 다른 저장소에 전송하기 위해 사용

  

상위 저장소 공용 저장소

  

다른 개발자들도 변경 사항을 푸싱할 수 있다

  

동기화 과정

pushing 각자 패치 해놓기

  

원격저장소가 가지고 있는 변경사항 요청

가져온 변경사항 지역 이력과 합침

  

변경사항 가져오고 합치는 작업 동시에 진행 이걸 pulling 이라 함

  
  

프로젝트 디렉터리 파일 추적

  

# 저장 대상 구조화하는 방법

  

최하층계층에서 저장하파일 내용단위로 추적

  

파일추적하는 대신 변수나 함수 등을 구성하는 각 문자와 줄 추적

이름

파일모드

님볼릭 파일여부와 같은 메타데이터를 추가

- 저장소 전체 이력을 저장하는데 필요한 공간이 줄어듬

- 두 파일 사이에서 함수나 클래스의 이동을 알아내거나 어디에서 복사된 코드인지 결정하는 것과 같은 작업 가능 해짐

  

모든 수정은 작업트리에서 일어남

저장소에 대한 현재 시점을 표현하며 일련의 평범한 디렉터리와 파일로 이루어짐

  

저장소에 파일과 디렉터리를 구성하는 방법은 프로젝트에 따라 다름

- 대부분 미리 정해 놓음 프로ㅈ겍트 기준

  

- 프로젝트 마다 새로운디렉터리 만들어 이력 공유하는 방식

- 프로젝트마다 새로운 저장소 만드는 방식

  

특정 마일 스톤을 달성했을 때 저장소 상태 추적할 수 있어야함

  

태그를 이용해 이러한 상태를 추적

  
  

태그 저장소 이력의 특정시점을 기록하는 용도로 사용하는 이름

  

특정리비전의 태그에 부여

  

브랜치로 분기 이력 만들기

프로젝트 전체 이야기 얻으려면 처음부터 끝까지

  

이야기 진행방향 여러개 이력 다른경우

  

달력 기능있는 프로젝트

  

달력 다시 작성 하려면 팀원동의필요ㅠ

변경사항추적

코드적체 다른 디렉터리에 복사해두고 바꾸기 시작

변경내역 추적할 수 없음

실수 되돌릴 수 없다는 문제

  
  

브랜치 생성하면 파일이 분기하는 위치가 저장소에 기록

브랜치는 다른 브랜치와 분리하여 내용에 대한 변경사항을 지속적으로 추적

- 분기이력 생성

  

마스터 브랜치

  

반드시 다른 브랜치와 합쳐야 한다는 엄격한 규칙은 없음

  

나줌에 지울 실험용 브랜치

주요버전 브랜치 일수도 있음

  
  

지역 브랜치를 생성하고 공유하지 않는 경우

몇가지 실험해보고 만족스러운 수준 되면 공유

실험한 내용 제대로 동작하지 않으면 조용히 지워버리기

  

합치기

git 은 두 브랜치의 변경사항을 놓고 어디서 변경이 발생했는지 비교

  

서로다른영역인경우

- 알아서 합침

  

서로 같은 영역인 경우 충돌 발생 후 알림

  

합치기 추적 합쳐진 커밋 내역 추적 이미 합쳐진 내용 다시 합치지 않음

  

잠금

- 특정코드 복사본 한번에 한 사람 만 가질 수 있음

  

낙관적 잠금

서로 변경한 영역에 충돌이 없으리라고 가정하므로 다수의 개발자가 같은 파일에 있는 동일한 코드 이용하는것을 허용

  
  
  

형상관리 CM ( Configuration Management )

형상 관리 도구는 애플리케이션의 여러버전에서 서로 다른 구성(configuration)을 다루기 위해 설계된 도구

  
  
  
  

걍 지우고 다시 치는게 나을경우

- 이미 있는경우

- 다시 쳐서 더 깔끔한 경우가 오히려 더 많을?

- 일부러는 시간 아까움

  

대부분의 버전관리시스템 자신이 가지고 있는 복사본과 떨어져 존재

  

프로젝트 코드를 저장할 위치를 정해야함

  
  

# 커밋

커밋은 저장소에 저장된 개별적인 이력

코드의 진행 상태를 기록함

  

git 은 앞에서 설정한 내용을 참조해서 사용자 이름과 이메일 주소를 기록하고 각 커밋에 메시지를 추가함

  

-m 옵션 다음 문자열이 커밋에 추가되는 메시지

  

git commit 은 공간을 절약하기 위해 일곱자리만 보여줌

  
  

## sha 보안해시 알고리즘 약어

- secure hash algorithm

- 데이터에 대한 짧은 문자열이나 요약 메시지 만으로도 다른 해시와 충돌할 가능성이 거의 없도록 설계

  

- git은 커밋하는 사람 정보 현재시각과 같은 저장소의 몇가지 메타 데이터를 이용해 커밋명을 생성

  

- 이런 정보를 조합해 다른 커밋과 충돌할 가능성이 낮은 고유한 해시를 생성

  

- 가능성은 있지만 마흔자리 문자열 기억하기 쉽지 않고 불필요하게 김

  
  
  
  
  
  

# git 에서 사용자 코드를 저장하는 곳

  

1. 파일 편집할때 직접 이용하는 작업 트리

2. 인덱스 == 스테이징 영역

- 작업트리와 저장소 사이의 버퍼 공간

- 저장소에 커밋하려는 대상만 올려두는 용도로 사용

3. git 이 코드를 저장하는 저장소

  

파일을 커밋하려면 변경사항을 스테이징 해야함

  
  

# 상태

  

파일상태

- modified

- committed

  

색깔별 구분

  
  

확인 명령어 : git status

  
  

# 커밋 메시지

- 커밋의 이유를 설명하는 모든 메타데이터 포함해야함

- 완벽한 로그메시지를 만드는 데는 장인 정신이 필요

  
  

분기이력

마음가는대로 사용하면 됨

범위 줄이기

유용한 형태의 브랜치

여러버전을 브랜치 별로 관리하기 위해 생성한 브랜치와 특정기능을 다루는 주제 브랜치

  

각 기능별로 기능 구현하려 할 때

  

add 로 로컬에서 stage 에 옮기고

commit 으로 stage에서 저장소로

  
  

편집기가 파일 변경됐다고 알려줌

- 이건 편집기 기능아닌가?

  

태그

1.0

  

2.0

  

branch 관리

- rebase

  

# 릴리스

rebase

  

릴리스 할때 프로젝트 이력 항상 함께 배포하지 않음

zip 파일 형태로 제공하는 정도

  

git archive 명령어

  

tar, zip 파일로

  

tar는 단순히 파일을 묶어줄 뿐 압축하지는 않음

zip은 압축파일형식이기 때문에 결과를 압축하려고 다른 프로그램에 입력으로 전송하지 않아도 되기에 직관적임

  

갱신할 위키페이지

코드를 배제한 인수테스트일지도

  

# 원격 저장소

  

받아오기

명령어 git clone

  

원격위치 사용할 로컬 디렉터리

  
  
  
  
  
  
  
  
  
  

# 아이디어

  

저장소의 프로젝트 구조가 최종적인 목차가 되는것?

# Git

  
  

[Git Repository](Git%200cb8598b5ff14ff9aa5004c88f5065be/Git%20Repository%20accb50712d164ef59b20716006c9cc25.md)

  

[Branch](Git%200cb8598b5ff14ff9aa5004c88f5065be/Branch%20def1301873f941ddbcd9724928888e0d.md)

  

# 도구

  

[도구](Git%200cb8598b5ff14ff9aa5004c88f5065be/%E1%84%83%E1%85%A9%E1%84%80%E1%85%AE%20e46eb11947954ef6bf7339afac7ec23e.md)

  

# 사용

  

작업을 할 때 브랜치의 수명은 되도록 짧게 가져가는 게 좋지만, feature 브랜치에서 기능을 완료하는데 해야 할 작업들이 많아서 오래 걸리는 경우 들이 있습니다. 그러다 보면 develop에 추가된 기능들이 필요한 경우가 종종 생기게 됩니다. 그럴 때는 feature 브랜치에 develop의 변경사항들을 가져와야 합니다.

  

1. feature-user 브랜치에 upstream/develop 브랜치를 merge 합니다.

> (feature-user)]$ git fetch upstream(feature-user)]$ git merge –no-ff upstream/develop

>

2. upstream/develop의 변경사항이 merge된 feature-user를 upstream에 push 합니다.

> (feature-user)]$ git push upstream feature-user

>

  

### **3. 완료된 기능을 이번 출시 버전에 포함시키기**

  

드디어 feature-user 브랜치에서 작업하던 기능이 완료되었습니다. 이젠 feature 브랜치를 이번 출시 버전에 포함시키기 위해서 develop에 merge 해야 합니다.

  

1. develop 브랜치에 upstream/feature-user 브랜치를 merge 합니다.

> (develop)]$ git fetch upstream(develop)]$ git merge –no-ff upstream/feature-user

>

2. upstream/feature-user 기능이 merge된 develop를 upstream에 push 합니다.

> (develop)]$ git push upstream develop

>

  

### **4. QA 시작하기**

  

이번 버전에 포함되어야 할 기능들이 모두 완료되었습니다. 이제부터 출시 담당자가 해야 할 일이 많습니다. 출시 담당자는 QA를 시작하기 위해 먼저 release 브랜치를 생성하고 upstream에 push하여 release 브랜치를 공유합니다.

  

1. release-1.0.0 브랜치를 생성합니다.

> (develop)]$ git fetch upstream(develop)]$ git checkout -b release-1.0.0 –track upstream/develop

>

2. release-1.0.0 브랜치를 upstream에 push합니다.

> (release-1.0.0)]$ git push upstream release-1.0.0

>

  

### **5. QA 중 버그 수정하기**

  

개발을 완료한 후 QA 중 버그가 발생하지 않으면 좋겠지만 항상 생각지 못한 예외 상황들이 발생하게 됩니다. 예외 상황이 발생할 때마다 버그 티켓이 하나씩 생성되는데 이 티켓들을 모두 해결해야만 앱을 출시할 수 있습니다.버그 티켓들도 티켓이기 때문에 ‘1. 티켓 처리하기’와 같은 방법으로 처리합니다.

  

1. release 브랜치에서 버그 티켓에 대한 브랜치를 생성합니다.

> (release-1.0.0)]$ git checkout -b bfm-101_bug_login_id_max_length

>

2. 버그를 수정합니다. (뚝딱뚝딱 :hammer:)

3. 작업 브랜치에 버그 수정 사항을 커밋합니다.

> (bfm-101_bug_login_id_max_length)]$ git commit -m "BFM-101 로그인 아이디 길이 제한 버그 수정"

>

4. 작업 브랜치를 origin에 push 합니다.

> (bfm-101_bug_login_id_max_length)]$ git push origin bfm-101_bug_login_id_max_length

>

5. Github에서 bfm-101_bug_login_id_max_length 브랜치를 release-1.0.0에 merge 하는 Pull Request를 생성합니다.

6. 동료에게 리뷰 승인을 받은 후 자신의 Pull Request를 merge 합니다.

  

### **6. 앱 출시**

  

발생하는 버그들을 모두 수정했다면 이젠 출시를 준비할 때입니다. release 브랜치를 master 브랜치와 develop 브랜치에 merge하고 마지막으로 master 브랜치에서 버전 태그를 달아줍니다.

  

1. release 브랜치를 최신 상태로 갱신합니다.

> (release-1.0.0)]$ git pull upstream release-1.0.0

>

2. release 브랜치를 develop 브랜치에 merge 합니다.

> (release-1.0.0)]$ git checkout develop(develop)]$ git pull upstream develop(develop)]$ git merge –no-ff release-1.0.0

>

3. develop 브랜치를 upstream에 push 합니다.

> (develop)]$ git push upstream develop

>

4. release 브랜치를 master 브랜치에 merge 합니다.

> (develop)]$ git checkout master(master)]$ git pull upstream master(master)]$ git merge –no-ff release-1.0.0

>

5. 1.0.0 태그를 추가합니다.

> (master)]$ git tag 1.0.0

>

6. master 브랜치와 1.0.0 태그를 upstream에 push 합니다.

> (master)]$ git push upstream master 1.0.0

>

  

이것으로 출시 담당자의 브랜치 관리는 끝이 나고, 앱을 스토어에 출시합니다. (hotfix는 없는걸로..)

  

# 활용

  

이전형상이랑 비교해서

  

커밋한적이 없으니까

  

discard하면 notepad 에서 돌려주겠지

  

오탐코드는 살릴수있는 방법이 없지 ?따로 저장 안해놔서?

  

---

  

github 잘못쓴경우 == 지울것? 확인하고 지울것

  

문법만있음 git을 그냥 메모장으로 사용함

  

# git

  

hot fix branch 딸때 pull받아서 최신 형상으러

  

Local master branch Reset 하고 다시

  

hotfix branch 삭제 안하고 남겨놓으면?

  

Initialize got flow

  

Featear release hotfix 선택가능

  

git config --add gitflow.multi-hotfix true

  

활용

notepad++로 reload안하고 반영하기

  

Push 전 저 확인

체이픽으로 가져오기

Hot fix branch 따기

  

gittea 가입해야함

  

respository 이름바꿔도 fork로 push는 가넝

  

# git history

reshper에서
git history

- 찾기? 기록?

  

# git tracking

  

feature의 feature가 아니라 여러 feature들이 있는것에서 그냥 받아오기

  

원격 저장소와 로컬저장소 1:1 매핑 시켜놓기

  

# git Fork 사용

  

## 기능

  

revert

  

reset

  

git fork에서 branch 바꾸니까 badcase 켜진거 다 사라짐

  

fork의 선 색깍들

  

push 했는지 항상 확인

  

- commit

  

# 확인할것

  

commit 하고 원격에 push 안한 local 저장소 삭제가 가능한가 데이터는 어떻게 남아있나

  

# git 실수

  

static 분석 올려서 생긴 파일 지우려다가 수정되는 내용들 더 지움

  

- feature 브랜치라서 복구 가능?

- 빌드하고 테스트 할 수 만 있으면 되지

  

# Wish 기능

  

stage 에 있는거 말고 unstaged에 있는것만 stash 하는 기ㅡㄴㅇ...

  

git hotfix
- local master,develop에 반영한 이후에

  

# commit

  

이름이 바뀌었네 새로 만들고…….기존꺼 냅둬야지

  

![Untitled](commiterror.png)

  

git branch 관리

  

C#

  

- 특수문자 경로 삭제

  

git log <filename>

git log -p <filename>

  

# reset

  

- unstage로 갔음 force push해서 추가해버림

  

# 복구

  

## 누락된 케이스나 잘못된 케이스 있는 경우

git 깨졌을때 이전 목록이랑 비교해서 눈으로 확인하기

```cpp

git remote add upstream origin

- origin https/,,,/.git

  

git fetch upstream

git rebase upstream/master

git push -f

```

  

[기능](Git%200cb8598b5ff14ff9aa5004c88f5065be/%E1%84%80%E1%85%B5%E1%84%82%E1%85%B3%E1%86%BC%203f5a6bf5b1ea4dc4831eeaf9facdb811.md)

  

# Rebase
![Untitled](rebase.png)

  

커밋이 불필요하게 여러 개로 나뉘어져 있으면 squash 진행
- 커밋 2개 합쳐야 하는 경우

  

작업 브랜치를 upstream/feature-user에 rebase함

작업 브랜치를 origin에 push

## git rebase

  

git rebase를 사용하여 커밋을 결합시키고 브랜치 기록을 수정합니다.

git rebase -i를 사용하면 기록 수정 시 표준 git rebase보다 훨씬 정밀한 제어가 가능합니다.

  

이전 또는 여러 개의 커밋을 수정하기 위해 git rebase를 사용하여 커밋 시퀀스를 새로운 기본 커밋에 결합시킬

  

rebase 도중 편집 또는 e 명령이 해당 커밋에서 rebase 재생을 일시 중지하고 git commit --amend를 사용하여 추가로 변경할 수 있도록 합니다. Git는 재생을 중단하고 다음과 같은 메시지를 표시합니다.

  

```jsx

it rebase -i HEAD~<number of commits to SHA>

git push origin <post-rebase SHA>:master

  

git push origin 복사SHA

```

  

## git reset

  

메인을 이전 커밋으로 다시 되돌릴 수 있습니다. 기록이 실수로 변경된 경우를 대비한 안전망을 제공합니다.

  

# git reflog

  

- head@1 확인

  

reflog는 변경 사항이 로컬 리포지토리에 커밋되고 리포지토리 브랜치 팁의 이동을 추적하는 경우에만 이런 안전망을 제공합니다. 추가적으로 reflog 항목에는 만료 날짜가 있습니다. reflog 항목의 기본 만료 기간은 90일입니다.

  

git reflog

  

- 브랜치 팁 또는 기타 커밋 참조에 적용되는 업데이트를 기록하기 위해 Git가 사용하는 메커니즘

  

어떠한 브랜치나 태그가 참조하지 않아도 Reflog를 사용해 커밋으로 되돌아갈 수 있습

기록을 다시 작성한 후 reflog는 이전 상태의 브랜치에 대한 정보를 포함하고 필요한 경우 그 상태로 되돌아갈 수 있습

어떠한 이유(분기 전환, 새 변경 사항에서 풀링, 기록 다시 작성 또는 단순히 새 커밋 추가)에서든 브랜치 팁이 업데이트될 때마다 새로운 항목이 reflog에 추가

  

git reflog --relative-date

  

- 상태 날짜 정보가 포함된 reflog 표시

  

[git diff](Git%200cb8598b5ff14ff9aa5004c88f5065be/git%20diff%209d7e4e9379444a23ab9db7c234ae316f.md)

  

# git reset

  

- mixed

- hard

  

git log --full-history -- A10_3_5.xml

  

- 삭제된 파일 히스토리 확인

  

git log --full-history -1 -- [file path]

  

- 파일을 삭제 한 마지막 커밋 만 보려면 -1을 추가로 사용

  

release는 마스터에서 그어야쟤

  

reset: 되돌리고 싶은 시점의 commit이력으로 돌아가는 것(시간여행)

  

# Conflict

  

feature/autosar 브랜치에는 규칙 전부 들어가 있지만 develop 브랜치에는 존재하지 않는 규칙 있음

  

develop 브랜치에서 삭제한 규칙들 존재함

  

- feature/autosar 브랜치는 브랜치가 생성된 형상만을 참조함!

- develop에서 삭제된 파일을 feature/autosar 브랜치에서 수정한뒤 develop 에 merge 해도 develop에는 삭제된 상태임

1. 삭제가 이루어진 커밋 확인

2. 파일 삭제가 이루어진 커밋을 찾아서 삭제된 파일 목록 추출!

3. feature/autosar 최신 형상에서 삭제된 파일 목록 복사해서 develop 브랜치에 수동으로 복사!

4. 그래도 없는 규칙과 템플릿 인스턴스들 feature/autosar 브랜치를 기준으로 develop 브랜치에 추가

  

conflict 발생하는 경우 직전 커밋을 기준으로 변경사항 추출

  

두브랜치에서 같은 파일을 각각 수정했을경우에만 conflic이 발생함

  

# stash 사용법

  

작업중 파일을 임시보관하는 snapshot 을 찍는 것

형상은 stash 하기 전 형상임

  

A 체크아웃 작업 stash 체크아웃 B브랜치 이동 작업 커밋 하고 local 없는 상태에서 A에다가 stash 확인해야함

  

- stash 적용할때 어떤 파일있으면 conflic 발생

- commit을 하고 amend 하는 방식이 더 안전 할수 도 있음

  

develop에서 개발

autosar 에 pull 땡겨오기

autosar 에 develop에서 개발한것 cherry pick

  

git

hotfix

  

- develop 과 master 둘다 반영해야함

- fork에서 자동으로 해줌

  

pull

  

- 하나씩 받아오는것

  

fetch 후 fast forward 하는것

  

- 순간이동

- 특정 위치로 이동 함

  

rebase

  

- merge 되었다는 전제하에

- merge 가 되어 있지 않으면 최종 merge 이후 작업한 내용은 날아감

  

cherry pick 보다 rebase 가 보기 좋음

  

git reflog

  

- head@1 확인

  

git reset --soft HEAD@{1}

  

- amend 취소되고 amend 된건 unstage 에 생김

  

cherry pick 한것 git finish 하면 이상한가 merge나 rebase 했어야하나?

  

- 고 하나만 수정할거라서...

  

master 이전에 땀

  

- hotfix 에 내용 추가하고 싶을때는... rebase가 맞았던듯

  

git은 같은 파일인거 어떻게 아는거지?

  

- 철자비교?

  

git config --add gitflow.multi-hotfix true

  

[사용기](Git%200cb8598b5ff14ff9aa5004c88f5065be/%E1%84%89%E1%85%A1%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%80%E1%85%B5%203b5150a6338c4801a3737924dfe40a74.md)

  

## 변경사항 확인하기

  

develop 사본 만들기

  

master에 병합하기

  

# 질문

  

# 공부할 내용

  

스터디 용

  

- 버전 관리(VC) 위키백과

[https://ko.wikipedia.org/wiki/버전_관리](https://ko.wikipedia.org/wiki/%EB%B2%84%EC%A0%84_%EA%B4%80%EB%A6%AC)

- 누구나 쉽게 이해할 수 있는 Git 입문

[https://backlog.com/git-tutorial/kr/](https://backlog.com/git-tutorial/kr/)

  

/입문편/Git의 기본/이력을 관리하는 저장소

[https://backlog.com/git-tutorial/kr/intro/intro1_2.html](https://backlog.com/git-tutorial/kr/intro/intro1_2.html)

  

- git--distributed-even-if-your-workflow-isnt (Pro Git Book)

[https://git-scm.com/book/en/v2](https://git-scm.com/book/en/v2)

- git--distributed-even-if-your-workflow-isnt (Pro Git Book) / ch2.2

[https://git-scm.com/book/ko/v2/Git의-기초-수정하고-저장소에-저장하기](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EC%88%98%EC%A0%95%ED%95%98%EA%B3%A0-%EC%A0%80%EC%9E%A5%EC%86%8C%EC%97%90-%EC%A0%80%EC%9E%A5%ED%95%98%EA%B8%B0)

- What does “@@ -1 +1 @@” mean in Git's diff output?

[https://stackoverflow.com/a/31615728](https://stackoverflow.com/a/31615728)

- git-diff 라인별 설명

[https://www.atlassian.com/git/tutorials/saving-changes/git-diff](https://www.atlassian.com/git/tutorials/saving-changes/git-diff)

  # 공부할 내용

스터디 용

- 버전 관리(VC) 위키백과 [](https://ko.wikipedia.org/wiki/%EB%B2%84%EC%A0%84_%EA%B4%80%EB%A6%AC)[https://ko.wikipedia.org/wiki/버전_관리](https://ko.wikipedia.org/wiki/%EB%B2%84%EC%A0%84_%EA%B4%80%EB%A6%AC)
- 누구나 쉽게 이해할 수 있는 Git 입문 [https://backlog.com/git-tutorial/kr/](https://backlog.com/git-tutorial/kr/)

/입문편/Git의 기본/이력을 관리하는 저장소 [https://backlog.com/git-tutorial/kr/intro/intro1_2.html](https://backlog.com/git-tutorial/kr/intro/intro1_2.html)

- git--distributed-even-if-your-workflow-isnt (Pro Git Book) [https://git-scm.com/book/en/v2](https://git-scm.com/book/en/v2)
- git--distributed-even-if-your-workflow-isnt (Pro Git Book) / ch2.2 [](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EC%88%98%EC%A0%95%ED%95%98%EA%B3%A0-%EC%A0%80%EC%9E%A5%EC%86%8C%EC%97%90-%EC%A0%80%EC%9E%A5%ED%95%98%EA%B8%B0)[https://git-scm.com/book/ko/v2/Git의-기초-수정하고-저장소에-저장하기](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EC%88%98%EC%A0%95%ED%95%98%EA%B3%A0-%EC%A0%80%EC%9E%A5%EC%86%8C%EC%97%90-%EC%A0%80%EC%9E%A5%ED%95%98%EA%B8%B0)
- What does “@@ -1 +1 @@” mean in Git's diff output? [https://stackoverflow.com/a/31615728](https://stackoverflow.com/a/31615728)
- git-diff 라인별 설명 [https://www.atlassian.com/git/tutorials/saving-changes/git-diff](https://www.atlassian.com/git/tutorials/saving-changes/git-diff)

github

  

gitlab

  

git
branches
commit_editmsg
config
description
head
info

# logs

  

HEAD, 각각의 브랜치 별로 작업 목록이 로그로 기록된다. gistory로 확인해보길 바란다.

  

# hooks

  

git에서 지원하는 기본적인 hook들이 정의되어 있다. .sample을 지우면 샘플이 적용되는데, 이 글에서는 각 hook에 대해서는 설명하지 않는다.

  

# HEAD

  

HEAD는 현재 로컬 저장소가 가르키고 있는 브랜치를 참조한다.

  

특정 브랜치가 아닌 특정 커밋으로 checkout하면 detach가 됐다는 메시지가 뜬 기억이 있을 것이다. 이때는 그 브랜치를 참조하는 것이 아니라, 커밋의 해시값이 HEAD에 들어가게 된다.

  

# index

  

index_gistory

  

index파일은 stage에 있는 파일들이다. 즉, git add를 진행하면 index의 파일이 수정된다. git은 index와 마지막 커밋을 비교하여 커밋할 파일이 있는지 판단한다. 또한 index와 현재 파일을 비교하여 수정된 파일이 있는지 여부도 확인한다.

  

# objects

  

objects의 구성은 실제 파일에 담긴 값들을 SHA1 해시한 값 40자 중 2자는 폴더명 38자는 파일명으로 두어 식별자로 활용한다. 해싱을 사용했을 때, 소스 코드의 일부만을 바꾸더라도 별개의 해시값이 되기 때문에, 파일 식별이 쉬워지게 된다. (추가로 SHA1 해시 처리 전, zlib으로 한번의 압축이 진행된다.)

  

## Blob

  

소스 코드, 이미지 등 다양한 파일의 데이터를 저장한다. 파일의 메타 데이터를 저장하지 않고 데이터 자체만을 저장한다. (파일명과 같은 메타데이터는 저장되지 않음) 그렇기 때문에, 동일한 소스 코드를 가진 파일이 여러 개 있더라도 하나의 blob 파일만 생성된다.

  

## Tree

  

폴더 구조를 git에서도 관리해주는 것이 tree 파일이다. Blob에는 실제 파일의 데이터들이 저장되는 것과는 다르게, tree에는 파일 식별자, 파일 데이터의 해시값, 파일의 이름이 저장된다. 폴더가 파일과 폴더로 구성되는 것처럼, tree는 blob 과 또 다른 tree로 구성된다. 파일 식별자는 100644(읽기 파일(blob)), 100755(실행 파일(blob)), 040000(디렉터리(tree)) 세 가지로만 구성된다.

  

커밋을 진행했을 때, 자동으로 파일 시스템 모드(권한 관련 설정)가 수정되는 chmod 644, chmod 755 명령어가 실행된 경험이 있을 것이다. 이는 git에서 지원하는 파일 시스템 모드가 100644, 100755 두 가지 뿐이기 때문이다.

  

위 파일을 보면, git으로 관리되고 있는 폴더는 읽기 파일 a,b,c, 실행 파일 d, 그리고 dir 폴더를 가지고 있다. a,b,c,d의 해시값이 같은 것으로 보아 파일의 내용은 모두 동일하다. (실제 네 개 모두 아무 값도 없는 empty 파일이다)

  

## Commit

  

commit_gistory

  

각각의 커밋별로 하나의 커밋 파일로 저장된다. git으로 관리되는 가장 바깥 tree의 해시값, author, commiter, 커밋 메시지의 정보가 저장이 된다.

  

parent에는 직전 커밋의 해시값이 저장되어, Linked List의 형태로 커밋들이 구성

  

# refs

  

refs의 폴더 구조는 위와 같이 구성되며, git에서 관리하는 branch들의 정보가 들어 있다. 로컬에서 작업하는 부분은 heads, 원격 저장소는 remotes 안에 관리 된다. 각 브랜치별 마지막 커밋의 해시값을 저장하고 있다.

  

# git의 명령어의 작동 이해하기

  

## git fetch

  

- 명령어는 원격저장소의 데이터를 가져옴

  

objects와 refs의 변화

  

objects: 파일의 데이터가 같은 경우를 제외한 다른 blob/tree/commit 정보들이 추가된다.

  

refs: 새로 생긴 remotes의 branch들을 추가하고, commit이 된 경우에는 각 브랜치 별로 최신 커밋으로 참조값을 수정해줘야 한다.

  

## git reset

  

git reset이 실행되면, 현재 HEAD가 가르키고 있는 브랜치의 커밋 해시값이 reset 위치의 커밋의 해시값으로 수정된다.

  

reset 하고 복원 가능?

  

- 가능

- git은 reset을 하는 그 시점에 objects의 파일을 삭제하지 않음

- 가비지 컬렉션의 방식으로 데이터가 많아졌을 때, 참조값이 없는 것의 삭제를 진행

  

git reset을 진행했을 때 ORIG_HEAD라는 파일이 생성

  

- reset 하기 전 커밋의 해시값을 따로 저장

- git reset --hard ORIG_HEAD를 통해서 reset을 복구 가능

- 직접 기존 커밋의 해시값으로 reset을 해도 마찬가지로 동작

네, Git에서 `HEAD`와 `master` 브랜치는 서로 다를 수 있습니다. 두 개념은 서로 다른 것을 나타냅니다:

---

### 1. **`HEAD`란?**
- **`HEAD`**는 현재 체크아웃된 브랜치를 가리키거나 특정 커밋을 가리킵니다.
- 일반적으로 브랜치를 체크아웃하면, `HEAD`는 그 브랜치를 가리키고 있습니다.
  - 예: `HEAD -> main` (현재 `main` 브랜치에 위치)
- 특정 커밋을 직접 체크아웃(`git checkout <commit-hash>`)하면, `HEAD`는 분리(detached) 상태가 되어 특정 커밋만 가리키게 됩니다.

---

### 2. **`master` 브랜치란?**
- **`master`**는 기본 브랜치 중 하나로, 보통 프로젝트의 주된 작업을 담고 있는 브랜치입니다.
- 하지만 요즘은 많은 프로젝트에서 기본 브랜치를 `main`으로 대체하기도 합니다.

---

### 3. **`HEAD`와 `master`가 다른 상황**
다음과 같은 경우에 `HEAD`와 `master`가 다를 수 있습니다:

#### 1) **다른 브랜치를 체크아웃한 경우**
   - 예: `git checkout feature-branch`를 수행하면 `HEAD`는 `feature-branch`를 가리키지만, `master`는 여전히 `master` 브랜치에 남아 있습니다.

#### 2) **Detached HEAD 상태**
   - 예: 특정 커밋을 체크아웃(`git checkout <commit-hash>`)하면 `HEAD`는 커밋을 가리키고, 브랜치와 연결되지 않은 상태가 됩니다.
   - 이 상태에서 커밋을 추가하면 `HEAD`는 계속 움직이지만 브랜치에는 영향을 미치지 않습니다.

#### 3) **`master`가 다른 위치에 있을 경우**
   - `master` 브랜치가 뒤처져 있거나 업데이트되지 않은 경우.
   - 예: 다른 브랜치에서 작업한 커밋들이 `master`에 병합되지 않았다면, `HEAD`가 가리키는 최신 상태와 `master`가 가리키는 커밋이 다릅니다.

---

### 4. 확인 방법
다음 명령어로 확인할 수 있습니다:

1. **`HEAD`가 가리키는 브랜치와 커밋**
   ```bash
   git log --oneline -1
   ```

2. **`master` 브랜치가 가리키는 커밋**
   ```bash
   git log master --oneline -1
   ```

3. **현재 상태 확인**
   ```bash
   git branch -v
   ```

---

### 요약
- **`HEAD`**는 현재 작업 중인 위치를 가리키는 포인터입니다.
- **`master`**는 브랜치 이름이며, 프로젝트에 따라 다를 수 있습니다.
- 두 개념은 다르며, 항상 같은 커밋을 가리키지는 않습니다.



git 
ijjeon1203  
3021idwn

`Fork` GUI 프로그램을 **Mac**에서는 잘 사용하지만, **Windows**에서는 같은 레포지토리를 열 수 없는 문제를 겪고 계시는군요. 이 문제는 여러 가지 원인으로 발생할 수 있습니다. 여기에 대해 가능한 몇 가지 원인과 해결 방법을 제시해 드리겠습니다.

### 1. **파일 경로 문제 (경로 길이 또는 경로 구분자)**
   - **Windows**와 **Mac**의 파일 시스템은 경로 구분자가 다릅니다. Mac은 기본적으로 `/` (슬래시)를 사용하고, Windows는 `\` (역슬래시)를 사용합니다.
   - 또한, Windows의 파일 시스템은 경로의 길이에 제한이 있을 수 있는데, 경로가 너무 길 경우 문제가 발생할 수 있습니다.

   **해결 방법**:
   - Windows에서 경로가 너무 길지 않도록 프로젝트의 위치를 확인해 보세요. 예를 들어, 너무 깊은 폴더 구조로 되어 있으면, 프로젝트를 `C:\`나 `D:\`와 같은 루트에 위치시켜 보세요.
   - `Git`이나 `Fork` 프로그램의 설정에서 **경로 길이 제한**을 조정할 수 있는 옵션이 있을 수 있으므로, 이를 확인해 보세요.

### 2. **Git 설정 문제**
   - **Git 설정**에 따라 Mac과 Windows에서 다르게 동작할 수 있습니다. 예를 들어, Git의 **라인 엔딩(Line Ending)** 설정이 다를 경우, 파일을 열 수 없거나 제대로 동작하지 않을 수 있습니다.
   
   **해결 방법**:
   - Git의 라인 엔딩을 `core.autocrlf` 설정을 통해 일관되게 맞추어 보세요. 이 설정은 Windows에서는 `true`로 설정되며, Mac에서는 `input`으로 설정하는 것이 좋습니다.

   ```bash
   git config --global core.autocrlf input   # Mac에서는 'input'
   git config --global core.autocrlf true    # Windows에서는 'true'
   ```

### 3. **파일 권한 문제**
   - Mac에서 작업할 때 파일에 대한 권한이나 속성이 Windows와 다를 수 있습니다. Windows에서는 파일 권한 문제가 발생할 수 있으며, 이로 인해 레포지토리가 제대로 열리지 않을 수 있습니다.

   **해결 방법**:
   - Windows에서 파일 권한을 확인하고, 필요하면 권한을 수정해 보세요. `Fork` 프로그램이 해당 파일을 읽고 쓸 수 있도록 충분한 권한이 있는지 확인합니다.

### 4. **Git 저장소의 인코딩 문제**
   - 레포지토리 내의 파일이나 폴더 이름에 **비-ASCII 문자**나 **특수 문자**가 포함되어 있을 경우, Windows에서는 해당 파일이나 폴더를 제대로 인식하지 못할 수 있습니다.
   
   **해결 방법**:
   - 가능하면 레포지토리 내의 파일과 폴더 이름을 **영어**로 변경하여 테스트해 보세요. 비-ASCII 문자로 인해 발생하는 인코딩 문제를 피할 수 있습니다.

### 5. **Fork 프로그램 버전 문제**
   - Fork 프로그램이 최신 버전이 아닐 경우, **버그**나 **호환성 문제**가 있을 수 있습니다.

   **해결 방법**:
   - Fork 프로그램을 최신 버전으로 업데이트해 보세요. 최신 버전에서 문제가 해결되었을 수 있습니다.

### 6. **Fork 프로그램 재설치**
   - Fork 프로그램 자체가 손상되었을 가능성도 있습니다. 프로그램을 완전히 삭제한 후 다시 설치하는 방법을 시도할 수 있습니다.

   **해결 방법**:
   - Fork를 **재설치**하여 문제가 해결되는지 확인해 보세요.

---

이 방법들을 하나씩 확인해 보시고, 여전히 문제가 해결되지 않는다면, 추가적인 오류 메시지나 상황을 알려주시면 더 구체적으로 도와드리겠습니다.

네, **Git Fork**라는 프로그램에 대해 알고 있습니다. **Fork**는 Git 리포지토리를 복사하여 **개인적인 작업을 할 수 있게** 해주는 도구입니다. Git에서 "fork"는 주로 **다른 사람의 프로젝트를 복제하여** 자신만의 작업 공간에서 수정하고 실험할 수 있도록 하는 기능입니다. 보통 GitHub와 같은 플랫폼에서 사용됩니다.

하지만 "Git Fork"는 보통 **GitHub의 Fork 기능**을 의미하거나, **Fork (GUI Git 클라이언트)**라는 프로그램을 말할 수도 있습니다. 이 두 가지를 구체적으로 설명해 드릴게요.

### 1. **GitHub에서의 Fork 기능**
   - **GitHub에서 Fork**는 다른 사람의 리포지토리를 내 계정으로 복사하여, **자유롭게 수정**하고 나중에 원본 리포지토리로 **변경사항을 반영**할 수 있도록 하는 기능입니다. 일반적으로 **오픈소스 프로젝트에서** 많이 사용되며, 프로젝트에 대한 기여를 쉽게 할 수 있습니다.
   
   - Fork 후, 수정 사항을 **Pull Request (PR)**로 제출하여 원본 리포지토리에 병합할 수 있습니다.

### 2. **Fork (GUI Git 클라이언트)**
   - **Fork**는 Git과 GitHub를 사용하는 개발자들을 위한 **GUI 클라이언트**입니다. 
   - Git 명령어를 몰라도 직관적인 그래픽 인터페이스를 통해 **리포지토리 관리**, **커밋**, **브랜치 관리**, **변경 사항 시각화** 등을 할 수 있게 도와줍니다.
   - Fork는 **Windows**와 **macOS**에서 사용할 수 있으며, Git을 더 쉽게 사용할 수 있도록 해줍니다.

   주요 기능:
   - **커밋 및 브랜치 관리**: Git의 커맨드를 직접 입력하지 않고도 커밋, 브랜치 생성, 병합 등을 쉽게 할 수 있습니다.
   - **시각화된 변경 사항**: 파일 간의 차이를 한눈에 볼 수 있어 변경 사항을 명확하게 파악할 수 있습니다.
   - **GitHub와의 통합**: GitHub와 연동되어 원격 리포지토리와의 상호작용도 가능합니다.

   Fork는 Git을 잘 모르는 사용자들이 GUI 환경에서 Git을 편리하게 사용할 수 있게 도와주는 도구입니다.

---

**정리하자면**, Git에서의 "fork"는 **리포지토리 복제**의 개념이며, **Fork 프로그램**은 Git을 그래픽으로 관리할 수 있는 클라이언트입니다.

**혹시 Git Fork에 대해 더 구체적인 정보가 필요하시거나 사용법에 대해 알고 싶으신가요?**


Windows에서 **Git GUI 프로그램인 Fork**를 사용할 때 **레포지토리가 열리지 않는 경우**가 발생할 수 있습니다. 이 문제는 여러 가지 원인으로 발생할 수 있으며, 각 원인에 대한 해결 방법을 아래에 제시해 드리겠습니다.

### 1. **Git 레포지토리 파일 손상**
   - Fork 프로그램에서 레포지토리를 열지 못하는 가장 일반적인 원인 중 하나는 **Git 레포지토리의 손상**입니다. 레포지토리 내부의 `.git` 폴더가 손상되었을 경우, Git과 Fork가 레포지토리를 정상적으로 읽지 못할 수 있습니다.

   **해결 방법**:
   - 레포지토리를 Git 커맨드라인을 통해 확인해 보세요. 터미널에서 해당 레포지토리로 이동한 뒤, `git status`를 실행하여 레포지토리 상태를 점검할 수 있습니다.
   - 레포지토리에서 문제가 발견되면, **`git fsck`** 명령어로 레포지토리의 무결성을 확인하거나, **`git reset --hard`**로 상태를 복원할 수 있습니다.

### 2. **레포지토리 경로 문제**
   - Windows에서는 **파일 경로**에 제한이 있을 수 있습니다. 경로가 너무 길거나, 경로에 특수 문자가 포함되어 있으면 레포지토리가 열리지 않을 수 있습니다. 특히, Windows의 **파일 경로 길이 제한**(기본적으로 260자 제한)이 문제를 일으킬 수 있습니다.

   **해결 방법**:
   - 레포지토리가 너무 긴 경로에 있는지 확인하고, 경로가 길지 않도록 레포지토리를 **루트 디렉토리**(예: `C:\my-repo`)에 옮겨 보세요.
   - Windows에서 경로 길이 제한을 해제하려면, `regedit`에서 `LongPathsEnabled`를 활성화할 수 있습니다:
     1. **`regedit`**를 열고 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem` 경로로 이동합니다.
     2. `LongPathsEnabled` 값을 `1`로 변경합니다.
     3. 시스템을 재부팅합니다.

### 3. **파일 권한 문제**
   - Windows에서 **파일 권한**이 제대로 설정되지 않으면 Git이나 Fork 프로그램이 해당 레포지토리에 접근할 수 없습니다. 이 경우, 레포지토리를 열려고 할 때 **접근 오류**가 발생할 수 있습니다.

   **해결 방법**:
   - 레포지토리 폴더와 `.git` 디렉토리의 **파일 권한**을 확인하고, Fork 프로그램이 해당 디렉토리에 접근할 수 있도록 **읽기/쓰기 권한**을 부여합니다.
   - `Properties` → `Security`에서 권한을 수정할 수 있습니다.

### 4. **인코딩 문제**
   - 레포지토리 내에 **비-ASCII 문자**가 포함된 파일이나 폴더가 있을 경우, Windows에서 문제가 발생할 수 있습니다. 특히, 파일 시스템과 Git의 인코딩 방식이 일치하지 않으면 레포지토리가 열리지 않는 경우가 발생할 수 있습니다.

   **해결 방법**:
   - 레포지토리 내에서 **비-ASCII 문자**가 포함된 파일명이나 폴더명이 있는지 확인하고, 가능하면 **영어 문자**로 변경해 보세요.
   - `core.quotepath`를 `false`로 설정하여 Git이 경로의 비-ASCII 문자를 처리할 수 있도록 할 수 있습니다:
     ```bash
     git config --global core.quotepath false
     ```

### 5. **Fork 프로그램의 버그 또는 호환성 문제**
   - Fork GUI 자체의 **버그**나 **호환성 문제**가 있을 수 있습니다. 특히, 프로그램이 최신 버전이 아니거나 시스템과 잘 호환되지 않는 경우 문제가 발생할 수 있습니다.

   **해결 방법**:
   - Fork 프로그램을 **최신 버전으로 업데이트**하거나, **재설치**하여 문제가 해결되는지 확인해 보세요.
   - 공식 [Fork Git 클라이언트](https://git-fork.com/) 사이트에서 최신 버전을 다운로드하여 설치합니다.

### 6. **Fork에서 Git 설정 확인**
   - Fork에서 사용하는 **Git 설정**이 Windows 환경에 맞지 않으면, 레포지토리가 제대로 열리지 않을 수 있습니다. 예를 들어, **Git의 경로**가 올바르게 설정되지 않았거나, Git 설정 파일이 손상된 경우가 있을 수 있습니다.

   **해결 방법**:
   - **Git 설정**을 확인하고, Fork에서 사용하는 Git 경로가 올바른지 점검합니다. Fork의 설정에서 **Git Path**가 제대로 설정되어 있는지 확인하세요.
   - Git 명령어가 정상적으로 작동하는지 확인하려면, `git --version` 명령어로 Git이 올바르게 설치되어 있는지 확인할 수 있습니다.

---

이 문제는 다양한 원인으로 발생할 수 있기 때문에, 각 해결 방법을 하나씩 시도하여 문제를 해결해 보세요. 만약 문제가 계속된다면, Fork에서 제공하는 **로그**나 **오류 메시지**를 통해 더 구체적인 원인을 파악할 수 있을 것입니다.

혹시 다른 세부적인 정보나 추가적인 오류 메시지가 있으면 알려 주세요. 더 구체적으로 도와드릴 수 있습니다!


`git fsck` 명령을 실행했을 때 발생한 **bad sha1 file** 오류 메시지는 Git 객체가 손상되었음을 의미합니다. 손상된 객체들은 `.git/objects/` 디렉토리 내에서 발생하며, 이로 인해 Git 레포지토리를 제대로 읽거나 쓰는 데 문제가 생길 수 있습니다. 특히, `.git/objects/` 디렉토리 안에 있는 파일들은 Git의 커밋, 트리, 블롭 등의 객체를 저장하는 중요한 파일들입니다.

### 손상된 객체 문제 해결 방법

여기서 제시된 해결 방법들은 레포지토리를 복구하거나 손상된 객체를 처리하는 데 도움이 될 수 있습니다.

#### 1. **`git fsck --full`로 더 자세한 오류 확인**
   `git fsck` 명령은 레포지토리에서 손상된 객체를 찾는 데 사용됩니다. 이 오류 메시지에서 손상된 객체가 SHA1 해시로 표시됩니다. **`--full`** 옵션을 사용하면 더 많은 정보를 얻을 수 있습니다.

   ```bash
   git fsck --full
   ```

   이를 통해 손상된 객체들이 무엇인지 더 정확히 파악할 수 있습니다.

#### 2. **손상된 객체 복구하기**
   `git fsck`로 확인된 손상된 객체는 일반적으로 Git에서 해당 객체를 **복구할 수 없게 되거나** 사용할 수 없는 상태로 나타납니다. 이 경우, 손상된 객체를 **다시 덮어쓸 수 있는 방법**은 없습니다. 하지만, 다음 방법들을 시도할 수 있습니다:

   - **`git reflog` 사용**: Git에서는 작업 히스토리를 추적하기 때문에 이전 상태로 되돌릴 수 있습니다.
     ```bash
     git reflog
     ```
     이 명령어는 이전 커밋이나 상태로 돌아갈 수 있는 히스토리를 보여줍니다. 손상되기 전의 커밋으로 복원할 수 있을 수 있습니다.
   
   - **`git checkout`으로 복구**: 손상된 객체가 특정 파일이나 커밋에만 영향을 미친다면, 해당 커밋을 체크아웃하여 **복구**할 수 있습니다.
     ```bash
     git checkout <commit-hash> -- <file-path>
     ```

#### 3. **원격 저장소에서 복제하기**
   손상된 객체를 복구하는 가장 간단한 방법은 원격 저장소에서 레포지토리를 다시 **복제(clone)** 하는 것입니다. 만약 로컬에서만 손상이 발생했다면, 원격 저장소에서 레포지토리를 새로 복제할 수 있습니다.
   
   ```bash
   git clone <repository-url>
   ```

   이 방법은 손상된 객체가 로컬에서만 발생한 경우 유효합니다. 만약 원격 저장소에서 문제가 발생했다면, 서버의 백업을 통해 복구해야 할 수도 있습니다.

#### 4. **손상된 객체 수동 삭제**
   **만약 손상된 객체 파일이 많이 있다면**, 이를 수동으로 삭제하고 다시 복원할 수 있는 경우가 있습니다.

   - 손상된 객체는 `.git/objects/2a/` 디렉토리에 존재합니다.
   - 해당 파일을 삭제한 후, 원격 저장소에서 **`git fetch`** 명령어를 실행하여 해당 객체를 다시 가져올 수 있습니다.
     ```bash
     rm .git/objects/2a/._43a131f8a3d8d8fca03b58ae6eae6df506e734
     rm .git/objects/2a/._0c6ad01065ae97b49aa2f6bfe9e489ba18ec44
     rm .git/objects/2a/._c91c8a34fec09de0626bcb9ef3c79e799e750f
     rm .git/objects/2a/._a73a9c8f3ec4bab36c653fe7594740e6f68e6c
     rm .git/objects/2a/._a48cf034b878b338be4bbeead7a62482908009
     ```

   - 그 후, `git fetch`로 원격 저장소에서 최신 객체를 다시 가져올 수 있습니다:
     ```bash
     git fetch --all
     ```

#### 5. **`git gc` (Garbage Collection) 실행**
   Git은 주기적으로 **garbage collection**을 통해 불필요한 객체를 정리합니다. 손상된 객체들이 정리되지 않았을 수 있으므로 `git gc` 명령어를 실행하여 Git 내부의 객체들을 정리해 보세요.

   ```bash
   git gc --prune=now
   ```

   `git gc`는 Git의 내부 데이터를 최적화하는 명령어로, 불필요한 파일들을 정리합니다.

---

### 결론

`bad sha1 file` 오류는 Git 객체가 손상되었음을 나타냅니다. 이 문제를 해결하려면 원격 저장소에서 레포지토리를 다시 복제하거나, 손상된 객체를 복구하기 위한 방법을 시도할 수 있습니다. `git reflog`나 `git checkout` 등을 사용하여 손상되기 전 상태로 돌아가거나, `git fetch`로 원격 저장소에서 최신 객체를 가져올 수도 있습니다.

만약 문제가 계속 발생한다면, 추가적으로 레포지토리 백업을 확인하거나, 원격 저장소에서의 문제를 점검할 필요가 있을 수 있습니다.

`git gc --prune=now` 명령어는 Git에서 **쓰이지 않는 객체**를 정리하고 **레포지토리 크기**를 최적화하는 데 사용되는 명령어입니다. 구체적으로 이 명령어는 **Git의 가비지 컬렉션(Garbage Collection)**을 실행하고, 일정 기간 이상 사용되지 않은 객체들을 **즉시 삭제**하는 작업을 수행합니다.

### `git gc` (Garbage Collection)란?

Git에서 **Garbage Collection (GC)**은 사용되지 않거나 불필요한 데이터를 정리하여 리포지토리의 크기를 최적화하는 작업을 말합니다. Git은 커밋, 브랜치, 태그, 파일, 메타데이터 등을 **객체(Objects)**라는 단위로 저장합니다. 시간이 지나면 사용되지 않는 객체들이 쌓이게 되며, 이는 디스크 공간을 낭비할 수 있습니다.

`git gc`는 이러한 객체들을 정리하여, **리포지토리의 크기를 줄이고 성능을 향상**시킵니다. 예를 들어, 삭제된 브랜치에 대한 데이터나 오래된 커밋, 병합되지 않은 변경사항 등이 남아 있을 수 있습니다.

### `--prune=now` 옵션

`--prune=now` 옵션은 **쓰이지 않는 객체를 즉시 삭제**하라는 명령입니다. 기본적으로 `git gc`는 쓰이지 않는 객체를 일정 기간(보통 2주) 동안 보관한 후 삭제합니다. 그러나 `--prune=now`를 사용하면, **즉시 모든 쓰이지 않는 객체들을 삭제**합니다. 즉, **기한을 두지 않고 바로 정리**하는 방식입니다.

- `--prune` 옵션은 Git이 "어느 정도 시간이 지난 후에" 삭제할 객체를 지정하는 데 사용됩니다. 예를 들어, `--prune=2.weeks.ago`는 2주 이상 된 객체를 삭제하라는 뜻입니다.
- `--prune=now`는 **"지금 바로 삭제"**를 의미합니다. 즉, Git이 객체를 수집하고 나서 **사용되지 않는 모든 객체**를 즉시 삭제하게 됩니다.

### `git gc --prune=now`의 주요 동작

1. **불필요한 객체 삭제**:
   - Git은 커밋, 브랜치, 태그, 파일, 객체 등이 **쓰이지 않거나 더 이상 참조되지 않는 경우** 해당 객체를 삭제합니다. 예를 들어, 이미 삭제된 브랜치에서의 커밋이나, 이전에 병합된 커밋들은 더 이상 필요하지 않다면 삭제됩니다.

2. **객체 압축**:
   - Git은 객체들을 저장할 때 **단일 파일로 압축**하는 방식으로 저장합니다. `git gc`는 이 작업을 수행하여 리포지토리의 크기를 줄이고 성능을 향상시킵니다.
   
3. **Repack**:
   - Git은 객체를 저장할 때 **pack file**이라는 파일에 압축해서 저장합니다. `git gc`는 여러 개의 작은 객체들을 하나의 큰 객체로 합쳐서 **pack**합니다. 이렇게 하면 Git이 효율적으로 디스크 공간을 사용할 수 있습니다.

4. **Index 최적화**:
   - Git은 **인덱스 파일**을 사용하여 빠르게 파일 변경 사항을 추적합니다. `git gc`는 이 인덱스를 최적화하여 성능을 향상시킬 수 있습니다.

### 예시

1. **일반적인 `git gc` 실행**:
   ```bash
   git gc
   ```
   이 명령어는 Git이 자동으로 가비지 컬렉션을 실행하고, 2주 이상 사용되지 않은 객체들을 삭제합니다.

2. **`--prune=now` 옵션을 사용한 `git gc` 실행**:
   ```bash
   git gc --prune=now
   ```
   이 명령어는 **모든 쓰이지 않는 객체를 즉시 삭제**합니다. 즉, 2주 이상의 기간이 지났든 아니든 관계없이 **즉시 삭제**됩니다.

### 주의 사항

- `git gc --prune=now`를 실행하면 **사용되지 않는 모든 객체가 즉시 삭제되므로**, 필요하지 않은 데이터도 함께 삭제될 수 있습니다. 예를 들어, 아직 병합되지 않은 브랜치에서의 커밋 등이 삭제될 수 있습니다. 따라서 중요한 데이터를 삭제하지 않도록 주의해야 합니다.
- **백업**을 하고 `git gc` 명령어를 실행하는 것이 좋습니다. 특히 큰 프로젝트나 협업 환경에서는 **팀원들과 공유되는 리포지토리**의 경우 주의 깊게 사용해야 합니다.

### 결론

- **`git gc`**는 Git 리포지토리에서 불필요한 객체를 정리하고 크기를 최적화하는 유용한 명령어입니다.
- **`--prune=now`** 옵션을 사용하면 즉시 모든 쓰이지 않는 객체를 삭제하여 레포지토리 크기를 빠르게 줄일 수 있지만, 데이터를 삭제할 때 신중해야 합니다.

이 명령어를 주기적으로 실행하여 리포지토리의 성능과 크기를 관리할 수 있습니다.

`git gc --prune=now` 명령어는 **사용되지 않는 객체**나 **쓰이지 않는 커밋** 등을 삭제하는 작업을 수행합니다. 하지만 **이전 커밋들이 삭제되기 위한 조건**이 있습니다. 일반적으로 `git gc --prune=now` 명령어 자체가 **커밋을 직접적으로 삭제**하지는 않습니다. 대신, **쓰이지 않거나 더 이상 참조되지 않는 객체**들을 정리하는 방식으로 동작합니다.

### 커밋이 삭제되는 경우

Git에서 커밋이 삭제되는 경우는 **해당 커밋이 더 이상 참조되지 않거나 사용되지 않을 때**입니다. 예를 들어, 다음과 같은 경우들입니다:

1. **삭제된 브랜치의 커밋**:
   - 브랜치가 삭제된 후, 그 브랜치에서 참조하는 커밋이 더 이상 다른 브랜치나 태그에서 참조되지 않으면, 그 커밋은 **"고아 커밋"(dangling commit)**으로 간주됩니다. `git gc --prune=now` 명령어는 이러한 고아 커밋을 정리합니다.

2. **`git reset --hard`로 이전 커밋으로 되돌렸을 경우**:
   - `git reset --hard` 명령어로 특정 커밋으로 되돌리면, 그 이후의 커밋들은 더 이상 현재 브랜치에서 참조되지 않게 됩니다. 그 커밋들도 **쓰이지 않는 커밋**으로 간주되어 `git gc --prune=now` 명령어가 실행될 때 삭제될 수 있습니다.

3. **`git rebase`로 커밋을 재정렬한 경우**:
   - `git rebase` 명령어를 사용하여 커밋을 재정렬하고, 이전 커밋들이 더 이상 참조되지 않으면, 해당 커밋들이 삭제될 수 있습니다.

4. **`git filter-branch` 또는 `git filter-repo`로 커밋을 제거한 경우**:
   - `git filter-branch`나 `git filter-repo` 명령어로 특정 커밋을 아예 제거한 경우, 그 커밋들도 더 이상 참조되지 않으므로 가비지 컬렉션 과정에서 삭제될 수 있습니다.

### `git gc --prune=now` 명령어가 삭제하는 것

- **삭제되지 않는 커밋**: `git gc --prune=now`는 **현재 사용 중인 커밋**이나 **참조되고 있는 커밋**은 삭제하지 않습니다. 예를 들어, 현재 브랜치에서 참조하는 커밋들은 안전하게 남습니다.
- **삭제되는 커밋**: `git gc --prune=now`는 **더 이상 참조되지 않는 커밋**만 삭제합니다. 예를 들어, 이미 병합된 브랜치에서의 커밋이 다른 브랜치에서 참조되지 않으면, 그 커밋은 삭제될 수 있습니다.

### `git gc`가 커밋을 삭제하는 과정

1. **Git은 내부적으로 "리치 객체"(reachable objects)와 "고아 객체"(dangling objects)를 구분합니다**:
   - **리치 객체**: 현재 브랜치나 태그, 기타 참조(예: `HEAD`, `refs/heads/`)에서 참조하는 커밋.
   - **고아 객체**: 아무런 참조도 받지 않는 커밋. 예를 들어, 삭제된 브랜치의 커밋이나 `git reset`으로 이동한 커밋 등이 여기에 포함됩니다.

2. **가비지 컬렉션 실행**:
   - `git gc`는 **고아 객체**를 찾아서 삭제합니다. 즉, 더 이상 참조되지 않는 커밋, 브랜치, 태그 등과 관련된 객체들을 삭제합니다.

### 커밋이 삭제되지 않게 하려면?

만약 커밋이 삭제되지 않도록 보장하려면, 해당 커밋을 다른 브랜치나 태그에서 참조하게 만들면 됩니다. 예를 들어:

- 해당 커밋을 **다른 브랜치**로 체크아웃하거나
- 해당 커밋을 **태그**로 지정하여 참조를 유지할 수 있습니다.

### 결론

`git gc --prune=now`는 **쓰이지 않는 커밋**이나 **참조되지 않는 객체**를 삭제합니다. 그러나 **현재 브랜치에서 참조되는 커밋은 삭제되지 않습니다**. 커밋이 삭제되는 경우는 **현재 참조되지 않는 상태일 때**로, 예를 들어 **삭제된 브랜치의 커밋**이나 **`git reset`으로 돌아간 커밋** 등이 해당됩니다. **안전하게 커밋을 보존하려면, 해당 커밋을 다른 브랜치나 태그에서 참조**하는 방법을 사용하는 것이 좋습니다.

Git 레포지토리를 정리하는 방법은 여러 가지가 있으며, 이를 통해 **디스크 공간을 절약하고 성능을 최적화**할 수 있습니다. 여기서는 Git 레포지토리를 정리하고 최적화하는 몇 가지 방법을 소개합니다.

### 1. **`git gc` (Garbage Collection)**

앞서 설명한 것처럼, **`git gc` (Garbage Collection)**는 사용되지 않는 객체들을 정리하고 Git 리포지토리의 크기를 최적화하는 데 사용됩니다. 

- **`git gc`**: 기본적으로 2주 이상 사용되지 않은 객체들을 정리합니다.
  ```bash
  git gc
  ```

- **`git gc --prune=now`**: 즉시 사용되지 않는 객체들을 삭제하여 리포지토리 크기를 줄입니다.
  ```bash
  git gc --prune=now
  ```

### 2. **`git prune`**

`git prune`은 **쓰이지 않는 객체**를 수동으로 삭제하는 명령어입니다. 이는 `git gc`와 비슷하지만, **가비지 컬렉션**을 트리거하지 않고 직접적으로 **사용되지 않는 객체들만 삭제**합니다.

```bash
git prune
```

- `git prune`은 **사용되지 않거나 더 이상 참조되지 않는 객체들만** 삭제합니다. 예를 들어, 삭제된 브랜치의 커밋, `git reset` 후 이전 커밋 등.

**주의**: `git prune`을 실행하기 전에 **`git gc`를 먼저 실행**하는 것이 좋습니다. `git prune`은 로컬에서만 영향을 미치므로 **원격 저장소와 동기화되지 않은 상태에서 사용하지 않도록 주의**해야 합니다.

### 3. **`git clean`**

`git clean` 명령어는 **작업 디렉토리**에서 **추적되지 않는 파일**을 삭제하는 데 사용됩니다. 예를 들어, `.gitignore`에 포함된 파일이나 Git에 추가되지 않은 파일들을 정리할 수 있습니다.

- **추적되지 않는 파일만 삭제**:
  ```bash
  git clean -n
  ```
  `-n` 옵션은 삭제될 파일 목록을 **리스트**로 보여줍니다.

- **실제로 파일 삭제**:
  ```bash
  git clean -f
  ```

- **디렉토리도 포함하여 삭제**:
  ```bash
  git clean -fd
  ```

**주의**: 이 명령어는 **삭제된 파일을 복구할 수 없으므로 주의**해서 사용해야 합니다. 파일이 실제로 삭제되기 전에 `git clean -n`을 사용하여 삭제 목록을 확인하는 것이 좋습니다.

### 4. **`git reflog expire`**

`git reflog expire` 명령어는 **reflog**에 있는 오래된 기록들을 삭제합니다. Git에서는 브랜치나 HEAD 포인터가 변경될 때마다 **reflog**에 기록을 남기는데, 오래된 reflog 기록을 정리하는 데 사용됩니다.

- **이전에 사용된 HEAD 참조 삭제**:
  ```bash
  git reflog expire --expire=90.days --all
  ```
  위 명령어는 **90일 이상된 reflog 기록**을 삭제합니다.

- **모든 reflog 삭제**:
  ```bash
  git reflog expire --expire=now --all
  ```

**주의**: `git reflog`는 중요한 참조 기록이므로, 기록을 삭제하기 전에 필요한 정보를 백업하는 것이 좋습니다.

### 5. **`git filter-repo` (대규모 리포지토리 정리)**

`git filter-repo`는 **큰 Git 리포지토리에서** 불필요한 커밋이나 파일을 제거할 때 사용하는 도구입니다. 이 도구를 사용하면 레포지토리에서 **민감한 정보나 큰 파일**을 제거할 수 있습니다.

- 예를 들어, 커밋 내에서 특정 파일을 제거하거나, 특정 파일 형식을 제거하는 등의 작업을 할 수 있습니다.

```bash
git filter-repo --path <파일 또는 디렉토리 경로> --invert-paths
```

### 6. **큰 파일 삭제 (`git filter-branch`와 BFG Repo-Cleaner)**

Git 리포지토리에서 **큰 파일**이나 **불필요한 파일**을 제거할 수 있는 방법입니다. 특히 민감한 정보를 Git에 실수로 커밋했을 때 유용합니다.

- **BFG Repo-Cleaner**: 대규모 리포지토리에서 큰 파일이나 민감한 정보를 쉽게 제거할 수 있는 도구입니다. `git filter-branch`보다 훨씬 빠르고 효율적입니다.
  - [BFG Repo-Cleaner 사용법](https://rtyley.github.io/bfg-repo-cleaner/)

- **`git filter-branch`**: Git에서 오래된 커밋이나 파일을 제거할 수 있습니다. 하지만 이 명령은 속도가 느리고 복잡할 수 있기 때문에, **BFG Repo-Cleaner**를 사용하는 것이 더 효율적입니다.

```bash
git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch <파일 경로>' --prune-empty --tag-name-filter cat -- --all
```

### 7. **브랜치 정리**

Git에서는 **사용되지 않는 브랜치**가 계속 남아 있을 수 있습니다. 오래된 브랜치나 병합된 브랜치는 정리하는 것이 좋습니다.

- **로컬에서 삭제된 브랜치 확인**:
  ```bash
  git branch --merged
  ```
  이 명령어는 현재 브랜치와 **병합된** 브랜치를 표시합니다. 병합된 브랜치는 삭제할 수 있습니다.

- **로컬 브랜치 삭제**:
  ```bash
  git branch -d <브랜치 이름>
  ```

- **원격 브랜치 삭제**:
  ```bash
  git push origin --delete <브랜치 이름>
  ```

### 8. **원격 저장소 정리 (GitHub, GitLab 등)**

- **대용량 파일이 포함된 커밋 삭제**: 원격 저장소에서 불필요한 대용량 파일이나 민감한 정보를 제거하는 데 `git filter-repo`나 **BFG Repo-Cleaner**를 사용합니다.
- **원격 저장소에서 태그 삭제**: 사용하지 않는 원격 태그를 삭제하려면:
  ```bash
  git push origin --delete <태그 이름>
  ```

### 결론

Git 레포지토리를 정리하는 방법은 여러 가지가 있습니다. 주요 방법은 **`git gc`**로 불필요한 객체를 정리하거나, **`git clean`**으로 작업 디렉토리에서 추적되지 않는 파일을 삭제하는 것입니다. 또한, **`git reflog expire`**를 통해 오래된 기록을 삭제하거나, **BFG Repo-Cleaner**를 사용하여 대규모 리포지토리에서 불필요한 파일을 제거하는 방법도 있습니다. 이들을 적절하게 조합하여 리포지토리의 크기를 최적화하고 성능을 향상시킬 수 있습니다.

`fatal: packed object <sha1> is corrupt` 오류 메시지는 Git 레포지토리에서 **패킹된 객체**가 손상되었음을 의미합니다. 이 문제는 다양한 이유로 발생할 수 있으며, **파일 시스템 문제**, **불완전한 Git 작업**, **디스크 오류** 등이 원인일 수 있습니다.

### 문제 해결을 위한 단계별 접근 방법

#### 1. **손상된 객체 확인 및 복구 시도**
   먼저, Git은 손상된 객체를 자동으로 복구할 수 없기 때문에, 이를 복구하려면 몇 가지 수동적인 방법을 시도해야 합니다.

   1. **레포지토리의 손상된 객체 삭제**
      손상된 객체를 수동으로 삭제한 후, `git repack`을 다시 시도할 수 있습니다. 손상된 객체는 `.git/objects/pack/` 디렉토리 내에 저장되므로, 이를 삭제하고 다시 패킹을 시도합니다.
   
      ```bash
      rm .git/objects/pack/pack-f12757a76af860f3aac79923fd8b0a2159d571fe.pack
      rm .git/objects/pack/pack-f12757a76af860f3aac79923fd8b0a2159d571fe.idx
      ```
   
      그 후, **repack** 명령어를 다시 실행해 보세요.
   
      ```bash
      git repack -a -f -d
      ```

   2. **패킹 객체 다시 생성**
      `git gc` (Garbage Collection)을 실행하면 **패킹 객체를 새로 생성**하고, 필요 없는 객체들을 삭제합니다. 이 명령어는 레포지토리의 최적화를 돕고 손상된 패킹 객체를 새로 생성합니다.
   
      ```bash
      git gc --aggressive --prune=now
      ```

#### 2. **백업 및 복원**
   손상된 Git 객체를 복구할 수 없는 경우, **백업을 사용하여 복원**하는 방법도 고려해야 합니다. 예를 들어, 다른 복사본이 있는 경우 해당 레포지토리를 복원하는 방법입니다. 

   - 원격 저장소에 변경사항이 푸시되었을 경우, 원격 저장소에서 복제하여 **로컬에서 복구**할 수 있습니다.
   
     ```bash
     git clone <원격 저장소 URL>
     ```

#### 3. **`git fsck`로 손상된 객체 확인**
   `git fsck`는 Git 저장소의 무결성을 검사하는 명령어로, 손상된 객체를 찾아내고 문제를 진단하는 데 유용합니다.

   ```bash
   git fsck --full
   ```

   이 명령어는 Git 리포지토리 내의 **모든 객체와 참조**를 검사하고 **손상된 객체**나 **고아 객체**를 찾아냅니다. 이를 통해 손상된 객체를 정확히 파악할 수 있습니다.

#### 4. **기타 방법**
   1. **새로운 레포지토리로 초기화**:
      손상된 객체가 복구되지 않는 경우, 새로운 Git 레포지토리로 작업을 복사하는 방법도 있습니다.
   
      ```bash
      git clone <원격 저장소 URL> new-repository
      cd new-repository
      ```
   
      새로운 레포지토리에서 필요한 작업을 진행하고, 손상된 레포지토리의 작업을 새로운 레포지토리로 **병합**하거나 **복사**할 수 있습니다.

   2. **디스크 오류 확인**:
      Git 객체 손상이 디스크 오류에 의한 것이라면 **디스크 검사 도구**를 사용하여 문제를 해결해야 할 수도 있습니다. 예를 들어, `chkdsk`(Windows) 또는 `fsck`(Linux) 명령어를 사용하여 디스크 오류를 검사하고 수정할 수 있습니다.

#### 5. **원격 저장소와 동기화**
   원격 저장소와 동기화되지 않은 손상된 로컬 레포지토리를 수정하는 경우, **원격 저장소와 동기화**하고 **새로운 브랜치를 만들거나 푸시**할 수 있습니다. 원격 저장소에 푸시되지 않은 작업이 많다면, 이를 원격에 푸시한 후, **원격 저장소에서 새로운 복제본을 내려받아** 작업을 계속할 수 있습니다.

   - 원격 저장소에서 작업을 푸시한 후, **로컬에서 다시 클론**할 수 있습니다.
     ```bash
     git clone <원격 저장소 URL>
     ```

---

### 결론

`fatal: packed object is corrupt` 오류는 레포지토리의 **패킹된 객체가 손상되었을 때** 발생합니다. 이 문제를 해결하기 위해서는 손상된 객체를 삭제하거나 `git gc` 명령어를 통해 리포지토리를 재패킹하거나, **원격 저장소와 동기화하여 로컬 작업을 복구**하는 방법을 시도할 수 있습니다. 만약 위 방법들이 효과가 없다면, **원격 저장소에서 복제**하여 새로운 복사본을 만들거나 **백업을 사용하여 복구**하는 방법도 고려해야 합니다.

`fatal: packed object <sha1> is corrupt` 오류는 Git 레포지토리에서 **패킹된 객체**가 손상되었음을 나타냅니다. 이 오류는 일반적으로 Git 저장소의 내부 파일 시스템 문제나 불완전한 작업으로 인해 발생할 수 있습니다. 또한 `error: bad object header`는 객체 헤더가 손상되었음을 나타내며, 이는 Git 저장소의 일부 객체가 손상된 상태임을 알립니다.

이 문제를 해결하기 위해 여러 가지 방법을 시도할 수 있습니다:

### 1. **손상된 객체 파일 삭제 후 재패킹**

손상된 객체 파일을 삭제한 후 Git을 재패킹하여 문제를 해결할 수 있습니다. 손상된 파일을 직접 삭제하고 `git repack`을 다시 실행해 보세요.

1. **손상된 패킹 객체 삭제**:
   손상된 객체가 `pack-f12757a76af860f3aac79923fd8b0a2159d571fe.pack` 파일에 있다고 명시되어 있으므로 해당 파일을 삭제합니다.

   ```bash
   rm .git/objects/pack/pack-f12757a76af860f3aac79923fd8b0a2159d571fe.pack
   rm .git/objects/pack/pack-f12757a76af860f3aac79923fd8b0a2159d571fe.idx
   ```

2. **재패킹**:
   `git repack` 명령어를 실행하여 패킹된 객체를 다시 정리하고 최적화합니다.

   ```bash
   git repack -a -f -d
   ```

3. **가비지 컬렉션 실행**:
   `git gc` 명령어를 실행하여 사용되지 않는 객체를 정리하고 Git 레포지토리의 최적화를 진행할 수 있습니다.

   ```bash
   git gc --aggressive --prune=now
   ```

### 2. **`git fsck`로 손상된 객체 확인**

`git fsck`는 Git 저장소의 무결성을 검사하고 손상된 객체를 식별하는 데 유용합니다. 손상된 객체가 있는지 확인하려면 `git fsck`를 실행하세요.

```bash
git fsck --full
```

이 명령어는 모든 객체와 참조를 검사하고 **손상된 객체**를 식별합니다. 손상된 객체를 삭제하거나 수정하는 방법을 파악하는 데 유용합니다.

### 3. **원격 저장소와 동기화**

손상된 로컬 레포지토리를 수정하는 데 실패한 경우, 원격 저장소와 동기화하여 문제를 해결할 수 있습니다. 원격 저장소에서 작업을 푸시한 경우, **원격 저장소에서 새로 복제**하여 손상된 데이터를 복구할 수 있습니다.

1. **원격 저장소에서 복제**:
   원격 저장소에서 새로 클론하여 문제를 해결합니다.

   ```bash
   git clone <원격 저장소 URL>
   ```

2. **원격 저장소 푸시**:
   만약 로컬에서 변경된 내용이 있다면, 새로 클론한 리포지토리에 **변경 사항을 푸시**할 수 있습니다.

### 4. **손상된 커밋 복구** (백업 활용)

만약 `git fsck`로 손상된 커밋이나 객체를 찾았다면, 해당 커밋을 복구하거나 백업을 사용하여 복원할 수 있습니다. 예를 들어, GitHub와 같은 원격 저장소에서 이전 커밋으로 돌아가거나 복구할 수 있습니다.

### 5. **BFG Repo-Cleaner 또는 `git filter-repo` 사용**

만약 손상된 객체가 대용량 파일이나 민감한 정보를 포함하고 있다면, **BFG Repo-Cleaner** 또는 **`git filter-repo`**를 사용하여 레포지토리를 정리할 수 있습니다. 이는 원격 저장소에서 큰 파일이나 민감한 데이터를 삭제하는 데 유용합니다.

### 6. **디스크 오류 확인**

손상된 Git 객체가 **디스크 오류**로 인해 발생할 수 있습니다. 디스크 오류를 점검하고 복구하려면 아래와 같은 도구를 사용할 수 있습니다:

- **Windows**: `chkdsk` 명령어로 디스크 오류를 검사하고 수정할 수 있습니다.
- **Linux**: `fsck` 명령어를 사용하여 파일 시스템의 오류를 검사하고 수정할 수 있습니다.

### 결론

`fatal: packed object is corrupt` 오류는 Git 저장소에서 **패킹된 객체가 손상되었을 때** 발생합니다. 이 문제를 해결하려면 손상된 객체를 삭제하거나 `git repack`과 `git gc` 명령어를 통해 레포지토리를 재정리해야 합니다. 또한, 손상된 데이터를 복구하거나 원격 저장소와 동기화하여 문제를 해결할 수 있습니다. 만약 위 방법들이 실패한다면, **원격 저장소에서 새로 클론하거나 백업을 사용하는** 방법을 고려해야 합니다.



# git 공부 
Stage - commit/local - push,pull

pull remote에 local을 sync하는것

stage의 내용 보여주고 싶은것 

gitk


visual code vs atom 


https://jobc.tistory.com/177


init 을 local 에서 

서버에서 init 
- read me 파일 없으면 clone 불가능 


20181130 

# git 
닌자커밋 
pr 안하고 마스터에 바로 

centralize

- merge권한 주고 니가 다 날려 
	- 작은프로젝트 빨리 할때는 이 방식이 좋음

fork - fork 
- 조장이 fork 


Git 도구- 대화형 명령

스크립트 통해 커밋할 파일 고르고 수정된 파일의 일부분만 커밋 할수도 있음
스크립트는 수정하는 파일이 매우 많아서 통째로 커밋하기 어려울 때 이슈별로 나눠 커밋하기 좋음 


git pull한뒤에 프로젝트를 새로 로드해서 새로운 파일을 추가해야함
- 파일하나만 새로 추가
- 전체 다 refresh 하고 추가 (시도 안해봄)
