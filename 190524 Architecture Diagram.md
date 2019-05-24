##### Docker Attach vs exec /bin/sh(bash)

**Attach**로 기본으로 설정된 쉘로 접속한 후 exit로 빠져나올 경우 Container는 종료된다.
그렇지만 **exec**로 Container에 접속한 후 exit로 빠져나올 경우 Container는 종료되지 않고 유지된다.



##### Docker Container Data vs Image Data

mysql Image를 통해 Container를 구동하였다.

새로운 table을 추가하고 Container를 Stop, restart하였다.
새로 추가한 table은 남아 있는가??
**남아 있다! Because: 추가한 table의 데이터는 Container에 메모리에 저장되어있다.**

그렇다면 Container를 지우고 다시 mysql Image를 통해 Container를 구동하면
추가한 table은 남아 있는가??
**남아있지 않다!**
**Because: Commit하지 않은 Container의 데이터는 Image에 적용되지 않는다.**



##### Docker를 통해 루비 어플리케이션 구동

Gemfile - 

```
source 'https://rubygems.org'
gem 'sinatra'
```



app.rb - ruby 동작 코드 파일

```
require 'sinatra'	// sinatra를 사용합니다.
require 'socket'	// socket을 사용합니다.

get '/' do		// 특별한 명령이 없다면 아래와 같이 동작 할 것입니다.
  "Hello Jes"
end
```



Dockerfile

```
# 1. 우분투 설치
FROM       ubuntu:16.04
MAINTAINER jes@jes.com
RUN        apt-get -y update

# 2. ruby 설치
RUN apt-get -y install ruby
RUN gem install bundler

# 3. 소스 복사
COPY . /usr/src/app

# 4. Gem 패키지 설치 (실행 디렉토리 설정)
WORKDIR /usr/src/app
RUN     bundle install

# 5. Sinatra 서버 실행 (Listen 포트 정의)
EXPOSE 4567  # 4567 Port번호로 연결
CMD    bundle exec ruby app.rb -o 0.0.0.0
```



Docker Image build & Container Run

```
docker build –t app  .  (t는 tag라는 뜻, .(현재 디렉토리의 Dockerfile 명시) 잊지말기)
docker images (우분투 16.04와 app이 보임)
docker run –d –p 8888:4567 app
docker ps (app Image를 통해 Run한 Container 확인)

```





