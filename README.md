# SolApi SMS Python Library

SolApi SMS는 SolApi 서비스를 사용하여 SMS, LMS, MMS 메시지를 쉽게 전송할 수 있게 해주는 Python 라이브러리입니다.

## 주요 기능

- SMS, LMS, MMS 메시지 전송
- 단일 및 대량 메시지 전송
- 예약 발송
- 간편한 설정 및 사용

## 설치

pip를 사용하여 라이브러리를 설치할 수 있습니다:

```bash
pip install solapi-sms
```

## 기본 사용 예시

```python
from solapi.config import SolApiConfig
from solapi.sms.message import SMS, MessageSender

# 설정
config = SolApiConfig(api_key="YOUR_API_KEY", secret_key="YOUR_SECRET_KEY")
sender = MessageSender(config)

# SMS 전송
sms = SMS("029302266", "안녕하세요, SolApi SMS 테스트입니다.")
response = sender.send_one(sms, "01012345678")
print(response.json())
```

## 고급 사용 예시

### 예약 발송

```python
from datetime import datetime, timedelta

# 24시간 후 발송
scheduled_time = datetime.now() + timedelta(hours=24)
scheduled_sms = SMS("029302266", "예약 발송 테스트입니다.", scheduled_date=scheduled_time)
response = sender.send_one(scheduled_sms, "01012345678")
```

### 대량 발송

```python
sms = SMS("029302266", "대량 발송 테스트입니다.")
to_numbers = ["01012345678", "01087654321", "01011112222"]
response = sender.send_many(sms, to_numbers)
```

### LMS 발송

```python
from solapi.sms.message import LMS

lms = LMS("029302266", "LMS 본문입니다. 긴 내용을 작성할 수 있습니다.", "LMS 제목")
response = sender.send_one(lms, "01012345678")
```

### MMS 발송

```python
from solapi.sms.message import MMS

mms = MMS("029302266", "MMS 본문입니다.", "MMS 제목", "FILE_ID")
response = sender.send_one(mms, "01012345678")
```

## 설정

`SolApiConfig` 클래스를 사용하여 API 키와 시크릿 키를 설정합니다:

```python
from solapi.config import SolApiConfig

config = SolApiConfig(
    api_key="YOUR_API_KEY",
    secret_key="YOUR_SECRET_KEY",
    domain="api.solapi.com",  # 선택적
    protocol="https",  # 선택적
    prefix=""  # 선택적
)
```

## 개발 및 테스트

프로젝트를 복제한 후, 의존성을 설치하고 테스트를 실행합니다:

```bash
git clone https://github.com/your-username/solapi-sms-python.git
cd solapi-sms-python
pip install -r requirements.txt
python -m unittest discover tests
```

## 라이선스

이 프로젝트는 MIT 라이선스 하에 배포됩니다. 자세한 내용은 `LICENSE` 파일을 참조하세요.