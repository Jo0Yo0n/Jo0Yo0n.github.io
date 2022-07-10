---
layout: post
sidebar: []
title: "Jekyll을 이용한 GitHub Blog 호스팅"
tags: [Blog, Jekyll, Github, Git]

date: 2022-07-10
last_modified_at: 2022-07-10
---

![Alt text](https://img1.daumcdn.net/thumb/R1280x0/?fname=http://t1.daumcdn.net/brunch/service/user/2kPh/image/THnwclNz6inrqYwzxVczKEcEgrQ.jpg)
<br/>우리 블로그 정상영업합니다...

Ruby로 만들어진 Jekyll을 이용해서 GitHub Pages에 블로그를 호스팅 했습니다. GitHub에서는 각 계정 당 하나의 웹페이지를 호스팅 해준다고 합니다.

개발, 공부 정리 블로그를 만들어야겠다는 생각을 한 지는 꽤 됐었는데, 드디어 만들게 됐네요. 다른 블로그 플랫폼도 있었지만, 굳이 GitHub 블로그를 선택한 이유는 높은 자유도 때문입니다. 이런 높은 자유도 때문에 호스팅을 하는 데 꽤 애를 먹기도 했지만, 하나하나 공부하는 재미도 있을 것 같고, 도움도 많이 될 것 같습니다. 아직은 조악하지만, 꾸준히 정리해 나가겠습니다.

---

####Jekyll을 이용한 GitHub 블로그 만들기

우선 Jekyll은 Ruby로 작성되었기 때문에 PC에 Ruby가 설치되어 있어야 합니다. 저는 Windows 운영체제에서 지원하는 WSL2 환경에서 zsh을 따로 설치해서 진행했습니다.

```
#Ubuntu Pakage 관리 툴인 apt update
sudo apt-get update -y && sudo apt-get upgrade -y

#Ubuntu에 최적화된 버전의 Ruby를 제공하는 BrightBox의 repository 사용
#Jekyll 공식 사이트 https://jekyllrb-ko.github.io/docs/installation/windows/ 참조
sudo apt-add-repository ppa:brightbox/ruby-ng
sudo apt-get update
sudo apt-get install ruby2.5 ruby2.5-dev build-essential dh-autoreconf

#Ruby gem 업데이트
#gem은 Ruby에서 지원하는 패키지 시스템으로 리눅스의 apt와 비슷한 역할을 한다고 합니다.
gem update

#jekyll 설치
#중요: sudo 사용 안함
gem install jekyll bundler
```

별거 아니지만 처음 Ruby를 설치할 때 꽤 애를 먹었습니다. 처음이신 분들은 공식 사이트를 보실 때 Quick Start만 보지 마시고, 문서를 모두 읽으시는 것이 좋을 것 같아요.

여기까지 하시면 거의 다 완성입니다. Jekyll은 정적 사이트를 만들기 위한 툴이기 때문에 별다른 설정 없이도 간단하게 사이트 제작이 가능합니다.

저는 대부분의 시간을 여기에서 날려 먹었습니다. 공식 사이트대로 따라가면 기본 테마가 적용되어 있는데, 이미 생성된 Jekyll project에서 다른 테마를 적용하는 부분이 어렵더라고요.

저는 Gem-based Theme Method로 테마 설치를 하려고 했는데, gem 방식으로 설치를 한 후에도 이것저것 설정해야 하는 부분이 있는 것 같습니다. local로는 정상적으로 호스팅이 되는데, GitHub repo에 push해서 확인하려니 GitHub actions에서 build 에러가 뜨는 것을 해결을 못하고 다른 방법을 이용했습니다.

제가 해결한 방법은 원하는 테마의 repo를 clone 해오는 방법입니다. local에 clone을 해 온 뒤, remote 연결을 미리 만들어 놓은 {username}/{username}.github.io로 바꾸어주면 끝입니다. 기본적인 부분이나 배포가 이미 설정되어 있어서 편합니다. 지금 이 블로그도 여기에서 크게 바뀐 부분이 없어요. 나머지는 원하시는 대로 바꾸시면 될 것 같습니다.

---

괜히 시작이 반이라는 말이 있는 게 아닌 것 같습니다. 끝나고 보면 간단한 거였는데, 막상 겪을 때는 참 어렵고 복잡하네요. 늘 멀리서 바라보는 습관을 가져야겠습니다.
