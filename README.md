# HallymFestival2023-Frontend

<div align="center">
    <img width="329" alt="image" src="https://user-images.githubusercontent.com/53892427/227495220-6f11cc27-120c-49d0-b894-b09f62f34bed.png" />


[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2FVoluntain-SKKU%2FHallymFestival2023-Backend-&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com)

</div>

## Front-end Team ✨

|                                      오소현                                      |                                      김경재                                      |
| :------------------------------------------------------------------------------: | :------------------------------------------------------------------------------: |
| <img width="160px" src="https://avatars.githubusercontent.com/u/53892427?v=4" /> | <img width="160px" src="https://avatars.githubusercontent.com/u/35104213?v=4" /> |
|                  [@osohyun0224](https://github.com/osohyun0224)                  |                   [@PortalCube](https://github.com/PortalCube)                   |
|                          한림대학교 빅데이터학과 20학번                          |                          한림대학교 빅데이터학과 20학번                          |

## Description

2023 한림대학교 비봉축전 웹어플리케이션 - PWA 삽질기 입니다.

안녕하세요, 저거 구현한 주인장 [@osohyun0224](https://github.com/osohyun0224) 입니다.

Vue.js 프로젝트에서 PWA를 구현하는 과정을 담은 안내서를 작성하고자 삽질기를 리드미에 작성합니다..

## 📌 PWA Vue.js 적용 계기
현재 하는 프로젝트가 본인 학교 전체 학생들을 대상으로 축제 웹사이트를 제작하고 있기 때문에, pwa의 offline, push message와 같은 기능을 넣고 싶어서 프로젝트에 pwa를 구현하게 되었습니다... 
결과를 스포하자면 남은 일정에 비해 프론트 개발일정이 너무 빡세서 pwa를 해당 프로젝트에 구현하지는 않습니다만 그래도 해당 기능을 구현하는 사람들을 위해 제가 개발하면서 고민했던 과정을 기록하고자 합니다.

## (1) PWA란?
Progressive Web Application의 약자인 PWA는, 웹으로 개발된 사이트를 앱처럼 사용할 수 있는 것입니다. 반응형이나, 모바일 화면을 고려하지 않은 웹사이트를 앱처럼 보이기에는 어려워서 이 점을 고려하여 웹사이트를 개발해야합니다.

PWA의 장점은 안드로이드와 아이폰 모두 앱으로 구현이 가능하다는 것입니다. 제가 구현을 공부하면서 아이폰에서 실행되려면 현재 16.4 버전 이상이어야 한다고 하는데 아이폰유저들이 필수로 해당 버전까지 업데이트를 해야한다는 점이 단점입니다. 

## (2) PWA 개발하기 전 준비되어야할 사항 필수 항목 3가지!!
#### 📌 Manifest.json 파일
#### 📌 Serveice Worker 준비
#### 📌 HTTPS 프로토콜 준비

### [1] Manifest.json 파일 작성
> 먼저, 웹앱매니페스트란, PWA의 설치와 앱의 구성 정보를 담고 있는 json 설정파일이다! 브라우저가 manifest파일을 읽어서 해당 웹사이트가 pwa로 구현된 것이라고 인식하므로 매우 중요한 파일!

#### [ 작성방법 ]

본인이 직접 작성할 수 도 있고, 공식 사이트의 도움을 받을 수도 있다. [PWA Manifest Generator] (https://www.simicart.com/manifest-generator.html/) 를 이용하면 manifest.json파일 코드를 직접 작성하여주고, 해당 파일에 필요한 아이콘들을 얻을 수 있다. 해당 아이콘들을 다운받아 폴더 안에 넣어주어야 한다.

- short_name : 여기에는 해당 웹사이트가 앱으로 구현되었을때, 앱의 이름이 된다. 나는 Hallym_Festival로 하였고 실제 앱으로 다운 받아 졌을때 아이콘 화면이다.

![](https://velog.velcdn.com/images/osohyun0224/post/773b0c49-70d6-4e42-9260-c31a7add346a/image.png)

- name: name이 있어야 배너를 설치 할 수 있다. 이것은 설치 배너에 표시되는 이름이며 검색의 키워드로 사용된다.

- icons : 이것은 위에 말했던 아이콘인데, 192px크기 이상의꺼는 무조건 필수로 넣어야한다. 

#### [내 코드 보기]
(1)  manifest.json 파일
```
{
  "theme_color": "#3eaf7c",
  "background_color": "#3eaf7c",
  "display": "standalone",
  "scope": "/",
  "start_url": "/",
  "name": "Hallym_Festival", // 내 프로젝트 이름
  "short_name": "PWA",
  "icons": [
    {
      "src": "icons/icon-192x192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "icons/icon-256x256.png",
      "sizes": "256x256",
      "type": "image/png"
    },
    {
      "src": "icons/icon-384x384.png",
      "sizes": "384x384",
      "type": "image/png"
    },
    {
      "src": "icons/icon-512x512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```
(2) 프로젝트 안에 파일 구조도 

![](https://velog.velcdn.com/images/osohyun0224/post/7285a084-b235-4340-83d4-eed74c124fb3/image.png)

무조건 public폴더 안에 icons 폴더를 만들어 아이콘들 크기별로 넣어주고, manifest.json 파일 작성해준다. index.html도 안에 반드시 생성해줘야한다.


(3) public/index.html
```
<!DOCTYPE html>
<html lang="ko">
  <head>
    <link rel="manifest" href="manifest.json">
    <link rel="manifest" href="install.webmanifest">
    //이코드는 밑에 (4)번 만들어주면 넣어주세요
    <link rel="apple-touch-icon" sizes="192x192" href="/icons/icon-192x192.png">
    <link rel="apple-touch-icon" sizes="256x256" href="/icons/icon-256x256.png">
    <link rel="apple-touch-icon" sizes="384x384" href="/icons/icon-384x384.png">
    <link rel="apple-touch-icon" sizes="512x512" href="/icons/icon-512x512.png">
  </head>
  </html>
```
public 폴더 아래에 있는 index.html에 위의 코드를 반드시 넣어줘야한다.

(4) public/install.webmanifest 파일
```
{
    "background_color": "purple",
    "description": "Shows random fox pictures. Hey, at least it isn't cats.",
    "display": "fullscreen",
    "icons": [
      {
        "src": "icons/icon-192x192.png",
        "sizes": "192x192",
        "type": "image/png"
      }
    ],
    "name": "한림대 비봉축전", 
    "short_name": "한림대",
    "start_url": "/"
  }
```

이 파일은 manifest.json파일 넣고 크롬 브라우저에서 실행안되길래 뭐가문제야! 하고 찾아보다가 오류를 해결하였습니다.
manifest.json 파일 크롬에서 안읽히면 위의 webmanifest파일 작성해주세요 얘도 같은 public 폴더 안에 넣어줘야합니다.

#### [크롬에서 manifest.json 돌아가는거 확인]
먼저 해당 프로젝트를 로컬에서 돌릴 때, 이거는 무조건 크롬에서 확인해야하므로, **크롬에서 로컬을** 돌려주세요!

해당 로컬페이지에서 f12를 눌러 manifest.json이 잘 인식되는 지 확인한다.
<잘 인식하지 못하는 예시>
![](https://velog.velcdn.com/images/osohyun0224/post/fe6e879d-bccf-415e-9ec8-9b30999b0e24/image.png)
위의 화면은 브라우저가 manifest.json파일을 인식하지 못하는 화면이다. 저거 뜨면 위의 (4) webmanifest파일 당장 작성하러 가십시오

<잘 인식될 때의 화면>
![](https://velog.velcdn.com/images/osohyun0224/post/f6152eb3-d7e9-4e5d-b55d-380b2f0948ff/image.png)
manifest.json 해결~

### [2] Service Worker 적용기
> 서비스워커의 핵심 기능은 웹 브라우저 안에 있지만 웹 페이지와는 분리돼서 실행되는 백그라운드 프로그램이며, 이를 이용하면 푸시 알림이나 사용자들에게 특정 메시지를 보낼 수 있다!

제일 중요하다고 볼 수 있는 서비스워커를 적용해보겠습니다.

먼저, 해당 프로젝트에 서비스 워커를 설치해야합니다.
```
npm i register-service-worker
npm i @vue/cli-plugin-pwa
```

#### [내 코드 보기]
(1) 파일 구조도부터 살펴보기

![](https://velog.velcdn.com/images/osohyun0224/post/08432cee-5ac5-47d5-a990-3222fb34cdb3/image.png)

![](https://velog.velcdn.com/images/osohyun0224/post/01f8044d-e11b-492c-bcf2-9f4648739b22/image.png)

위의 구조들 처럼 서비스워커 파일들이 들어가있어야합니다.

(2) registerServiceWorker.js 파일 **(src파일 밑에)**

아래의 코드는 배포용이다!
```
import { register } from 'register-service-worker'

/*if (process.env.NODE_ENV === 'production') { 
  register(`/service-worker.js`, {
    ready () {
      console.log(
        'App is being served from cache by a service worker.\n' +
        'For more details, visit https://goo.gl/AFskqB'
      )
    },
    registered () {
      console.log('Service worker has been registered.')
    },
    cached () {
      console.log('Content has been cached for offline use.')
    },
    updatefound () {
      console.log('New content is downloading.')
    },
    updated () {
      console.log('New content is available; please refresh.')
    },
    offline () {
      console.log('No internet connection found. App is running in offline mode.')
    },
    error (error) {
      console.error('Error during service worker registration:', error)
    }
  })
 }
```

**
localhost에서 실행할 때는 production 주석처리해야 돌아간다**

```
import { register } from 'register-service-worker'

/*if (process.env.NODE_ENV === 'production') { */
  register(`/service-worker.js`, {
    ready () {
      console.log(
        'App is being served from cache by a service worker.\n' +
        'For more details, visit https://goo.gl/AFskqB'
      )
    },
    registered () {
      console.log('Service worker has been registered.')
    },
    cached () {
      console.log('Content has been cached for offline use.')
    },
    updatefound () {
      console.log('New content is downloading.')
    },
    updated () {
      console.log('New content is available; please refresh.')
    },
    offline () {
      console.log('No internet connection found. App is running in offline mode.')
    },
    error (error) {
      console.error('Error during service worker registration:', error)
    }
  })
/* }*/
```

(3) main.js에서 import 해주기** (src밑에)**
```
import './registerServiceWorker';
```
해당 코드를 넣어준다. 

#### [크롬에서 Service Worker 돌아가는거 확인]
![](https://velog.velcdn.com/images/osohyun0224/post/4c5a29eb-1bdb-4d34-87c6-751c03bc8d45/image.png)

ㅠㅠㅠ 서비스 워커도 적용 성공


### [3] https 프로토콜 고찰
사실 이게 제일 하기 힘들었는데, ~~https로 할려면 많이 복잡...~~

이거에 대해서 구글링 열심히 했는데, 아래의 링크들을 참고해보면 된다. 
[nginx 무료 ssl 적용 - 티딩님](https://blog.naver.com/youngchanmm/222802167107)
[스프링부트 ssl 적용 - kirilocha님](https://velog.io/@kirilocha/Spring-boot-SSL-%EC%9D%B8%EC%A6%9D%EC%84%9C-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0)

https 프로토콜 적용해서 해당 웹사이트로 보안을 강화해야하는데, 이걸 하려면 ssl이 필요하다고 한다... 위의 두분의 글을 참고하여 구현해보자.

우선, 나는 저거 해결이 안되어서 vercel로 배포를 했는데 되긴했다!

[vercel 공식사이트](https://vercel.com/dashboard) 

내 위의 사진들을 보면 다 vercel로 배포를 하였고, 거기에서 다 잘 돌아가는 것을 확인할 수 있다.
결론은 일단 초기 단계에서는 vercel로 배포해도 가능은 하다!

![](https://velog.velcdn.com/images/osohyun0224/post/93d520e3-4fca-442b-a9f3-f22c7d758a82/image.png)

vercel로 해도 보안이 안전하게 잘 유지되고 있다.


### PWA 앱 적용 완성!

![](https://velog.velcdn.com/images/osohyun0224/post/9adc14fd-286e-48de-aa47-b1c0fc858209/image.png)

위의 과정을 잘 수행하면, 앱을 다운 받을 수 있는 아이콘이 링크 옆에 뜬다 ㅠㅠ

그리고 해당 앱을 모바일에서 확인은 안했는데 노트북에 깔리는 것을 확인할 수 있다. 

![](https://velog.velcdn.com/images/osohyun0224/post/2f208f7d-18e7-4659-ae26-4d3b8de6d6a0/image.png)

해당 앱을 실행하면 웹에서는 이렇게 뜬다

![](https://velog.velcdn.com/images/osohyun0224/post/8853744c-639b-4817-acf9-b4f11ed672b6/image.png)



이상으로 PWA를 내 프로젝트에 적용해보았다... 증말 2일 삽질했다 해당 내용을 내 깃허브 레포에도 올려두었으니 참고하면서 구현하길 바랍니다!
위의 내용은 제 벨로그에도 작성되어있습니다 (https://velog.io/@osohyun0224/Vue.js-PWA-%EC%A0%81%EC%9A%A9%ED%95%98%EB%8A%94-%EA%B3%BC%EC%A0%95%EC%9D%84-%EB%8B%B4%EC%9D%80-%EA%B8%B0%EB%A1%9D)
