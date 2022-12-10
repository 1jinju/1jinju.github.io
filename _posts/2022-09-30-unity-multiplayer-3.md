---
layout: post
title: 멀티플레이어 네트워크 동기화 3
subtitle: Unity
cover-img: /assets/img/black.jpg
thumbnail-img: https://blog.kakaocdn.net/dn/cYCW9l/btrR5xNeSAL/OSx5KSI1O92hJf8QKEO470/img.png
share-img: /assets/img/black.jpg
tags: [컴공, unity, 멀티플레이어, 네트워크 동기화]
---


이제 문 상태 동기화를 구현해보겠습니다.<br>
앞의 내용과 비슷하긴 한데, 버전 문제때문에 많은 우여곡절을 겪었습니다 ㅠㅠ<br>
차근차근 해결과정을 적어볼게요!<br>
<br>

# 2. 문 상태 동기화(1/2)
## Door
문을 만들겠습니다.<br>
하이러키 뷰에서 마우스 왼쪽 버튼을 눌러 3D Object에서 Cube를 선택하고 이름을 [Door]로 바꿔줍니다.<br>
큐브가 문처럼 보여야 하니까 Transform 컴포넌트를 변경해주었습니다.<br>

|Position|0	|4 |8  |
|Rotation|0	|0 |0  |
|Scale	 |4	|8 |0.3|

문을 갈색으로 만들어주겠습니다.<br>
프로젝트 뷰에서  마우스 오른쪽 버튼을 눌러 Create -> Material를 추가하고 이름을 DoorMat으로 바꿔줍니다.<br>

![DoorMat](https://blog.kakaocdn.net/dn/cYCW9l/btrR5xNeSAL/OSx5KSI1O92hJf8QKEO470/img.png)


Albedo, Metallic과 Smoothness를 조정하여 마음에 드는 색으로 바꿔주었습니다.<br>
이 DoorMat을 Door 오브젝트에 드래그하면 문의 색이 바뀝니다.<br>
<br>
 
플레이어와 마찬가지로 Door 오브젝트에 **NetworkObject**와 **ClientNetworkTransform**을 추가합니다.<br>

![컴포넌트 추가](https://blog.kakaocdn.net/dn/bFFClr/btrR5yL4QTP/DTQs0FzKGiC5LgwnWjd1N1/img.png)
 

문도 프리팹으로 만들어 NetworkManager에 네트워크 프리팹으로 추가해줘야 합니다.<br>
하이러키 뷰의 Door를 프로젝트 뷰로 드래그하여 프리팹으로 만들어줍니다.<br>

![Door 프리팹](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcHoiyY%2FbtrR71mzZ5o%2F50XkWoDxHzP772gkJwwaB0%2Fimg.png)
 
## Terrain
문과 플레이어의 충돌 검사를 위해 플레이어에 Rigidbody 컴포넌트를 추가할 예정인데,<br>
지형이 없다면 중력에 의해 플레이어가 아래로 떨어지게 됩니다.<br>
<br>
 

플레이어가 돌아다닐 수 있도록 지형을 만들어주겠습니다.<br>
하이러키 뷰에서 마우스 오른쪽 버튼을 눌러 3D Object -> Terrain를 선택합니다.<br>
문이 Terrain의 가운데에 오도록 Terrain의 위치만 바꿔주었습니다.<br>

|Position|-100|0 |-100|
|Rotation|0   |0 |0   |
|Scale	 |1	  |1 |1   |
 
![Terrain](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJSShm%2FbtrR8s4YK02%2FKw3pj3L68hpaHJqq0ijOl0%2Fimg.png)

## Player
아까 말했던 대로 Player 프리팹에 **Rigidbody**를 추가합니다.<br>
프로젝트 뷰의 Player를 두 번 클릭하면 프리팹에 컴포넌트를 추가할 수 있습니다.<br>

![리지드바디 추가](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbahVvQ%2FbtrR9c1qOpB%2Fw9LutbVhxFJDJK0SkdxJGk%2Fimg.png)



## NetworkManager
![Door 프리팹 추가](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fr8Lud%2FbtrSaq6K4Kh%2FkbdJcjxkDr4565btTOLqJ0%2Fimg.png()

인스펙터 뷰에서 NetworkManager 안에 있는 NetworkPrefabs에 +버튼을 눌러 Door 프리팹을 추가합니다.<br>

![실행 화면](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcCNPDY%2FbtrR8awMfcd%2FTNUwI3Axh86A73IGQctQo1%2Fimg.png)

 

스크립트가 없으니까 역시 쉬운 것 같아요 ㅎㅎ<br>
다음 글에서는 스크립트를 추가해서 문 상태 동기화를 마쳐보겠습니다.<br>
<br>
