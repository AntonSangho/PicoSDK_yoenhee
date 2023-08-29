# PicoSDK_yoenhee

C/C++ 관련 프로젝트를 라즈베리파이 Pico를 활용하여 해보기 
## Window (11)

위 [링크](https://github.com/raspberrypi/pico-setup-windows/tree/master#pico-setup-for-windows)에 접속해서 실행파일을 다운로드하며 설치하면 아래의 세팅이 윈도우 환경에서 준비됨.

근데 위 방식으로 하게되면 무엇을 세팅했는지 모르기 때문에 직접 세팅하는것을 해보기로함. 
### GNU Arm Embedded Toolchain 세팅하기  
1. [GNC Arm Embedded Toolchain Download](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads) 페이지에서 11.2-2022.02버전을 다운로드 한다. **(꽤 시간이걸림)** 



## Linux (Ubuntu 20.4)

### Tool chain설치하기
```bash 
sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi build-essential
```
### SDK update하기
```bash
cd pico-sdk
git pull
git submodule update
```

### Blink예제 실행하기
```bash
cd pico-example
mkdir build 
cd build
```
```bash
export PICO_SDK_PATH=../../pico-sdk
```
```bash
cmake
```
```bash
cd blink
make -j4```
```bash
ls /media/anton/RPI-RP2
```
```bash
sudo cp blink.u2f /media/anton/RPI-RP2/
```


 

# 참고
- [Getting started with Rasberry Pi Pico](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf) 

- [Intro to Raspberry Pi Pico and RP2040 - C/C++ Part 1](https://www.youtube.com/watch?v=B5rQSoOmR5w&t=10s&ab_channel=DigiKey)

- [윈도우에서 세팅하는 방법](https://shawnhymel.com/2096/how-to-set-up-raspberry-pi-pico-c-c-toolchain-on-windows-with-vs-code/)