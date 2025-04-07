#### 설치 확인

```bash
# 설치되어 있다면 패키지 정보가 출력됩니다.
rpm -q cronie

# 설치되어 있지 않다면, 아래 명령어로 설치할 수 있습니다:
sudo dnf install cronie
```

#### 서비스 관리
설치 후 cron 데몬을 활성화하고 실행하려면 다음 명령어를 사용합니다:

```bash
sudo systemctl enable crond   # 부팅 시 자동 시작 설정
sudo systemctl start crond    # 서비스 시작
sudo systemctl status crond   # 서비스 상태 확인
```

#### 설정 파일

cron의 실행 파일은 일반적으로 **/usr/sbin/crond**에 위치합니다. 

이는 cron 데몬으로, 백그라운드에서 실행되며 예약된 작업을 관리하고 실행합니다.

crond는 cron 데몬의 실행 파일입니다.
- 실행 파일: /usr/sbin/crond

시스템 부팅 시 자동으로 실행되며, 예약된 작업을 수행합니다.


- 사용자별 크론 작업: /var/spool/cron/
    - 각 사용자의 crontab 파일이 저장되는 디렉토리.

시스템 전체 크론 작업:
- /etc/cron.d/: 특정 작업을 정의하는 디렉토리.
- /etc/cron.daily/: 매일 실행되는 스크립트 저장.
- /etc/cron.hourly/: 매시간 실행되는 스크립트 저장.
- /etc/cron.weekly/: 매주 실행되는 스크립트 저장.
- /etc/cron.monthly/: 매월 실행되는 스크립트 저장.

#### 환경 변수 설정:

기본 PATH는 /usr/bin:/bin으로 설정되어 있으며, 필요에 따라 crontab 파일에서 수정 가능합니다.

실행 확인
다음 명령어로 cron 데몬이 실행 중인지 확인할 수 있습니다:

```bash
sudo systemctl status crond
# 만약 실행 중이지 않다면, 아래 명령어로 시작할 수 있습니다:
sudo systemctl start crond
```

이처럼 cron은 주로 /usr/sbin/crond에 위치하며, 관련 설정 파일은 /etc/cron.*와 /var/spool/cron/에 저장됩니다.

### 사용법

1. crontab 파일 열기
    ```bash
    # 이 명령어를 입력하면 현재 사용자의 crontab 설정 파일이 열립니다.
    crontab -e
    ```

2. crontab 문법
crontab 파일은 다음 형식으로 작성됩니다:

    ```text
    분 시 일 월 요일 명령어
    분: 0~59

    시: 0~23

    일: 1~31

    월: 1~12

    요일: 0~7 (0과 7은 일요일)
    ```

예제
```bash
```

3. 예제
```bash
# 설정은 매일 오후 2시 30분에 /home/user/script.sh를 실행합니다.
30 14 * * * /home/user/script.sh

# 매일 오전 9시에 program.py를 Python으로 실행.
0 9 * * * /usr/bin/python3 /home/user/program.py

# 매주 월요일 오전 8시에 스크립트 실행
0 8 * * 1 /home/user/backup.sh

#매시간마다 작업 실행
0 * * * * /home/user/hourly_task.sh

# 매분마다 로그 기록
* * * * * echo "Log entry at $(date)" >> /var/log/mylog.log
```

4. 현재 설정 확인
등록된 작업을 확인하려면:

```bash
crontab -l
```

