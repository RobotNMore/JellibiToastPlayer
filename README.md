# Jellibi Toast (v1.0) Player

**Jellibi Toast 보드(v1.0)** 는 아두이노 나노 호환보드이며 확장보드를 통해 블루투스 통신이 가능하고 네개의 서보 모터를 동시에 제어를 할 수 있습니다.  **Jellibi Toast(v1.0) Player** 는 Toast 보드 기반으로 블루투스를 통해 주행하고 그리퍼를 조작하여 움직이는 프로젝트입니다.  

아래 동영상 속 젤리비 토스트보드에 적용된 코드 입니다. 

[![로봇젤리비 그리퍼 축구경기](https://img.youtube.com/vi/yERpX4W8eDM/0.jpg)](https://youtu.be/yERpX4W8eDM?t=0s "로봇젤리비 그리퍼 축구경기")



### 젤리비 토스트 보드 핀맵 

우선 Jellibi Toast 보드의 핀맵은 아래 테이블과 같습니다.  (Jellibi Toast Player 프로젝트에서 사용하는 핀은 굵은 글씨체로 표시합니다.)

| 핀(포트) |                  기능                  |   확장보드 연결    |
| :------: | :------------------------------------: | :----------------: |
|   D13    |             LED (녹색표시)             |                    |
|   D12    |               Sonar 센서               |                    |
|   D11    | **Motor B PWM (오른쪽 모터 회전속도)** |                    |
|   D10    |  **Motor A PWM (왼쪽 모터 회전속도)**  |                    |
|    D9    |               Servo PWM                |                    |
|    D8    |             Button(오른쪽)             |                    |
|    D7    |              Button(왼쪽)              |                    |
|    D6    |             **LED(청색)**              |                    |
|    D5    |             **LED(적색)**              |                    |
|    D4    |     Motor B (오른쪽) 회전방향제어      |                    |
|    D3    |                 Buzzer                 |                    |
|    D2    |      Motor A (왼쪽) 회전방향제어       |                    |
|    D1    |  UART TX (펌웨어 업로드, 디버그포트)   | **확장보드 BT TX** |
|    D0    |  UART RX (펌웨어 업로드, 디버그포트)   | **확장보드 BT RX** |
|    A0    |              Button(위쪽)              |                    |
|    A1    |             Button(아래쪽)             |                    |
|    A2    |              CDS 조도센서              |                    |
|    A3    |                   -                    |                    |
|    A4    |              **I2C SDA**               |                    |
|    A5    |              **I2C SCL**               |                    |
|    A6    |          IR 센서 (모바일보드)          |                    |
|    A7    |          IR 센서 (모바일보드)          |                    |



### Jellibi 확장보드

젤리비 그리퍼를 움직이기 위해 사용하는 서보모터는  Duty 가 5 ~ 10% 인 50Hz 주기의 PWM(Pulse Width Modulation) 신호로 제어합니다. 젤리비 토스트 보드의 D9(Servo PWM) 핀(포트)을 통해 제어할 수도 있으나  젤리비 확장보드(Extension Board) 에는 PWM 신호를 만들어내는 칩(PCA9685) 이 장착되어 있으며 이 칩을 I2C(Inter-Integrated Circuit) 선로를 통해 제어하면 확장보드의 Servo0, Servo1, Servo2, Servo3 까지 총 네개의 서보모터 제어용 PWM 신호를 만들어 낼 수 있습니다. 

확장보드에는 또한 Bluetooth 통신을 위한 HC-06 모듈이 연결되어 있습니다. HC-06은 안드로이드 스마트폰이나 PC 등과 블루투스 무선 연결을 할 수 있으며 연결된 후 스마트폰등에서 전송하는 명령을 받아 젤리비 토스트 보드에 전달하여 처리할 수 있습니다. 

(확장보드를 연결한 상태에서 아두이노에서 펌웨어를 업로드 할 경우,  업로드하는 선로와 HC-06 블루투스 모듈이 사용하는 선로가 동일하여 펌웨어 업로드에 실패합니다. 이 때는 확장보드에 있는 스위치를 위쪽으로 올린 상태에서 업로드하고 스위치를 아래쪽으로 내려 HC-06 을 사용하도록 합니다. ) 

### 아두이노 PCA9685 PWM Servo 라이브러리 

아두이노에는 PCA9685 를 제어하기 위해 만들어진 라이브러리 가 있습니다.  

_아두이노 메뉴 > 스케치 > 라이브러리포함하기 > 라이브러리 관리_ 메뉴를 선택하면 표시되는 라이브러리 관리 창에서 'Adafruit PWM Servo' 를 검색하면 아래 그림처럼 Adafruit 에서 제작한 라이브러리를 설치 할 수 있습니다. 이 JellibiToastPlayer 프로젝트는 이 라이브러리 기반으로 제작되었기 때문에 설치가 필요합니다. 

![1560765506926](http://www.robotnmore.com/matthew/toast/servolibinstall.png)

### 빌드 및 실행 

1. 젤리비 토스트 보드와 PC 를 USB 케이블로 연결합니다. 
2. 아두이노 툴에서 JellibiToastPlayer 프로젝트를 열고 빌드를 진행하여 빌드에 문제가 없는 지 확인합니다.
3. 보드에 업로드 합니다. 
   1. 확장보드가 연결되어 있는 상태라면 스위치를 위로 올려 업로드 할 수 있는 상태로 변경합니다. 
4. 확장보드를 연결하고 스위치를 아래로 내려 HC-06 블루투스 모듈과 젤리비 토스트 보드가 통신 할 수 있도록 준비합니다. 
5. 안드로이드 Play Store 에서 "Arduino bluetooth controller" 등의 앱을 다운로드 하고 실행 한 후 HC-06 모듈을 검색하고 패어링을 진행합니다. (기본 PIN 코드(패스워드) 는 '1234' 입니다.) 
6. Arduino Bluetooth Controller 앱에서 명령어로 사용하는 문자인 'U' / 'R' / 'D' / 'L' / 'S'/ 'O' / 'o' / 'G' / 'g' 등을 버튼에 연결합니다.