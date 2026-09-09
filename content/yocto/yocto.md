# 구조 
```
Yocto Project
    ├── Poky          ← 레퍼런스 배포판 (빌드 시스템 포함)
    ├── BitBake       ← 빌드 엔진 (make 같은 것)
    ├── OpenEmbedded  ← 레시피 모음
    └── Layer         ← 기능별 모듈 단위
```


# layer 구조 
```
met+a/              ← OpenEmbedded 기본 레이어
meta-poky/         ← Poky 배포판 레이어
meta-nxp/          ← NXP i.MX 보드 지원
meta-variscite/    ← Variscite 보드 커스텀
meta-myapp/        ← 내가 만드는 앱 레이어
```


용어설명
Recipe (.bb)패키지 빌드 방법 정의 파일
Layer   Recipe들의 묶음
BitBake 레시피 읽고 빌드하는 엔진
Image   최종 결과물 (부팅 가능한 OS 이미지)
conf/local.conf 빌드 설정 파일
MACHINE 타겟 보드 지정


# 실제 빌드 흐름 
```
# 1. 환경 설정
source poky/oe-init-build-env build/

# 2. 보드 설정 (local.conf)
MACHINE = "imx8mp-var-dart"

# 3. 빌드
bitbake fsl-imx-xwayland   # 지금 쓰는 이미지!

# 4. 결과물
build/tmp/deploy/images/
```

# Variscite에서 Yocto 쓰는 이유

NXP BSP + Variscite 보드 설정이 레이어로 제공됨
필요한 패키지만 골라서 경량 OS 제작 가능
커널, 드라이버, 앱까지 한 번에 빌드

# 환경 구성
docker 설치 
```
sudo apt update && sudo apt install docker.io qemu-user-static
sudo usermod -aG docker ${USER}

```
sudo usermod -aG docker ${USER} 얘 사용법 확인 필요 


디렉토리 생성
- mkdir 
- name : var-mx95-yocto 


repo download
```
repo init -u https://github.com/varigit/variscite-bsp-platform.git -b walnascar -m imx-6.12.49-2.2.0.xml
repo sync -j$(nproc)
```
script 실행
./var-start-container.sh


최초한번 
MACHINE=imx95-var-dart DISTRO=fsl-imx-xwayland . var-setup-release.sh build_xwayland

이미 있을때 qt는 사용하지 않으니 
source setup-environment build_xwayland



bitbake fsl-image-gui


toolchain
- populate_sdk 



python 버전 에러 

python 3.9 설치 
```
sudo apt-get update
sudo apt-get install -y python3.9 python3.9-dev python3.9-distutils

# 기본 python3를 3.9로 변경
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.8 1
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.9 2
sudo update-alternatives --config python3
```

g++ 버전 에러 

g++ 10설치 

```
sudo apt-get install -y gcc-10 g++-10

# 기본 버전 변경
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-10 10
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-10 10
```

# bitbake 설정파일 수정 
```
cat >> /workdir/build_xwayland/conf/local.conf << 'EOF'
BB_NUMBER_THREADS = "8"
PARALLEL_MAKE = "-j4"
EOF
```

ptest는 패키지 테스트(Package Test) 빌드인데, 카메라 영상처리에 전혀 필요 없어요.
ptest 자체를 비활성화하세요:

```
echo 'DISTRO_FEATURES:remove = "ptest"' >> /workdir/build_xwayland/conf/local.conf

echo 'PTEST_ENABLED:pn-qtbase = "0"' >> /workdir/build_xwayland/conf/local.conf

```


공식 Variscite 빌드인데 패치가 안 맞는 건 이상
1. nnstreamer 소스가 최신으로 업데이트됨 — SRC_URI가 특정 커밋이 아닌 브랜치를 따라가면 소스가 바뀌어서 패치가 안 맞을 수 있어요
2. repo sync를 여러 번 했거나 중간에 소스가 변경됨


# OpenSSL 버전 호환성 문제
tpm2-tss-engine 1.2.0이 최신 OpenSSL 3.x API와 맞지 않아서 const 관련 컴파일 에러가 나는 거예요. 이건 코드 문제라 단순 재빌드로는 안 됩니다.

```
# local.conf에 추가
echo 'CFLAGS:append:pn-tpm2-tss-engine = " -Wno-error -Wno-discarded-qualifiers"' >> /workdir/build_xwayland/conf/local.conf

```
tpm2는 TPM 보안 칩 관련 패키지라 카메라 영상처리랑 무관해요. 필요 없으면 그냥 제외하는 게 더 깔끔합니다:


# error 
Yocto 버전업 되면서 변수명을 더 직관적으로 바꾼 거예요.

PNBLACKLIST → "blacklist"라는 단어가 인종차별적 표현이라는 이슈로
SKIP_RECIPE → 기능을 더 명확하게 표현


```
# 기존 PNBLACKLIST 라인들을 SKIP_RECIPE로 교체
sed -i 's/PNBLACKLIST/SKIP_RECIPE/g' /workdir/build_xwayland/conf/local.conf


grep -E "SKIP_RECIPE|PNBLACKLIST" /workdir/build_xwayland/conf/local.conf

```



