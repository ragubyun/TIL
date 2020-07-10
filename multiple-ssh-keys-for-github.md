# Github 여러 계정에서 SSH key 등록해서 사용하기

먼저 SSH 키를 각각 생성

``` shell
$ ssh-keygen -t rsa -C "account1@gmail.com" # 구별을 위한 메일주소
$ ssh-keygen -t rsa -C "account2@gmail.com"
```

그러면 아래와 같이 두개의 키 쌍이 생기고(파일명은 지정한 대로)

``` shell
~/.ssh/id_rsa_github-account1
~/.ssh/id_rsa_github-account1.pub
~/.ssh/id_rsa_github-account2
~/.ssh/id_rsa_github-account2.pub
```

두개의 키를 등록

``` shell
$ ssh-add ~/.ssh/id_rsa_github-account1
$ ssh-add ~/.ssh/id_rsa_github-account2
```

그리고 등록되었는지 확인

``` shell
$ ssh-add -l
```

``` shell
~~~ SHA256:~~~~~~~~~~~ account1@gmail.com (RSA)
~~~ SHA256:~~~~~~~~~~~ account2@gmail.com (RSA)
```

참고로 삭제는

``` shell
$ ssh-add -D
```

그리고 `~/.ssh/config` 파일 생성

``` shell
#account1@gmail.com account
Host github.com-account1
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_github-account1

#account2@gmail.com account
Host github.com-account2
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_github-account2
```

그리고 SSH connection 테스트

``` shell
$ ssh -T git@github.com-account1
$ ssh -T git@github.com-account2
```

결과 확인

``` shell
Hi account1! You've successfully authenticated, but GitHub does not provide shell access.
Hi account2! You've successfully authenticated, but GitHub does not provide shell access.
```

마지막으로 각 Github 계정에 SSH 공개키를 등록하고 각 계정의 repository의 remote 주소 설정을 아래와 같이 하면,


> git@github.com-**account1**:account1/some-repository.git

> git@github.com-**account2**:account2/some-repository.git

각 remote에 접근할 때 `~/.ssh/config` 파일에 설정되어 있는 *Host*와 일치하는 *HostName*의 ssh key를 가지고 접근한다.

참고로 ssh url에 해당 *Host*를 넣어서 clone 하는 것도 가능하며, 그렇게 하면 따로 remote url을 변경하지 않아도 되서 편하다.

``` shell
$ git clone git@github.com-account1:account1/some-repository.git
$ git clone git@github.com-account2:account2/some-repository.git
```
