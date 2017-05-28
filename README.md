# asp.net-core-docker-explain
asp.net core와 도커 설치 및 설정

>(우분투 14.40 기준)

* 도커 설치하기
  * curl -s https://get.docker.com/ | sudo sh

* 도커 관리자 권한 실행
  * sudo usermod -aG docker $USER

* 도커 버전 확인
  * docker version

* 컨테이너 검색
  * docker search [image name]

* 닷넷 코어 컨테이너 설치
  * docker run --rm -it microsoft/dotnet

* 도커 컨테이너 옵션
|옵션	 |설명                                   |
|:-------|--------------------------------------|
|-d	     |detached mode 흔히 말하는 백그라운드 모드    |
|-p	     |호스트와 컨테이너의 포트를 연결 (포워딩)       |
|-v	     |호스트와 컨테이너의 디렉토리를 연결 (마운트)     |
|-e	     |컨테이너 내에서 사용할 환경변수 설정          |
|–name	 |컨테이너 이름 설정                        |
|–rm	     |프로세스 종료시 컨테이너 자동 제거           |
|-it	 |-i와 -t를 동시에 사용한 것으로 터미널 입력을 위한 옵션|
|–link	 |컨테이너 연결 [컨테이너명:별칭]            ||

* 도커 컨테이너 목록 확인
  * docker ps [OPTIONS]
    * -a, --all

* 도커 컨테이너 중지
  * docker stop [OPTIONS] CONTAINER [CONTAINER...]

* 도커 컨테이너 제거
  * docker rm [OPTIONS] CONTAINER [CONTAINER...]
  * docker rm -v $(docker ps -a -q -f status=exited) (중지된 도커 모두 삭제)

* 도커 다운로드한 컨테이너 이미지 확인
  * docker images [OPTIONS] [REPOSITORY[:TAG]]

* 도커 컨데이터 이미지 다운로드
  * docker pull [OPTIONS] NAME[:TAG|@DIGEST]

* 도커 이미지 삭제
  * docker rmi [OPTIONS] IMAGE [IMAGE...]

* 도커 로그 확인
  * docker logs [OPTIONS] CONTAINER
    * -f : 전체로그
    * --tail : 일정로그 (--tail 10 ${WORDPRESS_CONTAINER_ID})

* 도커 컨테이너 실행
  * docker restart [CONTRAINER ID]
  * docker start [CONTAINER ID]

* 컨테이너 접속
  * docker exec -it  [CONTAINER ID] /bin/bash 
  * 접속 중 exit (컨테이너 중지 및 터미널 해제)
  * ctrl + p, ctrl + q (컨테이너 미중지 및 터미널 해제)
  
* 컨테이너 이미지 생성
  * docker diff [CONTAINER ID] (변경사항 확인)
  * docker commit [CONTAINER ID] [레파지토리명/이미지이름:이미지테크]

# Docker remote api
* Setting
   1. sudo vi /lib/systemd/system/docker.service
   2. ExecStart=/usr/bin/docker -d -H fd:// **$DOCKER_OPTS**
   3. [없으면 추가] EnvironmentFile=/etc/default/docker
   4. sudo vi /etc/default/docker
   5. DOCKER_OPTS="-H tcp://0.0.0.0:[임의포트]"
   6. systemctl daemon-reload
   7. systemctl restart docker
   8. [실행확인] ps aux | grep docker
      