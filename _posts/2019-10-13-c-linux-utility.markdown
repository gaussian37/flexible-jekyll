---
layout: post
title: 쓸만한 리눅스 유틸리티 정리 
date: 2019-02-08 00:00:00
img: c/linux/linux.jpg
categories: [c-linux] 
tags: [리눅스 유틸리티] # add tag
---

<br>

- 이 글에서는 리눅스에서 사용할 만한 유틸리티에 대하여 알아보도록 하겠습니다.
- 물론 제가 사용해보고 좋았던 것을 정리하기 위함이니 호불호가 있을 수 있음을 참조해 주시면 감사하겠습니다.

<br>

## **목차**

<br>

- ### vim
- ### terminator
- ### 나눔고딕코딩 폰트 설치
- ### uim (한글 키보드 사용)
- ### gparted: GUI 환경 파티션 및 포맷
- ### putty를 이용한 시리얼 원격 접속
- ### (Window) : minGW
- ### xclip을 이용한 clipboard 복사
- ### octave 설치 및 octave 패키지 설치 방법
- ### baobab을 이용한 디스크 사용 현황 확인
- ### tree를 이용한 디렉토리 구조 출력
- ### tweak tool을 이용한 GUI 제어
- ### NVIDIA GPU 상태 확인
- ### 터미널 tab 관리

<br>

## **vim**

<br>

- `vim` 관련 내용은 다룰 것이 많아서 따로 정리하였습니다.
- 아래 링크를 참조하시기 바랍니다.
    - https://gaussian37.github.io/c-linux-vim-setting/

<br>

## **terminator**

- 우분투를 사용할 때 터미널을 분할 하시고 싶을 때가 간간히 있습니다. 이럴 때 유용한 프로그램입니다. 
- 먼저 terminator를 설치합니다. 
    - `sudo apt install terminator`
- 터미널에 `./terminator`라고 치면 사용할 수 있습니다.
- terminator 를 분할하는 핫 키는 다음과 같습니다.
    - ctrl + shift + e 세로분할
    - ctrl + shift + o 가로분할
    - ctrl + shift + w 닫기
    - ctrl + shift + q 종료

<br>

## **나눔고딕코딩 설치**

<br>

- `sudo apt install fonts-nanum-coding`

<br>

## **uim (한글 키보드 사용)**

<br>

- 참조 : https://pangtrue.tistory.com/70
- 먼저 `uim`을 설치합니다.
    - `sudo apt install uim`

<br>

- `Region & Language`에 들어가서 Input source에 English하나만 남기고 지웁니다. 
    - 예를 들어 language는 영어, Format은 한국, Input source는 English(US)로 해놓으면 됩니다.

<br>

- `Language Support`에서 Keyboard input method가 IBus로 설정되어있을텐데, `uim`으로 바꿔줍니다.

<br>

- 다음으로 사용할 uim을 설정해보겠습니다. (한영전환 단축키와 한자 단축키)
- `Input Method`를 실행하고 `Global settings 탭`의 `Input method deployment` 영역에서 `Specify default IM` 항목을 체크합니다. `Default Input method`를 `Byeoru`로 두고 `Enabled Input methods`를 `Byeoru` 만 두고 나머지는 제거합니다.
- 그리고 키 바인딩을 위하여 `Byeoru Key bindings 1 탭`에 들어가서 다음과 같이 세팅합니다.
    - \[Byeoru\] on: "hangul"
    - \[Byeoru\] off: "hangul"
    - \[Byeoru\] convert Hangul to Chinese characters: "hangul-hanja"
    - \[Byeoru\] confirm conversion: "return"
    - \[Byeoru\] cancel conversion: "escape"

- 마지막으로 다음과 같이 명령어를 터미널에서 입력합니다.

<br>

```
// 오른쪽 Alt키의 기본 키 맵핑을 제거하고 'Hangul'키로 맵핑
xmodmap -e 'remove mod1 = Alt_R'
xmodmap -e 'keycode 108 = Hangul'

// 오른쪽 Ctrl키의 기본 키 맵핑을 제거하고 'Hangul_Hanja'키로 맵핑
xmodmap -e 'remove control = Control_R'
xmodmap -e 'keycode 105 = Hangul_Hanja'

// 키 맵핑 저장
xmodmap -pke > ~/.Xmodmap
```

<br>

## **gparted 설치: GUI 환경 파티션 및 포맷**

<br>

- 파티션을 나누거나 USB 포맷을 다양한 옵션을 걸어서 하고 싶을 때, 명령어가 아닌 GUI 환경해서 하고 싶으면 `gparted`를 통해 쉽게 할 수 있습니다.
- `sudo apt install gparted` 

<br>

## **putty를 이용한 시리얼 원격 접속**

<br>

