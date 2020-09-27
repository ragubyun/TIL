# 작업 끝난 branch를 위한 꿀 커맨드 alias 설정

- `브랜치`에서 작업이 끝난 후
- `merge 대상이 되는 브랜치` 에 merge 가 다 되고
- 해당 `브랜치`를 버리지 않고 계속 쓸 예정일 경우
- 최신화 시켜놓지 않으면
- 다음에 작업하기 전 꼭 최신화를 해야 하나
- 까먹고 하지 않으면
- __귀찮은 일이 생김__

``` shell
alias gbc='git branch --show-current'
alias gcd='git checkout develop'
alias gpp='git pull --prune'
alias gmd='git merge develop --ff-only'
alias gp='git push'
alias done='gbc | pbcopy; gcd; gpp; git checkout $(pbpaste); gmd; gp'
```

> 이제 작업이 끝나면 `done` 명령어로 간단하게 최신화
