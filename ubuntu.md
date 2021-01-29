# ubuntu 설정

## 기본 설정

[링크](https://luckyyowu.tistory.com/409)

### zsh-autosuggestions 관련

우분투 터미널에선 안되던 autosuggestions이 vscode에서 되길래 찾아보니까 solarized dark 테마와 색이 겹쳐서 그런거였다 ... [참고](https://stackoverflow.com/questions/47310537/how-to-change-zsh-autosuggestions-color)

`ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=60'`를 `~/.zshrc`에 추가해줬다.  
`60`은 색 값, 변경 가능 -> [참고](https://coderwall.com/p/pb1uzq/z-shell-colors)

---

## ctrl + alt + up / down 해제하기

dconf-editor를 설치한다

```bash
sudo apt install dconf-editor
```

실행하고 `org > gnome > desktop > wm > keybindings`로 가서

`switch-to-workspace-up`과 `switch-to-workspace-down`을 변경해준 뒤 로그아웃 하고나면 변경 완료
