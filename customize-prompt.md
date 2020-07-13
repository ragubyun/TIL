# prompt 설정

> 이렇게 깔끔하게 바꾸고싶다.

![prompt clean](./images/prompt-not-clean.png)

![prompt not clean](./images/prompt-clean.png)

## zsh

아래 shell script를 .zshrc에 추가

``` shell
function parse_git_branch() {
    git branch 2> /dev/null | sed -n -e 's/^\* \(.*\)/(\1) /p'
}

COLOR_RED=160
COLOR_ORANGE=172
COLOR_SKY=039
COLOR_GREEN=041
COLOR_GREY=008
COLOR_PUPPLE=099

function branch_color() {
    local git_status="$(git status 2> /dev/null)"

    if [[ $git_status =~ "Untracked files" ]]; then
      echo -e $COLOR_GREY
    elif [[ $git_status =~ "Changes not staged for commit" ]]; then
      echo -e $COLOR_RED
    elif [[ $git_status =~ "Changes to be committed" ]]; then
      echo -e $COLOR_ORANGE
    elif [[ $git_status =~ "Your branch is ahead of" ]]; then
      echo -e $COLOR_PUPPLE
    else
      echo -e $COLOR_GREEN
    fi
}

setopt PROMPT_SUBST
export PROMPT='%F{$COLOR_SKY}%~ %F{$(branch_color)}$(parse_git_branch)%F{$COLOR_SKY}$ %f'
```

- `%n` $USERNAME.
- `%~` Current working directory, but if the current working directory starts with $HOME, that part is replaced by a ‘~’.
- `%F (%f)` Start (stop) using a different foreground color.
  - e.g. '%F{cyan}..%f' or '%F{0-255}..%f'
- `%K (%k)` Start (stop) using a different background color. The syntax is identical to that for %F and %f.
  - e.g. '%K{cyan}..%k' or '%K{0-255}..%k'
- `%B (%b)` Start (stop) boldface mode.

more detail : [ZSH Prompt Expansion](http://zsh.sourceforge.net/Doc/Release/Prompt-Expansion.html)

## bash

아래 shell script를 .bash_profile에 추가

``` shell
parse_git_branch() {
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}

# export PS1="\u@\h \W\[\033[32m\]\$(parse_git_branch)\[\033[00m\] $ "
# export PS1="\e[0;32m\u@\w $ \e[0m"
```

- `\u` $USERNAME.
- `\w` Current working directory ($HOME is represented by ~)
- `\e[ (\e[0m)` Begin(Exit) color changes.
  - e.g. '\e[0;32m[....] \e[0m'
  - The first number in color code specifies the typeface.
    - 0 Normal
    - 1 Bold
    - 2 Dim
    - 4 Underlined
  - The second number indicates the color
    - 30 Black
    - 31 Red
    - 32 Green
    - 33 Brown
    - 34 Blue
    - 35 Purple
    - 36 Cyan
    - 37 Light gray

### 참고

- [Change basn prompt linux](https://phoenixnap.com/kb/change-bash-prompt-linux)
- [Add Git Branch Name to Terminal Prompt (Linux/Mac)](https://gist.github.com/joseluisq/1e96c54fa4e1e5647940)
- [Show your git status and branch (in color) at the command prompt](https://coderwall.com/p/pn8f0g/show-your-git-status-and-branch-in-color-at-the-command-prompt)