---
title: EC2 우분투 Node 개발환경 셋팅
date: 2018-08-25 19:28:10
categories:
    - etc
---

### ec2 셋팅

- 보안그룹 
  - SSH / Postgresql / HTTP / HTTPS  허용

- 탄력적 IP 생성 후 인스턴스 셋팅

- ssh 접속

우분투의 경우 ubuntu@를 붙임

ssh -i */path/my-key-pair*.pem ubuntu@*public-dns-hostname*

https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/TroubleshootingInstancesConnecting.html#TroubleshootingInstancesConnectingMindTerm

### root password 변경

> sudo passwd root

### locale 설정

```powershell
locale
sudo apt install language-pack-ko
sudo locale-gen ko_KR.UTF-8
sudo dpkg-reconfigure locales
sudo update-locale LANG=ko_KR.UTF-8 LC_MESSAGES=POSIX
```

### timezone 설정

> sudo ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime

KST 확인

> date

### vim 8.0

> sudo add-apt-repository ppa:jonathonf/vim
>
> sudo apt-get update
>
> sudo apt-get install vim vim-gtk

### zsh

>  sudo apt install zsh
>
> sudo vi /etc/pam.d/chsh

auth       required   pam_shells.so  : required => sufficient로 변경

> chsh -s /usr/bin/zsh 
>
> curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh

>  sudo reboot
>
> echo $SHELL

위 커맨드로 /usr/bin/zsh가 나오면 okay.





## node

```bash
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs
```

### nvm

- curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash

- >  sudo vi ~/.zshrc 에서 아래 내용 추가
  >
  > export NVM_DIR="$HOME/.nvm"
  >
  > [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"

### 이미지 편집

이미지 편집 기능이 필요하지 않으면 스킵.

c compiler, libpng, zlib

> sudo apt install graphicsmagick build-essential

libjpeg

- wget https://www.ijg.org/files/jpegsrc.v9c.tar.gz
- tar xzf jpegsrc.v9c.tar.gz
- cd jpeg-9b
- ./configure --prefix=/usr/local/libjpeg
- make
- sudo make install

graphicmagick 의 gm 커맨드와 oh-my-zsh gm 커맨드가 겹치므로

OH-MY-ZSH의 gm을 제거해줘야 한다 : 

> vi  ~/.oh-my-zsh/plugins/git/git.plugin.zsh 에서 alias gm 주석 처리

### global yarn

- curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add    
- echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
- sudo apt update
- sudo apt install yarn
- yarn config set prefix ~/.yarn-global
- yarn config get prefix
- cat ~/.yarnrc
- path
  - vi ~./.zshrc 추가 => export PATH="$PATH:`yarn global bin`"

> #test 해보장
>
> yarn global add knex gm pg imagemagick

### postgresql

- wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O- | sudo apt-key add -
- echo "deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main" | sudo tee /etc/apt/sources.list.d/postgresql.list
- sudo apt-get update && sudo apt-get install postgresql
- sudo service postgresql start
- sudo su - postgres
- psql
- CREATE USER bglamour WITH PASSWORD 'bglamour';
- create database bglam_local;
- psql postgres -U username : postgres DB에 username 롤로 접속