- `sudo apt install putty` 명령어로 putty를 설치합니다.
- 리눅스 PC와 시리얼 통신할 보드를 연결한 다음에 `dmsg | grep tty`를 입력하여 시리얼 통신으로 연결 가능한 포트를 찾습니다.
- 예를 들어 `[30862.686810] usb 3-4: FTDI USB Serial Device converter now attached to ttyUSB0`와 같이 나옵니다.
- `sudo putty /dev/ttyUSB0 -serial -sercfg 115200,8,n,1,N` 와 같이 입력하여 원격 통신을 할 수 있습니다.
- `putty` 명령어 이후의 각 파라미터들은 사실 GUI환경에서 사용자가 입력해 주어야 하는 순서대로 입력된 것입니다.
- 여기서 각 파라미터를 살펴보겠습니다.
- **serial line to connect to** : `/dev/ttyUSB0`
- **speed (baud)** : 115200
- **data bits** : 8
- **parity** : n
- **stop bits** : 1
- **flow control** : N (OFF)

<br>

## **(Window) : minGW**

<br>

- 윈도우에서 C언어를 사용하고 싶을 때, 비주얼 스튜디오는 너무 과하다고 생각되면 `minGW(minimal GNU for Window)`를 사용하시면 됩니다.
- 설치 링크 : http://mingw-w64.org/doku.php/download/mingw-builds
    - 요즘 사용하시는 대부분의 컴퓨터가 64비트인 것을 참조하여 위 링크를 올렸습니다.

<br>
<center><img src="../assets/img/c/linux/utility/1.png" alt="Drawing" style="width: 800px;"/></center>
<br>

- 다은 받은 파일을 실행 하였을 때, 64비트 컴퓨터를 사용하신다면 위와 같이 입력하면 됩니다.
- 저 같은 경우에 `minGW`를 다음 경로에 설치하였습니다.
    - 예) C:\Program Files\mingw-w64\
- 설치한 경로를 찾아서 더 하위 경로인 bin 디렉토리 까지 찾아보겠습니다.
    - 예) C:\Program Files\mingw-w64\x86_64-8.1.0-posix-seh-rt_v6-rev0\mingw64\bin
- bin 디렉토리까지의 경로를 **고급시스템설정보기-환경변수-시스템변수-path**에 추가합니다.
    - 추가하는 목적은 어느 경로에서도 바로 bin 까지의 경로를 접근할 수 있게 하여, 어느 경로에 있더라도 `minGW`를 사용할 수 있도록 합니다.
- 커맨드 창을 열어 어떠한 경로에서라도 `gcc --version`을 입력하셨을 때, 정상적으로 실행이 된다면 `minGW`를 사용하실 수 있습니다.

<br>

## **xclip을 이용한 clipboard 복사**

<br>

- 리눅스 터미널에서 copy & paste를 하려고 할 때, 마우스를 사용하지 않는 방법에 대하여 알아보겠습니다.
- 즉, 키보드만을 이용하여 특정 내용을 copy 하거나 복사하려고 할 때 입니다.
- 먼저 클립보드에 복사된 내용을 터미널에 붙어넣기 할 때에는 간단합니다.
    - 터미널에 클립보드에 복사된 내용 붙여넣기 : `ctrl + shift + v`
- 만약 마우스로 터미널의 어떤 영역을 드래그 한 상태에서 클립보드로 복사하고 싶다면 다음 키 조합으로 사용 가능합니다.
    - 터미널에 드래그 된 영역 클립보드로 복사하기 : `ctrl + shift + c`
- 그러면 터미널의 출력 결과를 클립보드로 복사하기 위한 방법에 대하여 알아보기 위해 다음 앱을 설치합니다.
    - `suto apt-get install xclip`
- 터미널의 출력 결과를 클립보드로 복사하고 싶으면 다음 명령어를 이용합니다.
    - `명령어 | xclip -selection clipboard`
    - 예를 들어 `pwd | xclip -selection clipboard`와 같이 이용하면 pwd 결과를 파이프를 통하여 xclip으로 보내고 그 결과를 클립보드로 저장합니다.
- 하지만 매번 `| xclip -selection clipboard`를 써야하는 것은 불편하기 때문에 `alias`를 이용하여 간편하게 사용해보겠습니다.
    - `alias ccopy='xclip -selection clipboard'`
    - 이 경우 `pwd | ccopy` 라고만 쓰면 됩니다.

<br>

## **octave 설치 및 octave 패키지 설치 방법**

<br>

- 리눅스에서 MATLAB을 사용하고 싶을 때, 따로 설치하기 부담스럽거나 라이센스가 없다면 간이적으로 `octave`를 설치하여 사용할 수 있습니다.
- 사실상 Simulink를 사용하지 않는다면 MATLAB 대신 `octave`로 거의 사용하실 수 있습니다.
- 공식 홈페이지 : https://www.gnu.org/software/octave/
- 설치 방법 : `sudo apt-get install octave`
- octave를 설치한 다음 실행은 터미널에서 `octave`만 치면 GUI 환경이 기본적으로 실행되고 다양한 옵션을 주고 싶으면 `octave -h`를 이용하여 옵션을 확인할 수 있습니다.
- MATLAB에는 툴박스라는 것을 유료로 제공하여 추가 함수 등을 구매해서 사용할 수 있지만 `octave`에서는 추가 패키지만 설치하면 사용할 수 있습니다. 관련 패키지의 정보는 아래 링크에서 확인하실 수 있습니다.
    - 패키지 관령 정보 :https://octave.sourceforge.io/packages.php
