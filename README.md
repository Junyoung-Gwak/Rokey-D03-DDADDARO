# Cake lettering robot- DDADDARO
(따끈따끈 로봇 베이커리)

ROKEY 6기 - 협동1(ROS2를 활용한 로봇 자동화 공정 시스템 구현)

# DDADDARO Project: M0609 Robot Arm Control

이 프로젝트는 **Doosan Robotics M0609** 로봇팔 제어와 웹 기반의 **고객/관리자 모니터링 시스템**을 통합한 솔루션입니다. ROS 2 Humble 환경에서 작동하며, Rosbridge를 통해 웹 인터페이스와 실시간으로 통신합니다.
![레터링_근접샷_1_1_1_1_1](https://github.com/user-attachments/assets/470b348c-202b-4db3-a7d3-a7b548e5e3f4)
---

## 시스템 설계 그림
![Screenshot from 2026-02-02 15-38-21.png](attachment:1ec64ee3-47dc-48fb-b043-2d5fbd98562e:Screenshot_from_2026-02-02_15-38-21.png)

## Flow chart 그림
![image.png](attachment:3f7d297d-5cb8-4a3d-a21b-a2032e62eaad:image.png)



---

## 1. 개발 환경 (Environment)

### Hardware
- **Robot Arm:** Doosan Robotics M0609
- **Control PC:** Ubuntu Samsung Laptop, Ubuntu Asus Laptop
- **Connection: Ethernet (LAN) cable (Static IP: 192.168.1.100)

### Software
- **OS:** Ubuntu 22.04 LTS
- **ROS Version:** ROS 2 Humble
- **Language:** Python 3.10, Node.js (JavaScript)

---

##  2. 설치 방법 (Installation)

프로젝트 실행을 위해 필요한 의존성 패키지들을 설치합니다.

### 2.1 ROS 2 의존성 설치
```bash
# 패키지 업데이트
sudo apt update

# Rosbridge Server 설치 (웹-ROS 통신용)
sudo apt install ros-humble-rosbridge-server

### 2.2 Node.js 및 npm 설치

# Node.js 및 npm 설치 (모니터링 웹 환경용)
sudo apt install nodejs npm

### 2.2 Python 의존성 설치 (requirements.txt)
프로젝트 실행에 필요한 Python 라이브러리들을 설치합니다.

pip install -r requirements.txt
## 3. 실행 방법 (Usage)


# 프로젝트 루트 폴더에서 실행
터미널을 여러 개 열어 아래 순서대로 실행해 주세요.

Step 1: M0609 로봇팔 연결
실제 로봇과 통신을 시작하고 Rviz를 통해 상태를 확인합니다.

ros2 launch dsr_bringup2 dsr_bringup2_rviz.launch.py mode:=real host:=192.168.1.100 port:=12345 model:=m0609


Step 2: Rosbridge Server 구동
웹 모니터와 ROS 2 노드 간의 메시지 브릿지를 실행합니다.

ros2 launch rosbridge_server rosbridge_websocket_launch.xml


Step 3: 웹 모니터링 시스템 실행
각 모니터 대시보드를 로컬 서버로 구동합니다.

- PC1 에서 실행
[고객용 모니터]
cd ~/ddaddaro_ws/custom_monitor
npm install  # 첫 실행 시 의존성 설치 필요
npm run dev


- PC2 에서 실행
[관리자용 모니터]
cd ~/ddaddaro_ws/admin_monitor
npm install  # 첫 실행 시 의존성 설치 필요
npm run dev


Step 4: 메인 로직 실행
프로젝트의 핵심 동작 노드를 실행합니다.

- PC2 에서 실행
ros2 run ddaddaro ddaddaro



## 4. 프로젝트 구조 (Structure)

ddaddaro: 메인 ROS 2 패키지 및 제어 로직

custom_monitor: 고객용 인터페이스 (React)

admin_monitor: 관리자용 제어 및 모니터링 대시보드 (React)

dsr_bringup2: 두산 로봇 하드웨어 인터페이스 설정
