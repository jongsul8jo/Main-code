
### Arduino 코드 설명

- **SoftwareSerial espSerial(2, 3);**：소프트웨어 시리얼 정의, ESP-01과 통신에 사용됩니다.
- **const int mq7Pin = A0;**：MQ-7 센서가 연결된 핀을 정의합니다.
- **const char* ssid 와 password**：WiFi의 SSID와 비밀번호를 정의합니다.
- **const char* server 와 int port**：서버의 IP 주소와 포트를 정의합니다.
- **unsigned long previousMillis 와 interval**：데이터 수집 주기를 제어하기 위해 시간 간격을 정의합니다.
- **void setup()**：시리얼 통신을 초기화하고, ESP-01 모듈을 리셋하며, WiFi 모드를 설정하고 WiFi 네트워크에 연결합니다.
- **void loop()**：10초마다 센서 데이터를 읽고 WiFi를 통해 서버에 전송합니다.
- **bool sendCommand(String command, int maxTime)**：ESP-01로 AT 명령어를 보내고 응답을 기다립니다.

### Flask 서버 코드 설명

- **Flask 및 필요한 모듈 가져오기**：Flask, request, render_template, SQLAlchemy 및 datetime을 가져옵니다.
- **Flask 앱 설정**：Flask 앱을 설정하고 데이터베이스 URI와 트랙 수정 설정을 구성합니다.
- **SensorData 모델 정의**：SensorData라는 데이터베이스 모델을 정의합니다. 이 모델은 타임스탬프와 센서 값을 저장합니다.
- **데이터베이스 테이블 생성**：애플리케이션 컨텍스트에서 데이터베이스 테이블을 생성합니다.
- **/update 엔드포인트**：센서 데이터를 받아 데이터베이스에 저장합니다.
- **/ 엔드포인트**：저장된 센서 데이터를 웹 페이지에 시각화하여 표시합니다.
- **Flask 앱 실행**：Flask 서버를 실행합니다.

### HTML 템플릿 설명

- **HTML 기본 구조**：HTML 문서의 기본 구조를 정의합니다.
- **CSS 스타일**：테이블 스타일을 정의하여 테이블이 100% 너비를 가지며, 경계선을 추가하고, 셀 패딩을 설정합니다.
- **JavaScript**：10초마다 페이지를 새로고침하여 실시간 데이터를 표시합니다.
- **HTML 본문**：센서 데이터를 테이블 형식으로 표시합니다. 데이터는 타임스탬프와 센서 값으로 구성됩니다.

### 데이터베이스 초기화 스크립트 설명

- **필요한 모듈 가져오기**：Flask 앱, 데이터베이스 및 SensorData 모델을 가져옵니다.
- **데이터베이스 초기화 함수**：clear_database 함수를 정의하여 SensorData 테이블의 모든 데이터를 삭제하고 변경 사항을 커밋합니다.
- **스크립트 실행**：애플리케이션 컨텍스트에서 clear_database 함수를 실행하여 데이터베이스를 초기화합니다.

### 네트워크 접근 방법

내부 네트워크의 장치에 대한 공용 IP가 없는 경우, 네트워크를 통해 외부에서 이 웹사이트에 접근하려면 네트워크 터널링 소프트웨어를 사용할 수 있습니다. 예를 들어, ngrok 또는 FRP(fast reverse proxy)와 같은 도구를 사용하여 로컬 서버를 공용 웹에서 접근 가능하게 할 수 있습니다.
