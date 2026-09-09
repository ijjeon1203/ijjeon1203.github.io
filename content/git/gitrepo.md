1. gitlab에서 그룹으로 묶기
2. group에 repo 이름을 가진 repository 생성 
   1. 이 repository안에 default.xml 생성

3. repo 초기화 
```
repo init -u https://gitlab주소/project/repo.git -b main
```

4. repo 동기화

```
repo sync 
```

1. 

# default.xml 파일 내용 
```
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <remote name="origin" fetch="http://192.168.1.233:30080/2026-fcu"/>
  <default remote="origin" upstream="master" revision="master" sync-j="4"/>
  <project name="fcu_sw"/>
  <project name="docs"/>
</manifest>

```


# trouble shooting 

접속 안될 때 접속확인부터 

```
git ls-remote http://192.168.1.233:30080/2026-fcu/repo.git
```