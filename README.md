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

## Open OCD (On-Chip-Debugger) 
라즈베리파 3B+에 OPEN OCD를 설치하여 디버깅으로 사용해보기 

*OpenOCD란?  
: 제조사에서 제공해주는 tool을 사용하지 않고 프로그램할 때 필요하다. 

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
make -j4
```
*참고: '-j' 옵션을 사용하면 실행할 동시 작업 수를 지정할 수 있습니다. 라즈베리파이 3에는 쿼드코어 CPU가 탑재되어 있기 때문에, 4개의 동시 작업을 선택했습니다. 
```bash
sudo make install 
```
### GDB 설치하기
```bash
sudo apt install gdb-multiarch
```
<img src="https://www.electronicshub.org/wp-content/uploads/2021/03/Pico-SWD-2.jpg" width="700" height="400">

### SWD pin 연결하기
|Rasberry Pi Pico | Raspberry Pi|
|---|---|
|SWDIO|GPIO24(PIN18)|
|GND|GND(PIN20)|
|SWCLK|GPIO25(PIN22)|
<img src="https://www.electronicshub.org/wp-content/uploads/2021/03/Program-Raspberry-Pi-Pico-with-SWD-Image-2.jpg" width="500" height="300">

### SWD로 Raspberry Pi pico를 프로그램 넣기
<img src="https://www.electronicshub.org/wp-content/uploads/2021/03/Pico-SWD-3.jpg" width="700" height="400">

```bash 
openocd -f interface/raspberrypi-swd.cfg -f target/rp2040.cfg -c “program blink/blink.elf verify reset exit”
```  
- 위의 명령은 OpenOCD를 호출하여 blink.elf 파일을 라즈베리 파이 파이 파이코에 프로그래밍하고, 보드를 리셋한 후 OpenOCD를 종료합니다. 모든 것이 정상적으로 진행되면 터미널에 다음과 같은 내용이 표시되고 Raspberry Pi Pico의 LED가 깜박이기 시작해야 합니다.

### SWD로 디버깅하기 

하기에 앞서 전에 만들었던 build 디렉토리를 제거한 뒤에 새 build디렉토리를 만들어야 합니다. 
<img src="https://www.electronicshub.org/wp-content/uploads/2021/03/Pico-SWD-6.jpg" width="700" height="400">

...이 뒤에 내용은 [링크](https://www.electronicshub.org/programming-raspberry-pi-pico-with-swd/)를 참고해서 진행하면됨.







### 참고링크
- [Raspberry pi and OpenOCD](https://iosoft.blog/2019/01/28/raspberry-pi-openocd/)
- [Adafruit Programming Microcontrollers using OpenOCD on a RasberryPI ](https://learn.adafruit.com/programming-microcontrollers-using-openocd-on-raspberry-pi/overview)
- [Open OCD User manual](https://openocd.org/doc/html/index.html)
- [DeskOfLadyada](https://www.youtube.com/live/-EIaDxSIBYw?si=cKCvN8DlGxepgTew) 
  - "제조사에서 제공해주는 tool을 사용하지 않고 프로그램할 때 필요하다."   
  - "다양한 제조사를 지원해준다. 
- [Learn how to Program and Debug Rasberry Pi Pico with SWD](https://www.electronicshub.org/programming-raspberry-pi-pico-with-swd/)
- [Programing Raspberry Pi Pico using C | Getting started with SDK](https://www.electronicshub.org/program-raspberry-pi-pico-using-c/)

