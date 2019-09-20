---
title: CircleCI를 활용해서 build한 파일 서버에 배포하기
date: 2018-09-02 19:28:10
categories:
    - DevOps
---

한창 CI/CD에 대한 연동 작업을 하고 있다. Circle CI를 활용하여 빌드 배포 자동화를 완성해보자. Circle CI는 1개의 컨테이너를 제공하는데, 1달에 1500 시간 사용할 수 있으며, 여러 repository 까지 무료로 제공해준다! 

https://circleci.com

- 작업 흐름은 다음과 같다.

1. git push
2. circle ci 에서 event catch
3. circle ci 빌드 시작
   1. docker를 통해 ubuntu, node 이미지 실행
   2. build
4. 성공한 build 파일을 배포할 서버로 전송
5. 운영 서버에 접속 후 서버 리스타트

## Circle CI 셋팅

- Circle CI에 프로젝트 추가

Circle CI 대시보드 => Add Project 에서 원하는 repository 추가

- Circle CI에 연결된 프로젝트에 SSH Key를 추가

다음 링크를 참고 : https://twpower.github.io/47-deploy-to-server-in-circle-ci

- config.yml 셋팅

````shell
cd 프로젝트 경로로 이동
mkdir .circleci
cd .circleci
sudo vi config.yml
````

다음과 같은 내용을 입력한다

````yaml
# Javascript Node CircleCI 2.0 configuration file
#
# Check https://circleci.com/docs/2.0/language-javascript/ for more details
#
version: 2
jobs:
  build:
    docker:
      # specify the version you desire here
      - image: circleci/node:8

      # Specify service dependencies here if necessary
      # CircleCI maintains a library of pre-built images
      # documented at https://circleci.com/docs/2.0/circleci-images/
      # - image: circleci/mongo:3.4.4

    working_directory: ~/web2.0

    steps:
      # 빌드한 결과를 SSH를 활용하여 운영서버에 전송하기 위한 모듈 install
      - run: sudo apt install -y rsync

      - checkout

      # Download and cache dependencies
      - restore_cache:
          keys:
          - v1-dependencies-{{ checksum "package.json" }}
          # fallback to using the latest cache if no exact match is found
          - v1-dependencies-

      - run: yarn

      - save_cache:
          paths:
            - node_modules
          key: v1-dependencies-{{ checksum "package.json" }}
        
      # run build
      - run: yarn build # 여기에 해당하는 빌드 커맨드를 입력한다!

      - deploy:
          name: SSH File Transfer
          # branch가 master라면 실행, 본인의 branch를 입력할것.
          command: |
            if [ "${CIRCLE_BRANCH}" == "master" ]; then
                ./deploy-test.sh
            fi

````

- deploy-test.sh 생성

````shell
cd 프로젝트 루트
sudo vi deploy-test.sh
chmod +x deploy-test.sh
````

다음 내용을 입력하자

````shell
#!/bin/bash
## file transfer
rsync -avP [circle ci를 통해 빌드된 파일경로] [서버host]@[서버주소]:[빌드된 파일을 저장할 경로] -e "ssh -o StrictHostKeyChecking=no"

## server restart
ssh [서버host]@[주소] -o StrictHostKeyChecking=no <<'ENDSSH'
# 이곳에다가 커맨드를 입력한다.
# 필자의 경우 pm2를 활용하여 서버를 리스타트 시켜주었다.
/home/ubuntu/.yarn-global/bin/pm2 restart web
ENDSSH
````

저장후 sh를 실행가능하도록 만든다

> chmod +x deploy-test.sh

rsync를 활용하는 것이 굉장히 빠르다. (scp를 사용하면 파일전송만 1시간이 걸린다;;) rsync의 옵션의 경우 다음 링크를 참조( http://gyus.me/?p=214 )

>  <<'ENDSSH'   ENDSSH

여기서 ENDSSH는 원하는 글자로 바꿔도 된다. 시작 끝 태그만 동일하면 됌.



자 이제 git 커밋을 자동하면 자동으로 빌드/배포/리스타트가 이루어진다!!

## Reference

circle CI : https://twpower.github.io/47-deploy-to-server-in-circle-ci

rsync : http://gyus.me/?p=214

