---
layout: post
title: 멀티플레이어 네트워크 동기화 1
subtitle: Unity
cover-img: /assets/img/black.jpg
thumbnail-img: https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbP8p8F%2FbtrRSQycJcN%2FNn3kS6wcYsLK5kOK4xwV4k%2Fimg.png
share-img: /assets/img/black.jpg
tags: [컴공, unity, 멀티플레이어, 네트워크 동기화]
---

최근에 학과 전시회에 출품하려고 유니티로 공포게임을 만들었는데, 많은 걸.. 배워서 글을 써봅니다.
<br><br> 
저는 멀티플레이어 게임에서 플레이어나 오브젝트를 동기화하는 부분을 맡았습니다.
<br> 
각 클라이언트에서 오브젝트의 위치가 변하면 나머지 클라이언트에서도 변하는 게 보이게 구현해야 하는데요.
<br> 
동기화 같이 서버와 통신하는 부분을 처음 해봐서 많이 해맸습니다..
<br><br> 
이 글은 game object용 NETCODE를 사용하여 멀티플레이어 게임을 만들고자하는 분들께 도움이 될 것 같습니다.<br> 
저도 공유하면서 공부하려고 블로그를 써봅니다 ㅎㅎ<br> 
복습 겸 예습 겸 ^^..<br> 
<br><br> 
제가 쓰고 있는 버전은 2022.1.17입니다.<br> 
<br><br> 

# 1. 플레이어 위치 동기화(1/2)
## 필요한 패키치 설치
우선 game object용 NETCODE를 설치해줍니다.<br> 
Window -> Package Manager에서 왼쪽 상단의 + 버튼을 눌러 add package from git URL를 선택해서<br> 

`com.unity.netcode.gameobjects`<br> 
위의 걸 복사해서 설치해줍니다.

![netcode가 설치된 화면](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbP8p8F%2FbtrRSQycJcN%2FNn3kS6wcYsLK5kOK4xwV4k%2Fimg.png "netcode가 설치된 화면")


## Network Manager
하이러키 뷰에서 빈 게임 오브젝트를 추가하고 이름을 [Network Manager]로 변경합니다.<br> 
Network Manager의 인스펙터 뷰에서 Add Component를 눌러 **NetworkManager**와 **UnetTransport**를 추가해줍니다.<br> 
 
![Network Manager](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FBqP0h%2FbtrRRLRUhf5%2F6wByqEgjjPnJQmkn5QpBr0%2Fimg.png)

Select Transport를 눌러 Unet Transport를 선택해줍니다.<br> 

![Network Transport로 Unet Transport 선택](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbY3sdv%2FbtrRRCAZh4y%2F9ZBZkS5STNMx9MwEhd7Lzk%2Fimg.png)

<br>
<br> 

## Player
이제 플레이어를 만들어보겠습니다.<br> 
하이러키 뷰에서 마우스 오른쪽 버튼을 눌러 3D Object에서 Cube를 선택하고 이름을 [Player]로 바꿔줍니다.<br> 
인스펙터 뷰에서 **Network Object**와 **Client Network Transform**을 추가합니다.
<br> 
![Client Network Transform](https://blog.kakaocdn.net/dn/s9bhi/btrRTtv0kno/PllXfdENDwtEJLlxCdB2J0/img.png)

Client Network Transform를 추가하려면 먼저 Window -> Package Manager에서 git URL로 패키지를 설치해야 합니다.

```https://github.com/Unity-Technologies/com.unity.multiplayer.samples.coop.git?path=/Packages/com.unity.multiplayer.samples.coop#main```
<br><br> 

옛날 버전을 사용하시는 분은 Client Network Transform 말고 **Network Identity**와 **Network Transform**를 추가해서 구현하시면 됩니다.<br> 
제가 쓰는 버전에서는 Network Identity가 deprecated 되었다고 뜨면서 사용할 수 없어서 ... ㅠㅠ<br> 
한참을 구글링하다가 Client Network Transform를 발견했습니다.<br> 
<br> 
<br> 
NetworkTransform는 항상 서버에서 클라이언트로만 위치를 동기화하고 클라이언트의 위치 변경은 허용되지 않지만,<br> 
Client Network Transform는 클라이언트의 위치를 다른 모든 클라이언트와 동기화합니다.<br> 
<br><br> 

이제 코드를 제외하면 컴포넌트 추가는 다 했으니까..<br> 
다음 글에서는 코드 추가하고 플레이어 동기화 마무리할게요!<br> 

 