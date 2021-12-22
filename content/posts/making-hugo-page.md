---
title: "hugo 페이지 만들고 github pages에서 퍼블리싱하기"
date: 2021-12-22T20:46:47+09:00
---

hugo 첫 포스팅 내용은 역시 이게 제일 적절하지 싶어서 써 봅니다.

hugo에 대해서 설명부터 살짝 하자면 정적 페이지 생성기라고 보시면 됩니다.
정적 페이지가 뭔지에 대해선 넘어가겠습니다.

[hugo quickstart guide](https://gohugo.io/getting-started/quick-start/)
먼저 여기 참조하면서 진행하면 되겠습니다.

윈도우판은 인스톨 방법만 조금 다릅니다. powershell쓰시고 [chocolatey](https://chocolatey.org/)로 인스톨하면 됩니다.

```
choco install hugo -confirm
또는 
choco install hugo-extended -confirm
```
으로 인스톨하시면 됩니다. 

그다음 원하는 폴더 안에 /bin, /sites를 만들어주시고
sites폴더 내에서
```
C:\Hugo\Sites> hugo new site example.com
```
하시면 example.com으로 정의된 사이트 하나가 만들어집니다.

다음은 테마 등록입니다. 테마 리스트는 [여기](https://themes.gohugo.io/) 있습니다.

이렇게 새로 만든 example.com폴더에 들어가서 일단 git등록을 하시고
```
git init
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
```
퀵스타트 가이드에서 저렇게 돼 있으니 따라서 등록을 해줍니다. 저는 ink테마를 사용했습니다.

다음은 sites/example.com/config.toml에 
```
theme = \"ananke\" 
```
를 추가해주시면 되겠습니다.

이렇게 만들면 아무것도 없는 페이지가 하나 나오는데 이제 포스트를 추가해 보겠습니다.

```
hugo new posts/my-first-post.md
```

content/posts/my-first-post.md파일이 추가될 것이고
대충 내용물에 아무거나 쓴 다음에

```
hugo server -D
```
하면 내용물이 http://localhost:1313/ 에서 브라우저로 확인할 수 있습니다.

이렇게만 하면 자기 로컬에서만 확인을 할 수 있기 때문에 깃허브에서 제공하는 github pages에서 공짜로 쭈는 도메인을 써 보겠습니다.

위에서 git init을 했기 때문에 로컬에선 git설정이 되어 있는 상태일 것입니다.

[hosting on github](https://gohugo.io/hosting-and-deployment/hosting-on-github/)를 참고하면서 해보겠습니다.

.github/workflows/gh-pages.yml을 같은 패스에 복붙해주시면 되겠습니다.

commit push하기만 하면 hugo가 실행되기 때문에 github에서 github pages설정만 해주면 되겠습니다.

다폴트 도메인은 {유저명}.github.io/{레포지토리명}이므로 config.toml도 맞춰서 변경하면 되겠습니다.