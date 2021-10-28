# 도커

> 컨테이너 기반 가상화 도구

## 가상화

### 🤔 가상화가 왜 필요할까?

궁금증에 앞서 이런 상황을 가정해봅니다.

1. 서버에 개발한 프로그램을 올립니다.
2. 이 때, 서버에 사용가능한 자원이 남는 경우가 발생합니다.
3. 그래서 프로그램을 하나 더 서버에 더 올리기로 합니다.
4. 하지만 기존에 프로그램과 새로운 프로그램 사이에 충돌이 발생하는 경우

따라서 가상화는 서버의 자원을 나누어 각각 프로그램에 알맞게 나누어준다고 생각할 수 있습니다.

### 서버 가상화
하나의 물리적 서버 호스트에서 여러 개의 서버 운영 체제를 게스트로 실행할 수 있게 해주는 소프트웨어 아키텍쳐입니다.

## 하이퍼 바이저

서버 가상화 기술을 구현할 수 있게 해주는 소프트웨어입니다.

이렇게 생성된 여러 개의 운영체제는 가상 머신이라는 단위로 구별합니다.

각 가상머신에는 여러 운영체제가 설치되어 사용되고 하이퍼 바이저에 의해 생성되고 관리되는 운영체제를 **게스트 운영체제**라고 부릅니다.

각 게스트 운영체제는 다른 게스트 운영체제와 완전히 독립된 공간과 시스템 자원을 할당 받아 사용합니다.

### 역할

* OS에게 자원을 나누어주며 조율
* OS들의 커널을 번역해서 하드웨어에 전달

>대표적인 가상화 툴 (eg. VirtualBox, VMWare)

### 단점
각종 시스템 자원을 가상화하고 독립된 공간을 생섣하는 작업은 **하이퍼 바이저**를 반드시 거치기 때문에 일반 호스트에 비해 성능 손실이 발생합니다.

또한, 가상 머신에는 **게스트 운영체제**를 사용하기 위한 라이브러리, 커널 등을 전부 포함하기 때문에 배포하기 위한 이미지로 만들었을 때 크기 또한 더 커집니다.

즉, 가상 머신은 완벽한 운영체제를 생성할 수 있는 장점은 있지만 성능이 느리고, 용량상으로 부담이 됩니다.

**따라서 이런 단점을 극복하기 위해 컨테이너라는 기술이 등장합니다.**

## 컨테이너
가상화된 공간을 생성하기 위해 리눅스 자체 기능인 chroot, 네임스페이스, cgroup을 사용함으로써 프로세스 단위의 격리 환경을 만듭니다.

컨테이너 안에는 애플리케이션을 구동하는데 필요한 라이브러리 및 실행 파일만 존재합니다.

그렇기 때문에 이미지로 만들었을 때, 이미지의 용량 또한 가상 머신에 비해 대폭 줄어듭니다.

따라서 이미지를 만들어 배포하는 시간이 가상머신에 비해 빠르며, 가상화된 공간을 사용할 때, 성능 손실도 거의 없다는 장점이 있습니다.

>이러한 컨테이너 기술을 도커만의 기술이 아닙니다.
<br>
도커 이외에 여러 벤더사에서도 제공합니다.

**도커는 결론적적으로 컨테이너 기술에 여러 기능을 추가한 오픈소스 프로젝트입니다.**

프로그래밍 관점에서 자주 접할 수 있는 컨테이너는 컨테이너에 담긴 것들의 **라이프 사이클**을 관리해줍니다.

가상화 관점에서의 **컨테이너란 이미지의 목적에 따라 생성되는 프로세스 단위의 격리 환경**입니다.

이 떄, 이미지는 간단히 **컨테이너를 만들기 위한 틀**이라고 생각할 수 있습니다.

컨테이너는 파일 시스템과 격리된 시스템 자원 및 네트워크를 사용할 수 있는 독립된 공간을 가집니다.

컨테이너가 실행되며, 프로세스가 실행되기에 필요한 자원들을 할당 받고 프로세스를 실행합니다.

이 때, 커널을 통해 필요한 자원들을 가져옵니다.

**Host OS**에서는 컨테이너 환경에서 실행되는 프로세스나 직접 실행되는 프로세스나 똑같은 프로세스로 취급됩니다.

컨테이너는 **Host와의 격리를 통해 독립된 개발 환경을 보장**합니다. 컨테이너에 어떤 설정을 하든 Host OS에 영향을 끼치지 않습니다. 즉, 독립적인 개발환경을 보장받을 수 있음을 의미합니다.

 이를 통해 프로세스를 컨테이너 단위로 바라볼 수 있게 되고 프로세스의 관리, 확장에 용이해집니다.

### 🤔 그렇다면 컨테이너를 관리하는 방법은?

사용자는 **Docker Engine**을 통해 컨테이너를 관리할 수 있습니다.

## 도커엔진