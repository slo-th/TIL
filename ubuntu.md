# ubuntu 설정

## 기본 설정

https://luckyyowu.tistory.com/409

---

## ctrl + alt + up / down 해제하기

dconf-editor를 설치한다

```bash
sudo apt install dconf-editor
```

실행하고 `org > gnome > desktop > wm > keybindings`로 가서

`move-to-workspace-up`과 `move-to-workspace-down`을 변경해준 뒤 로그아웃 하고나면 변경 완료