- 패키지는 octave를 실행한 다음 octave의 커맨드 창에서 다음 명령어를 통해 설치를 할 수 있습니다.
    - `pkg install -forge package_name`
    - 예를 들어 `pkg install -forge image`를 입력하면 image 관련 패키지가 설치 됩니다.
- 패키지를 설치한 다음 패키지를 사용하고 싶으면 다음 명령어를 매번 실행해 주어야 합니다.
    - `pkg load package_name`
    - 예를 들어 `pkg load image`를 입력하면 됩니다.
- 만약 어떤 패키지를 계속 사용할 예정이라면 디폴트 값으로 설정해 주어야 하는데 터미널에 `vim ~/.octaverc` 또는 `gedit ~/.octaverc`를 입력하여 위에서 설명한 것과 같이 `pkg load package_name`을 입력해 줍니다. 예를 들어 `pkg load image`를 입력하면 됩니다.
- `~/`은 `home` 디렉토리를 뜻하는 명령이고 `.octaverc`는 octave를 실행할 때, 같이 실행되는 명령어들을 모아두는 숨김 파일 형태입니다.
- 따라서 octave를 실행할 때, pkg load 명령어가 실행되므로 기본값으로 패키지를 등록해서 사용할 수 있습니다.

<br>

## **baobab을 이용한 디스크 사용 현황 확인**

<br>

- 리눅스에서 디스크 사용 현황을 확인 하기 위한 방법으로 크게 2가지가 있습니다.
- 가장 쉬운 방법은 `df -h` 명령어를 통하여 사용 현황을 확인하는 방법이 있는 데 터미널에서 보기에 시인성이 좋지 않습니다.
- 반면 `baobab`을 이용하면 recursive 하게 각 폴더 안의 상세 내용 까지 그래픽적으로 확인할 수 있습니다.
- 설치 : `sudo apt-get install baobab`
- 실행 : `sudo baobab`
- 접근 권한이 필요한 디스크의 경우 `sudo baobab`을 명령어를 통해 확인할 수 있으니 `sudo baobab`을 사용하길 권장드립니다.

<br>

## **tree를 이용한 디렉토리 구조 출력**

<br>

- `tree` 명령어를 이용하면 현재 위치 기준으로 하부 디렉토리의 구조를 tree 형태로 출력할 수 있습니다.
- 설치 : `sudo apt-get install tree`
- 터미널 창에서 `tree` 라고 입력하면 현재 위치 기준으로 모든 하부 디렉토리 구조를 볼 수 있습니다.
- 만약 `depth` 기준으로 구분이 필요할 때에는 `L` 옵션을 사용하면 됩니다. 예를 들어 `tree -L 1`은 depth가 1인 경우입니다.

<br>

## **tweak tool을 이용한 GUI 제어**

<br>

- 리눅스 우분투에서 GUI 관련 변경을 하려면 다양한 명령어들을 알아야 하는데 이 기능들을 GUI 환경에서 제어할 수 있도록 설정할 수 있는 tool이 있습니다. 이 tool 이름이 tweak 이고 설치 방법은 다음과 같습니다.
- 설치 : `sudo apt-get install gnome-tweak-tool`
- 설치를 마친 다음에 시작키를 누르고 `tweak`을 누르면 그래픽 창이 하나 뜨는데 그 창에서 다양한 기능을 사용해 보면 됩니다.

<br>

## **NVIDIA GPU 상태 확인**

<br>

- 리눅스에 NVIDIA 설치를 완료하였으면 `nvidia-smi` 명령어로 GPU 사용 상태를 터미널에서 확인할 수 있습니다.
- 만약 실시간으로 상태를 업데이트해서 보고싶으면 다음 명령어를 이용합니다.
    - `watch -d -n 초 nvidia-smi`
    - 만약 0.5초 간격으로 업데이트 해서 터미널에서 보고 싶으면 `watch -d -n 0.5 nvidia-smi`라고 입력하면 됩니다.

<br>

## **터미널 tab 관리**

<br>

- 참조 : [https://superuser.com/questions/657867/how-to-open-new-tab-in-existing-terminal-session-and-using-keyboard-shortcut-m](https://superuser.com/questions/657867/how-to-open-new-tab-in-existing-terminal-session-and-using-keyboard-shortcut-m)
- 리눅스 터미널을 사용할 때, 기존 터미널에서 탭을 생성하여 하나의 터미널 창에서 여러개의 터미널을 사용하고 싶은 경우가 있습니다.
 - 새로운 터미널 창을 생성하는 단축키가 `CTRL + ALT + T`인 반면 기존의 터미널에서 새로운 탭으로 새로운 터미널을 생성하려고 하면 `CTRL + SHIFT + T` 를 사용하여 오픈하면 됩니다. 
- 만약 여러개의 탭이 실행되어 있는 경우 `ALT + (tab number)`를 이용하여 원하는 탭을 바로 접근할 수 있습니다. 예를 들어 ALT + 1 (첫번째 터미널 탭으로 변경) Alt + 2 (두번째 터미널 탭으로 변경)와 같이 접근할 수 있습니다.