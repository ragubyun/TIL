# prompt 설정

> 이렇게 깔끔하게 바꾸고싶다.

![sample prompt](./images/sample-prompt.png)

## zsh

``` shell
$ export PROMPT='%F{cyan}%n@%~ $ %f'
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

``` shell
$ export PS1="\e[0;32m\u@\w $ \e[0m"
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

참고: [Change basn prompt linux](https://phoenixnap.com/kb/change-bash-prompt-linux)