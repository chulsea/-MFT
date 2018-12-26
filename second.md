### git

### [git](https://git-scm.com/book/ko/v1/Git%EB%A7%9E%EC%B6%A4-Git-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0)

- `Git`은 분산형버전관리시스템(DVCS - Distributed Version Control System)이다.

  소스코드의 버전 관리를 할 수 있고, 이력이 관리된다.

- 사용자 정보 설정

> 메일주소는 반드시 GitHub 계정과 동일해야하고 유저네임도 맞춰주는 것이 좋다.
>
>  `--global` 옵션으로 설정하는 것은 딱 한 번만 하면 된다. 해당 시스템에서 해당 사용자가 사용할 때는 이 정보를 사용한다. (만약 프로젝트마다 다른 이름과 이메일 주소를 사용하고 싶으면 `--global` 옵션을 빼고 명령을 실행한다.)

```bash
$ git config --global user.name "###"
$ git config --global user.email "test@example.com"
```

- git 명령어 자동 색칠

```bash
$ git config --global color.ui true
```

> Mac 에서 한글파일명 깨짐 및 commit 오류 문제 해결
>
> ```bash
> $ git config --global core.precomposeunicode true
> $ git config --global core.quotepath false
> ```

- 설정 확인

```bash
$ git config --global --list
```

---

#### 기초 명령어 정리

```bash
$ git init
$ git add .
$ git commit -m "example"
$ git remote add origin https://github.com/example		# remote 는 한번만
$ git push -u origin master							# 첫 push 이후로는 git push 만 입력
```

##### 1. git 저장소 설정

```bash
$ git init
student@DESKTOP MINGW64 ~/Desktop/TIL (master)
```

**주의!! 반드시 현재 디렉토리에 git을 사용하고 있는지, (master) 표기가 생겼는지 확인 할 것**

#### 2. git add

`git add`는 현재 `working directory` 에서 `commit` 할 목록에 담아놓는 것이다.

그리고 그 목록은 `INDEX(staging area)` 라고 한다.

```bash
$ touch a.txt
$ git add .
```

- `git add a.txt`를 해도 되지만, 우선 `git add .` 을 하자!!
- `.` 은 리눅스 상에서 현재 디렉토리를 뜻한다.

#### 3. git commit

`git commit`은 현재 소스코드 상태를 **스냅샷**을 찍는 것과 동일하다.

`staging area`에 담겨 있는 내용을 이력으로 기록한다.

```bash
$ git status
$ git commit -m "커밋메시지"
```

#### 4. git status

git의 현재 상태를 확인한다. **자주자주 입력하면서 확인하는 습관을 만들어 보자!**

```bash
$ git status
```

------

#### 원격 저장소로 보내기(git push)

사전에 github 에 저장소(repository)를 만들어 놓는다.

1. github 저장소(원격저장소) `url`를 `origin` 이라는 이름으로 설정한다.

```bash
$ git remote add origin https://github.com/example/TIL.git
```

2. 원격 저장소로 보낸다.(push)

```bash
$ git push -u origin master
```
> 한번 push 한 이후로는 `git push` 까지만 입력해도 된다.
- git 학습 사이트
  - [git 입문](https://backlog.com/git-tutorial/kr/intro/intro1_1.html)
  - [git 간편안내서](https://rogerdudler.github.io/git-guide/index.ko.html)
  
#### 웹 크롤링
### 코스피 정보 가져오기

Beautiful Soup library 설치 [doc]
```
$ pip install bs4
```

Beautiful Soup 체험해보기

```python
from bs4 import BeautifulSoup
url = 'https://www.google.co.kr/'
html_doc = requests.get(url).text
soup = BeautifulSoup(html_doc, 'html.parser')

print(soup.prettify())
코스피 가져오기
import requests
from bs4 import BeautifulSoup
import os

token = os.getenv("TELEGRAM_BOT_TOKEN")
method_name = "getUpdates"
url = f'https://api.telegram.org/bot{token}/{method_name}'
update = requests.get(url).json()


chat_id = update["result"][0]["message"]["from"]["id"]
method_name = "sendmessage"

url_cos = "https://finance.naver.com/sise/"
html_cos = requests.get(url_cos).text
soup = BeautifulSoup(html_cos, 'html.parser')
select = soup.select_one('#KOSPI_now') 
msg = "코스피: " + select.text
msg_url = f'https://api.telegram.org/bot{token}/{method_name}?chat_id={chat_id}&text={msg}'

print(msg_url)
print(requests.get(msg_url))
```
