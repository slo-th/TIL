# 생활코딩 linux

## 명령어

- ls : 현재 디렉토리의 파일 목록을 출력
- ls -l : 자세히 보기
- pwd : 현재 디렉토리를 출력
- mkdir 디렉토리명 : 디렉토리 생성
- cd 경로 : 디렉토리 변경
  - 상대경로 : 현재 디렉토리를 기준으로 경로를 표현
    - .. : 부모 디렉토리
    - . : 현재 디렉토리
  - 절대경로 : 최상위 디렉토리(/, root)를 기준으로 경로를 표현
- rm 파일명 : 파일 삭제
- rm -r 디렉토리명 : 디렉토리와 그 안의 모든 디렉토리, 파일 삭제
- 명령어 --help : 명령어의 설명서 출력
- man 명령어: 메뉴얼, 자세한 설명
  - /키워드 : 검색, n 누르면 다음 위치로 이동
- sudo 명령어: super(root) user로 명령 실행
- nano 에디터
  - ^W : 검색
  - ^O : 저장
  - ^X : 나가기
  - ^6 : 범위 선택 . . ?? 단어를 모르겠음
- apt
  - apt-cache search 키워드 : 검색
  - apt-get update : 목록을 최신 상태로 업데이트(갱신)
  - apt-get upgrade : 앱을 최신 버전으로 업그레이드
  - apt-get install 키워드 : 설치
  - apt-get remove 키워드 : 삭제
- wget URL : 파일 다운로드
  - wget -O 파일이름 URL : 파일이름 지정하여 다운로드
- find : 파일 검색
- locate : 파일 검색(mlocate라는 db를 뒤짐 -> sudo updatedb로 업데이트)
- whereis : 실행 파일과 매뉴얼의 위치를 출력 ($PATH와 $MANPATH에서)
- ps : 현재 실행되고 있는 프로세스를 출력
  - ps aux : 백그라운드에서 실행되는 프로세스도 출력

---

## IO Redirection

|명령어|설명|예|
|---|---|---|
> | stdout을 redirect | `ls -l > ls_result.txt`
>> | stdout을 redirect하고 파일 끝에 추가 | `ls -l >> ls_result.txt`
2> | stderr를 redirect | `rm directory/ 2> err.txt`
< | stdin을 redirect | `cat < err.txt`
<<haha | 'haha' 전 까지의 입력을 받음 | `cat <<lol`

ls -al > result.txt 2> error.txt : 명령의 결과는 result.txt에, 에러는 error.txt에 출력

---

## Shell

사용자는 Shell을 통해서 입력을 하고 Kernel은 Shell이 번역한 명령을 수행  

---

## 백그라운드 실행

- Ctrl + z : 실행중인 프로그램을 백그라운드로 보냄  
- jobs 명령어로 백그라운드 프로그램을 볼 수 있음.  
- fg : 다시 실행  
- fg %n : 특정 프로그램을 다시 실행  
- kill %n : 특정 프로그램 종료
- kill -9 %n : 완전 종료
