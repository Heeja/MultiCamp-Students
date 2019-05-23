# Docker

### Docker container

#### Docker 실행

docker container run -d -p 8888:8080 Docker ID/



#### Docker container 목록 확인

docker container ls [-a]

- -a: exit된 container도 출력된다.



#### Docker container 중지

docker container stop [container ID]



#### dokcer container 시작

docker container start (restart) [container ID]





실행하는 디렉토리에 .yml 파일이 있어야 docker-compose 명령어를 실행할 수 있다.

docker-compose up

docker-compose up --scale echo=10

--scale: 해당 서비스의 컨테이너를 여러개 실행하는 옵션

** .yml의 services의 이름이 "echo"여야 한다. "echo1"로 되어있으면 여러개의 컨테이너가 생성되지 않는다.

docker-compose log

docker-compose stop

docker-compose pause

docker-compose unpause

docker-compose down





docker container cp ./main.go 36d55ee:/echo/main.go

docker container stop 36d55ee

docker container start 36d55ee

docker container commit --author ""

docker container commit --author "holeonline" --message "My first Docker image Commit." 36d55ee holeonline/echo:latest







docker network ls

container를 실행할 때 네트워크를 지정하지 않으면 기본설정인 bridge로 설정된다.

* Drvier
  * bridge
  * host - NAT
  * null

