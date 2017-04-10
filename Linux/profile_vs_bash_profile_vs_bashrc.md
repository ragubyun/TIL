# .profile, .bash_profile, .bashrc 의 차이점

## Login Shell vs Non-login Shell

위 세 종류의 파일을 이해하려면 각 파일이 로드되는 시점을 이해해야 하는데, 두가지 시점이 있다.

바로 `Login Shell`과 `Non-login Shell`

- Login Shell : 계정과 암호를 입력하여 계정에 로그인 하는 시점.
  - GUI 계정 접속 -> `.profile` 로드(shell의 종류에 관계없이 로드됨)
  - ssh로 원격 접속(shell을 통해서 계정에 접속 하게됨) -> `.bash_profile`(shell이 zsh인 경우 `.zprofile`) 로드
- Non-Login Shell : 계정 로그인과 관계없이 shell을 실행하는 시점.
  - 터미널을 띄움 -> `.bashrc`(shell이 zsh인 경우 `.zshrc`)
  - 터미널이 떠있는 상태에서 창 혹은 탭을 하나 더 띄움 -> 위와 동일함.

> 여기서 '로드'의 의미는 `source` 명령과 같은 의미이다.

각 파일별로 다시 정리하면,

- .profile : 계정에 로그인 할 때 로드된다. shell과 상관없는 것들을 여기에 넣는다.
- .bash_profile : 꼭 bash를 통하여 계정에 로그인 할 때 로드된다.(zsh인 경우 .zprofile) -> shell을 통해서 계정에 접속할 때 필요한 것들을 여기에 넣는다.
- .bashrc : 계정 로그인 과정 없이 bash가 실행될 때마다 로드된다.(zsh인 경우 .zshrc) -> 계정 로그인과 상관없지만 shell이 실행될 때마다 필요한 것들을 여기에 넣는다.

## 각 파일의 위치

- /etc/.profile(모든 계정에 공통으로 로드), ~/.profile(각 계정별로 로드) -> 둘다 순서대로 로드됨
- ~/.bash_profile, ~/.zprofile(각 계정별로 로드)
- ~/.bashrc, ~/.zshrc(각 계정별로 로드)

> 맥 기준으로 작성하였음. 확인해보니 우분투는 동일하나 다른 종류의 리눅스까지는 확인 안해봄..

---

참고 블로그 : [Bash: .profile, .bash_profile, .bashrc](http://dogfeet.github.io/articles/2012/bash-profile.html)