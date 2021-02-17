# git

- git clone URL 디렉토리명: 디렉토리 안에 clone

#### git update

```bash
# ubuntu
sudo add-apt-repository ppa:git-core/ppa -y
sudo apt update
sudo apt upgrade
```

#### git init 기본 branch 이름 설정

git 2.28 이후

```bash
git config --global init.defaultBranch main
```

## 커밋 이후의 수정 사항 버리기

| command                    | alias(zsh)        | description                |
| -------------------------- | ----------------- | -------------------------- |
| `git checkout -- FILENAME` | `gco -- FILENAME` | 작업트리에서 되돌리기      |
| `git reset --hard`         | `grhh`            | 스테이징 취소하고 되돌리기 |
