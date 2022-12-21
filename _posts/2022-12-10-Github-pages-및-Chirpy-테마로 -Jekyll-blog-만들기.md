---
title: Github pages 및 Chirpy 테마로 Jekyll blog 만들기
author: jhbak
date: 2022-12-10 22:55:00 +0900
categories: [Blogging, jekyll]
tags: [TIL, chirpy, theme]
render_with_liquid: false
---

# Jekyll Chirpy 테마로 TIL 블로그 제작하기

본 포스팅은 MAC 환경에서 Jekyll Chirpy 테마를 사용하여 Github pages로 호스팅 되는 블로그를 개설하는 것에 대해 다루고 있습니다.

로컬 편집 툴은 VScode를 사용했으며, 위 조건이 다른 경우 설치 방법이 달라질 수 있습니다.

## 사전 준비 사항

---

### 1) 미리 설치할 것

[Jekyll Docs](https://jekyllrb.com/docs/installation/){:target="\_blank"} 및 [The fastest and easiest way to install Ruby on a Mac in 2022](https://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/){:target="\_blank"} 페이지를 참고하여 아래의 필요 사항을 설치해두어야 합니다.

대부분의 경우 아래 커맨드를 터미널에 순서대로 입력한다면 이상 없이 설치 될 것입니다.

- `Homebrew` 설치:

```terminal
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

- `Chruby` 및 `Ruby-install` 설치:

```terminal
brew install chruby ruby-install xz
```

- `Ruby` 및 `RubyGems` 설치:

```terminal
ruby-install ruby
```

<!-- prettier-ignore -->
> RubyGems는 Ruby와 함께 설치된다. 
{: .prompt-info}

- `Ruby` 설치 확인:

```terminal
ruby --v
```

- `Jekyll` 설치:

```terminal
gem install jekyll
```

- `Bundler` 설치:

```terminal
gem install bundler
```

- `Git` 설치:

```terminal
brew install git
```

- VScode

```terminal
brew install --cask visual-studio-code
```

### 2) 진행 절차 미리보기

1. Chirpy Repository Fork 하기
2. Local 환경으로 Clone 하기
3. Local 환경에서 Test 하기
4. 원격 저장소로 Local 변경사항 push 하기
5. Github pages 배포 확인하기

<!-- prettier-ignore -->
> 앞으로 어떤 절차가 예정되어 있는지 미리 알고있으면 예상치 못하게 절차가 꼬이는 문제를 예방할 수 있다.
{: .prompt-tip}

## Chirpy 테마로 Jekyll 블로그 설치

---

### Stetp 1. Chirpy Repository Fork

[Chirpy theme Github Repo](https://github.com/cotes2020/jekyll-theme-chirpy)에서 내 원격 저장소로 Chirpy 테마 파일을 복사해서 가져옵니다.
저장소 우측 상단의 `Fork > Create a new fork` 클릭 해줍시다.

![Fork chirpy repo](/assets/posting/Github%20pages%20%EB%B0%8F%20Chirpy%20%ED%85%8C%EB%A7%88%EB%A1%9C%20Jekyll%20blog%20%EB%A7%8C%EB%93%A4%EA%B8%B0/1.png)

Repository name을 `<Github username>.github.io`로 변경후 Fork 완료 해줍니다.

<!-- prettier-ignore -->
> 1.  저장소 이름을 github username으로 변경하는 것은 github pages를 사용해서 우리의 블로그를 호스팅 하기 위해서 입니다.
> 2.  별도의 호스팅을 사용할 경우 원하는 이름을 사용할 수 있습니다.
> 3.  저장소의 이름은 추후 Setting에서 언제든지 변경할 수 있습니다. 
{: .prompt-info}

![Fork chirpy repo](/assets/posting/Github%20pages%20%EB%B0%8F%20Chirpy%20%ED%85%8C%EB%A7%88%EB%A1%9C%20Jekyll%20blog%20%EB%A7%8C%EB%93%A4%EA%B8%B0/2.png)

### Stetp 2. Local 환경으로 Clone 하기

앞으로 이것저것 많은 것들을 수정하게 될텐데 Github에 올라가있는 상태로는 소스코드의 편집이 쉽지 않습니다.

VScode로 소스코드를 편리하게 편집하기 위해서 원격 저장소에 Fork한 저장소를 Local 환경으로 Clone 해서 가져올 예정입니다.

Fork 해온 저장소에서 `Code > REPO_URL` 복사해줍니다.

![Copy repo URL](/assets/posting/Github%20pages%20%EB%B0%8F%20Chirpy%20%ED%85%8C%EB%A7%88%EB%A1%9C%20Jekyll%20blog%20%EB%A7%8C%EB%93%A4%EA%B8%B0/3.png)

터미널에 아래의 명령어를 입력하면 Clone을 실행할 수 있습니다.
`<REPO_URL>` 위치에 <u>위의 이미지에서 복사한 URL</u>을, `<DIR>` 위치에 <u>원하는 작업 위치</u>를 입력합니다.

```
git clone <REPO_URL> <DIR>
```

<!-- prettier-ignore -->
> `<DIR>` 는 생략할 수 있습니다. 생략시 현재 위치에서 실행 
{: .prompt-tip}

ex) 변수 예시

- `<REPO_URL>` → https://github.com/pjh1821/pjh1821.github.io.git
- `<DIR>` → C:\\Users\\Documents

### Stetp 3. Chirpy theme 파일 초기화 하기

Clone 받은 소스코드 Root 위치에서 터미널에 아래 커맨드를 입력하면 몇가지 파일이 삭제됩니다.
제작자가 DEMO로 넣어둔 내용 등을 삭제해서 바로 사용할 수 있도록 하는 명령어인 것 같습니다.

```
bash tools/init.sh
```

이상태에서 일단 한번 커밋해줍니다.

```
git add .
git commit -m "Create TIL blog powered by jekyll Chirpy theme"
```

### Stetp 4. 로컬 환경에서 TEST 하기

변경된 Local 파일이 서버에서 제대로 구동되는지 확인하기 위해서 아래의 명령어를 실행해줍니다.

```
bundle
jekyll serve
```

아래와 같이 출력된다면 정상 동작 되고 있는 것입니다.
표시된 IP 주소를 웹 브라우저에 입력하면 생성된 블로그를 확인 할 수 있습니다.

![Local test](/assets/posting/Github%20pages%20%EB%B0%8F%20Chirpy%20%ED%85%8C%EB%A7%88%EB%A1%9C%20Jekyll%20blog%20%EB%A7%8C%EB%93%A4%EA%B8%B0/4.png)

### Stetp 5. Local 변경사항 Github 저장소로 PUSH 하기

로컬에서 문제없이 잘 동작하는 것을 확인했으니 원격 저장소로 변경사항을 업로드 합니다.

```
git push origin master
```

<!-- prettier-ignore -->
> - github는 master 브랜치를 main으로 변경했습니다.  
>   하지만 Chirpy 테마는 master를 사용하고 있어서 master 브랜치를 사용합니다.
> - main으로 브랜치 명을 변경할 수 있지만 원본 변경사항을 merge 할 때 문제가 발생할 수 있을 것 같아서 손대지 않았어요.
{: .prompt-info}
> clone 해서 생성된 프로젝트는 remote 명령어를 사용하지 않아도 이미 원격 저장소가 지정되어 있습니다.
{: .prompt-tip}

### Stetp 6. `github.io`로 변경사항 반영 및 배포 확인하기

원격 저장소로 변경사항 업로드가 완료되었다면 잠시 후 pages를 통해서 확인 가능합니다.
`<username>.github.io` 를 웹 브라우저에 입력 후 제대로 출력되는지 확인할 수 있습니다.

![Check deployment](/assets/posting/Github%20pages%20%EB%B0%8F%20Chirpy%20%ED%85%8C%EB%A7%88%EB%A1%9C%20Jekyll%20blog%20%EB%A7%8C%EB%93%A4%EA%B8%B0/5.png)

위의 이미지와 같이 텅빈 페이지가 출력되었나요? 축하합니다.  
Jekyll Chirpy 테마 및 Github pages를 활용하여 블로그 생성이 완료되었습니다.

## Reference

---

- [하얀눈길 블로그 포스팅](https://www.irgroup.org/posts/jekyll-chirpy/)
- [Chirpy DEMO - Getting started](https://chirpy.cotes.page/posts/getting-started/)
- [pages에 jekyll theme 추가 하는 방법 docs](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll)
