---
layout: post
title: Reinstall 3 OSes (ft. post-finalterm)
tags: [os, linux, macos]
---

기말고사가 끝났다. ~~성적은 묻지 말자.~~

2018년처럼, 기말고사 후 OS 재설치를 하게 되었다.

## Introduction
macOS, Linux, Windows 3개를 쓰고 있는데, 파티션을 다음과 같이 해 놓은 상태였다.

- macOS: 50GiB (그냥 안쓰고 비상용으로 냅둠)
- Linux: 100GiB (주로 코딩&삽질용)
- Windows: 100GiB (과제용~~이라 읽고 과제하다 멘붕할때 코딩용~~)

이번에는 맥을 다시 쓰고, 윈도우를 계속 쓰다가 암이 걸려서 다음과 같이 설치하기로 했다.

- macOS: 125GiB (개발용 #1)
- Linux: 125GiB (개발용 #2)
- Windows (VM): 50GiB @ 외장SSD (이건 정말 과제용)

현재 macOS와 Linux를 설치한 상태이다. 리눅스는 만자로를 Architect Edition으로 설치했는데, 처음에는 그걸로 WM/DE를 여러 개 설치할 수 있는 줄 알고 썼지만 그건 착각이었다. (원래 계획은 Cinnamon + i3 조합으로 리눅스를 쓰는 것이었다.) ~~만자로 쓴다고 할때 친구 반응: '차라리 원자로를 써라'~~

macOS 설치는 그냥 bootable installer를 만들어서 SSD 전체를 포맷하고 설치한 거라서, 뭐 딱히 설명할 건 없고, Architect Edition으로 설치한 이야기를 하려고 한다.

## Manjaro installation w/ Architect 
### Boot
일단 부팅을 하면 grub으로 만든 것으로 추정되는 메뉴가 뜬다. 거기서 timezone이나 keyboard layout같은 것을 설정할 수 있다. timezone을 설정했지만 후에 무쓸모한 것으로 밝혀졌다. ~~리눅스 설치하는 도중에 `^Z`로 멈추고 `date`로 시간보는 흑우가 있다?~~

어쨌든 부팅을 하면 간단한 쉘을 볼 수 있었다. 여기서 `setup` 명령어를 입력하면 설치 프로그램이 시작된다.

### Network
가장 답이 없는 부분은 와이파이를 연결하는 것이었다.

`setup`을 실행하면 처음에 인터넷에 연결하라는 메시지가 뜨고, 네트워크 설정 메뉴를 띄워준다.

그래서 나는 거기서 와이파이를 설정했지만 연결되는 일은 일어나지 않았다.

왜 이러지? 라는 생각과 함께 `ls /dev`를 해봤는데, 아예 와이파이 모듈이 잡히지 않았다. 와이파이 드라이버가 로딩되지 않은 것이다.

이전에도 이런 이슈를 아치리눅스에서 겪은 적이 있었고, 이럴 때는 그냥 와이파이 모듈을 로드하면 되었다.

```shell
$ sudo modprobe brcmfmac
```

이렇게 모듈을 로드한 뒤에는 `nmcli`로 와이파이를 간단하게 연결하면 된다. (`$wifi_name`은 당연히 연결할 와이파이의 이름으로 바꿔야 한다.)

```shell
$ nmcli device wifi connect $wifi_name -a
```

그리고 나서 본격적으로 설치를 할 수 있다.

### Installation
우선 텍스트로 된 메뉴가 뜨는데, prepare installation으로 들어가면 콘솔을 설정하고, 디스크를 파티션하는 등의 일을 할 수 있다.

콘솔을 설정할 필요는 딱히 없었고, 디스크 파티션만 하면 된다.

맥의 경우 EFI만 지원하므로(뇌피셜) `cgdisk`를 사용해서 파티션하면 된다.

설치 전 맥에서 미리 125GiB FAT 파티션을 만들어 두었다. 리눅스에서 APFS의 크기를 줄이는 것은 불가능하기 때문이다. (사실 이건 그 이전세대인 HFS에서도 마찬가지인데, gparted로 shrink를 시도했다가 몇시간이 걸렸고 그마저도 실패했던 경험이 있다.)

`cgdisk`에서는 만들어둔 파티션을 없애고 100GiB를 데이터 파티션, 16GiB를 swap으로 할당했다 (분명 macOS에서는 125GiB으로 보였는데, 9GiB가 사라졌다.)

파티션을 만들고 나서, 암호화하거나 LVM을 사용하는 옵션을 주었지만 LVM은 디스크를 통째로 지우지 않는 이상 사용할 수 없고, 암호화는 굳이 지금 안해도 되는 부분이여서 그냥 넘어갔다.

그리고 나서 파티션을 mount(+format)하는 메뉴가 나온다. 아까 만든 파티션을 루트로 설정하고 btrfs로 포맷했다. 한 번 실험해보고 싶어서였는데, 어떻게 될지는 모르겠다. (나중에 btrfs 망함... 같은 포스트가 올라올지 모르겠다.) swap파티션도 설정하고 넘어가면 된다. `/boot` 파티션은 있는 것을 고르면 된다.

이제 mirrorlist를 설정하면 된다. rank mirrors by speed로 빠른 미러들을 찾을 수 있다. 그리고 나서 refresh pacman keys라는 옵션이 있는데, 나는 했지만 알고보니 필요 없다고 한다.

이제 install desktop system 메뉴를 선택하고 본격적인 설치를 하면 된다.

install base라는 창이 뜨는데, 여기서는 커널을 한 개 이상 선택하면 된다. 그 다음 DE/WM을 고르는데, **하나만 고를 수 있다.** ~~젠장~~ 패키지를 몇개 더 고르고, 설치를 하면 된다. 일반적인 pacman과 달리 progressbar가 뜨지 않는다. 나 빼고 아무도 신경 안쓰는 문제여서 그런지 해결책이 없는 것 같다.

매우 오랜 시간 동안 다운로드와 설치가 끝나면, 그래픽 드라이버를 설치해야 한다. 나는 iris를 사용하고 있어서 그냥 오픈소스 드라이버를 설치했다.

이제 남은 설정들은 대부분 크리티컬한 건 아니지만, 잘못하면 골치가 아프다.

### Post-Installation
일단 부트로더를 정한다. 나는 refind를 선택했다.

fstab을 설정하게 하는데, 여기서는 무난하게 UUID로 정하는 것이 좋다.

hostname과 locale, keyboard layout, timezone, root password를 설정한 후, 일반 사용자를 하나 만들면 끝난다.

이제 chroot into installation을 선택한 후, 일반 사용자에서 sudo를 사용할 수 있도록 wheel에 추가한다. (여기서 `$user_name`은 당연히 사용자 이름이다.)

```
$ usermod -aG wheel $user_name
```

그리고 재부팅하면 설치한 리눅스를 볼 수 있다.
