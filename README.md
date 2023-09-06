# PicoSDK_yoenhee

C/C++ 관련 프로젝트를 라즈베리파이 Pico를 활용하여 해보기 
## 개발환경 
### Window (11)

위 [링크](https://github.com/raspberrypi/pico-setup-windows/tree/master#pico-setup-for-windows)에 접속해서 실행파일을 다운로드하며 설치하면 아래의 세팅이 윈도우 환경에서 준비됨.

근데 위 방식으로 하게되면 무엇을 세팅했는지 모르기 때문에 직접 세팅하는것을 해보기로함. 
### GNU Arm Embedded Toolchain 세팅하기  
1. [GNC Arm Embedded Toolchain Download](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads) 페이지에서 11.2-2022.02버전을 다운로드 한다. **(꽤 시간이걸림)** 



### Linux (Ubuntu 20.4)

#### Tool chain설치하기
```bash 
sudo apt install cmake gcc-arm-none-eabi libnewlib-arm-none-eabi build-essential
```
#### SDK update하기
```bash
cd pico-sdk
git pull
git submodule update
```

#### Blink예제 실행하기
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
### 참고링크
- [Getting started with Rasberry Pi Pico](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf) 

- [Intro to Raspberry Pi Pico and RP2040 - C/C++ Part 1](https://www.youtube.com/watch?v=B5rQSoOmR5w&t=10s&ab_channel=DigiKey)

- [윈도우에서 세팅하는 방법](https://shawnhymel.com/2096/how-to-set-up-raspberry-pi-pico-c-c-toolchain-on-windows-with-vs-code/)

## Debugging 
라즈베리파 3B+에 OPEN OCD를 설치하여 디버깅으로 사용해보기 

### 라즈베리파이 3B+에 OpenOCD 설치하기
```bash 
sudo apt install automake autoconf build-essential texinfo libtool libftdi-dev libusb-1.0-0- dev 
```
```bash
git clone https://github.com/raspberrypi/openocd.git
```
```bash 
cd openocd
./bootstrap
```
```bash 
./configure –enable-ftdi –enable-sysfsgpio –enable-bcm2835gpio
```
```bash
make
```
여기까지 진행했음. make를 하면 뻗는 문제가 있음. 부분적인 것을 빌드하는 방법을 찾아야함.




*OpenOCD란?
- 제조사에서 제공해주는 tool을 사용하지 않고 프로그램할 때 필요하다. 

### 참고링크
- [Raspberry pi and OpenOCD](https://iosoft.blog/2019/01/28/raspberry-pi-openocd/)
- [Adafruit Programming Microcontrollers using OpenOCD on a RasberryPI ](https://learn.adafruit.com/programming-microcontrollers-using-openocd-on-raspberry-pi/overview)
- [Open OCD User manual](https://openocd.org/doc/html/index.html)
- [DeskOfLadyada](https://www.youtube.com/live/-EIaDxSIBYw?si=cKCvN8DlGxepgTew) 
  - "제조사에서 제공해주는 tool을 사용하지 않고 프로그램할 때 필요하다."   
  - "다양한 제조사를 지원해준다. 
- [Learn how to Program and Debug Rasberry Pi Pico with SWD](https://www.electronicshub.org/programming-raspberry-pi-pico-with-swd/)

