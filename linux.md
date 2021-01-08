# 생활코딩 linux

## 명령어

- `ls` : 현재 디렉토리의 파일 목록을 출력
- `ls -l` : 자세히 보기
- `pwd` : 현재 디렉토리를 출력
- `mkdir` 디렉토리명 : 디렉토리 생성
- `cd 경로` : 디렉토리 변경
  - 상대경로 : 현재 디렉토리를 기준으로 경로를 표현
    - .. : 부모 디렉토리
    - . : 현재 디렉토리
  - 절대경로 : 최상위 디렉토리(/, root)를 기준으로 경로를 표현
- `rm 파일명` : 파일 삭제
- `rm -r 디렉토리명` : 디렉토리와 그 안의 모든 디렉토리, 파일 삭제
- `명령어 --help` : 명령어의 설명서 출력
- `man 명령어`: 메뉴얼, 자세한 설명
  - /키워드 : 검색, n 누르면 다음 위치로 이동
- `sudo 명령어`: super(root) user로 명령 실행
- nano 에디터
  - ^W : 검색
  - ^O : 저장
  - ^X : 나가기
  - ^6 : 범위 선택 . . ?? 단어를 모르겠음
- apt
  - `apt-cache search` 키워드 : 검색
  - `apt-get update` : 목록을 최신 상태로 업데이트(갱신)
  - `apt-get upgrade` : 앱을 최신 버전으로 업그레이드
  - `apt-get install` 키워드 : 설치
  - `apt-get remove` 키워드 : 삭제
- `wget URL` : 파일 다운로드
  - `wget -O 파일이름 URL` : 파일이름 지정하여 다운로드
- `find` : 파일 검색
- `locate` : 파일 검색(mlocate라는 db를 뒤짐 -> sudo updatedb로 업데이트)
- `whereis` : 실행 파일과 매뉴얼의 위치를 출력 ($PATH와 $MANPATH에서)
- `ps` : 현재 실행되고 있는 프로세스를 출력
  - `ps aux` : 백그라운드에서 실행되는 프로세스도 출력
- `tail -f` : 파일의 마지막 10줄을 출력하되 내용이 추가될 때마다 출력
- `rsync` : 동기화(remote sync)

---

## IO Redirection

|명령어|설명|예|
|---|---|---|
`>` | stdout을 redirect | `ls -l > ls_result.txt`
`>>` | stdout을 redirect하고 파일 끝에 추가 | `ls -l >> ls_result.txt`
`2>` | stderr를 redirect | `rm directory/ 2> err.txt`
`<` | stdin을 redirect | `cat < err.txt`
`<<haha` | 'haha' 전 까지의 입력을 받음 | `cat <<lol`
`2>&1` | stderr를 stdout으로 redirect | `rm directory >> error.txt 2>&1`

`ls -al > result.txt 2> error.txt` : 명령의 결과는 result.txt에, 에러는 error.txt에 출력

---

## Shell

사용자는 Shell을 통해서 입력을 하고 Kernel은 Shell이 번역한 명령을 수행

|쉘|경로|
|---|---|
|bash| ~/.bashrc|
|zsh | ~/.zshrc |
쉘이 시작할 때 실행되는 명령이 적힌 파일

---

## 백그라운드 실행

- Ctrl + z : 실행중인 프로그램을 백그라운드로 보냄  
- `jobs` 명령어로 백그라운드 프로그램을 볼 수 있음.  
- `fg` : 다시 실행  
- `fg %n` : 특정 프로그램을 다시 실행  
- `kill %n` : 특정 프로그램 종료
- `kill -9 %n` : 완전 종료
- `명령 &` : 명령을 백그라운드에서 실행

## daemon

시스템이 켜져 있는 동안 계속 작동하는 프로세스  

자동으로 시작되게 해야 할 경우  
CLI환경 - `/etc/rc3.d/`  
GUI환경 - `/etc/rc5.d/`  
위 디렉토리에서 링크를 생성  
접두사 S: 시작, K: 시작하지 않음

```zsh
/etc/init.d/데몬이름.d start
service 데몬이름 start
invoke-rc.d 데몬이름 start
```

daemon 시작 명령어

## cron

정기적으로 명령을 실행시켜주는 프로그램  
`crontab -e` 명령으로 편집할 수 있다.

|키워드|의미|범위|용법| |
|---|---|---|---|---|
|`m`|minite|0-59|n : n분에 실행| */n : n분마다 실행|
|`h`|hour|0-23|n: n시에 실행| */n : n시간마다 실행|
|`dom`|day of month|1-31|
|`mon`|month|1-12|
|`dow`|day of week|0-6, 0=SUN|
|`command`|command||

[자세한 정보](https://crontab.guru/)

## 사용자

|명령어|설명|
|---|---|
| `id` | 유저와 그룹의 id를 출력하는 명령어 uid = userid / gid = groupid|
|`who` | 현재 시스템에 접속중인 유저의 정보를 출력하는 명령어
|`su` | 사용자를 변경하는 명령어
|`passwd` | 암호를 변경하는 명령어
|`useradd` | 사용자 생성, 모든 설정을 명시해야함.
|`adduser` | 기본 설정(/etc/adduser.conf)으로 사용자를 생성한다.
|`usermod` | 사용자를 수정(modify)

## 권한

d|rwxrwxr-x | 4 | sloth sloth | 4.0K | 1월  7 23:57 | TIL

1. d : type(d = directory, - = file, l = link)
2. rwxrwxr-x: access mode(3개씩 나눠서 owner, group, other)
3. 4 : ??
4. sloth sloth : owner, group
5. 4.0K : 용량
6. 1월 7 23:57 : 생성된 시각
7. TIL : 디렉토리/파일명

|키워드|의미|파일|디렉토리|
|---|---|---|---|
|r|read|읽기|읽기|
|w|write|쓰기|쓰기|
|x|execute|실행|접근(cd)

`chmod` : 권한을 변경하는 명령어  

```zsh
chmod o+r example.txt # other에 read 추가
chmod u-x example # user(owner)에 execute 제거
chmod 777 example # rwxrwxrwx 로 설정
```

[chmod wikipedia](https://ko.wikipedia.org/wiki/Chmod)

## 인터넷, 네트워크, 그리고 서버

client와 server가 통신한다... client는 request를 보내고 server는 response를 보낸다.  
google.com으로 접속하면 dns(domain name system) server를 조회하여 google.com의 ip address로 접속

### apache 웹 서버

웹 서버는 기본적으로 80번 포트를 사용  
설정 파일: `/etc/apache2/apache2.conf`  
document root: `var/www/html/`  
log 파일 : `/var/log/apache2/access.log error.log`  

### ssh

패키지: openssh-client openssh-server

`ssh 사용자@address` : 원격 접속

### hosts

dns server를 거치기 전에 hosts파일을 먼저 보고 일치하는 domain name이 없으면 dns server를 본다.

`/etc/hosts`에 위치

ip와 domain name을 적음  
`127.0.0.1  google.com`

해커의 공격 대상이 되기도 한다

## ssh public private key

- `ssh-keygen`: ssh 공개키 비공개키 생성 명령어
- `ssh-copy-id`: 공개키를 대상 authorized_keys에 추가함
