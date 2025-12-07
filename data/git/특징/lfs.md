

# 특정 repo에 git lfs 적용하기

(해당 레포로 이동 후)
git lfs install

# 특정 repo에 git lfs 해제하기

(해당 레포로 이동 후)
git lfs uninstall

# LFS로 File 관리하기

먼저 lfs를 사용하고자 하는 repo에서 다음을 입력하여 lfs를 적용해야한다.

git lfs install

그 다음 lfs로 관리할 파일을 track한다. 기본적으로는 해당 파일을 git add하기 전에, git lfs track을 해주어야한다. 만약 기존에 add해둔 파일을 lfs로 관리해야하는 상황이라면 git rm --cache로 먼저 unstaging을 시킨 다음, 다시 git lfs track을 해야한다.

git rm --cahced <file path>
git lfs track <file path>

그러면 해당 파일의 내용이 원래의 contents가 아니라, lfs pointer로 바뀌는 것을 알 수 있다.또한 lfs로 트래킹하는 파일에 대한 정보는 .gitattributes을 통해서 관리가 되어 이 변경사항을 꼭 add해주어야한다. 나머지는 일반적인 git push와 동일하다.
