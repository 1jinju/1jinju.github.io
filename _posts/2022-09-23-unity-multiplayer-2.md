---
layout: post
title: 멀티플레이어 네트워크 동기화 2
subtitle: Unity
cover-img: /assets/img/black.jpg
thumbnail-img: https://blog.kakaocdn.net/dn/bpiLw9/btrRY1FBJvJ/Asm6fJlnroU68LSM1cydO1/img.png
share-img: /assets/img/black.jpg
tags: [Unity]
---

지난 글에서 패키지를 설치하고 필요한 오브젝트와 컴포넌트를 추가했는데요.<br>
이제 알맞은 코드를 넣어보겠습니다!<br>
<br>

# 1. 플레이어 위치 동기화(2/2)

## Network Manager
프로젝트 뷰에서 C# Script를 새로 만든 후 이름을 HelloWorldManager로 바꿔줍니다.<br>
이 스크립트를 Network Manager 오브젝트에 Add Component로 추가해줍니다.<br>

```cs
// HelloWorldManager.cs

using UnityEngine;
using Unity.Netcode;
using Unity.Netcode.Transports.UNET;

public class HelloWorldManager : MonoBehaviour
{
    private static string ip = "127.0.0.1";

    void Start()
    {
        Application.targetFrameRate = 30;
    }

    void OnGUI()
    {
        GUILayout.BeginArea(new Rect(10, 10, 300, 300));
        if (!NetworkManager.Singleton.IsClient && !NetworkManager.Singleton.IsServer)
        {
            StartButtons();
        }
        else
        {
            StatusLabels();
        }

        GUILayout.EndArea();
    }

    static void StartButtons()
    {
        ip = GUILayout.TextField(ip, 20);
        NetworkManager.Singleton.GetComponent<UNetTransport>().ConnectAddress = ip;
        if (GUILayout.Button("Host"))
        {
            NetworkManager.Singleton.StartHost();
        }
        if (GUILayout.Button("Client"))
        {
            NetworkManager.Singleton.StartClient();
        }
        if (GUILayout.Button("Server"))
        {
            NetworkManager.Singleton.StartServer();
        }

    }

    static void StatusLabels()
    {
        var mode = NetworkManager.Singleton.IsHost ?
            "Host" : NetworkManager.Singleton.IsServer ? "Server" : "Client";

        GUILayout.Label("Transport: " +
            NetworkManager.Singleton.NetworkConfig.NetworkTransport.GetType().Name);
        GUILayout.Label("Mode: " + mode);
    }
}
``` 

**컴파일할 때 에러가 뜨는 경우**

![error 메시지](https://blog.kakaocdn.net/dn/bpiLw9/btrRY1FBJvJ/Asm6fJlnroU68LSM1cydO1/img.png)

ProjectSettings -> Player -> OtherSettings -> Configuration에서 Assembly Version Validation을 비활성화합니다.<br>

참고: [참조에 '유니티 플라스틱'오류가 있습니다. 문제 #113 · gkngkc/UnityStandaloneFileBrowser (github.com)]

[참조에 '유니티 플라스틱'오류가 있습니다. 문제 #113 · gkngkc/UnityStandaloneFileBrowser (github.com)]: https://github.com/gkngkc/UnityStandaloneFileBrowser/issues/113

옛날 버전에서는 NetworkManager와 NetworkManagerHUD를 컴포넌트로 추가하면 자동으로 아래와 같은 GUI가 만들어져 편리했었습니다.<br>

![NetworkManagerHUD](https://blog.kakaocdn.net/dn/bUbi3Q/btrRXbJsBBM/bW1VMZIN46qoojGhDTypT0/img.png)


그러나 제 버전에서는.. mlapi가 잘 작동하지 않는 관계로..<br>
HelloWorldManager.cs를 추가하여 아래와 같이 호스트, 클라이언트 또는 서버로 시작하기 위한 GUI를 만들어주었습니다.<br>
![HelloWorldManager.cs](https://blog.kakaocdn.net/dn/cqLJsP/btrRXC0RGy3/c1PIBt7jfQ3hVqz5lRhOJ1/img.png)

<br>

## Player
플레이어 위치를 동기화해보겠습니다.<br>
PlayerCtrl.cs를 새로 만들고 Player 오브젝트에 추가해줍니다.<br>
 
```cs
using UnityEngine;
using Unity.Netcode;

public class PlayerCtrl : NetworkBehaviour
{
    void Update() { 
        // 로컬 플레이어가 아니면 return되어 if 문 아래 코드가 동작하지 않음
        if (!IsLocalPlayer)
        {
            return;
        }

        var x = Input.GetAxis("Horizontal") * Time.deltaTime * 150.0f;
        var z = Input.GetAxis("Vertical") * Time.deltaTime * 3.0f;

        transform.Rotate(0, x, 0);
        transform.Translate(0, 0, z);
    }
    
}
```
**주의**
1. PlayerCtrl 클래스는 MonoBehaviour가 아닌 NetworkBehaviour를 상속해야 합니다.
2. isLocalPlayer가 아니라 IsLocalPlayer입니다.
    - 제가 isLocalPlayer로 써서 한참을 해맸습니다..


이제 Player 오브젝트를 프로젝트 뷰로 드래그하여 프리팹으로 만들고 하이러키 뷰에서 삭제합니다.<br>

![Project 뷰](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbW3JAZ%2FbtrRY3cnXDD%2FPG5aDPRclV2ynqhfvpka81%2Fimg.png)

 

플레이어는 시작 씬에서 호스트나 클라이언트 버튼을 눌렀을 때 스폰되어야 합니다.<br>
따라서, 플레이어 프리팹을 네트워크 프리팹으로 설정해주겠습니다.<br>
<br> 

NetworkManager 오브젝트로 가서 Player Prefab에 방금 만든 Player 프리팹을 넣어줍니다.<br>

![NetworkManager에 프리팹 추가](https://blog.kakaocdn.net/dn/JsCX9/btrRY3Dr4Tx/hZocbTeJQcCFz1uk04yBYK/img.png)


## 실행
이제 플레이어 위치 동기화가 잘 수행되고 있는지 확인해보겠습니다.<br>
테스트하기 위해 빌드가 필요한데요.<br>
<br>
 

1. File -> Bulid And Run을 누르면 아래와 같이 빌드한 파일을 넣을 폴더를 선택하는 창이 뜹니다.
![파일탐색기](https://blog.kakaocdn.net/dn/6wxo1/btrRWLxx4Y3/PdoQ0EbLHvW9zUk4cRF6v0/img.png)

저는 이 프로젝트 바깥에 새 폴더를 만들어서 exe 파일을 넣었습니다.<br>
<br>

2. 빌드가 완료되면 유니티 프로젝트에서는 Host로 실행하고, exe 파일은 Client로 실행합니다.<br>
![Run](https://blog.kakaocdn.net/dn/djw5d4/btrRY2xOMcA/UYqXdK5k58nbUDQGoK0141/img.png)
 


3. 방향키로 플레이어를 움직여보면 각 창에서 위치가 서로 동기화되는 것이 보입니다.<br>
하이러키 뷰에 Player(clone)이 2개 생성되어 있는 것을 통해 이를 확인할 수 있습니다.<br>

![플레이어 동기화](https://blog.kakaocdn.net/dn/voG22/btrRYuOSmNz/d1UQ2WkJm991PijBGw5vg1/img.png)
<br>


이로써 플레이어 위치 동기화를 마쳤습니다.<br>
다음 글에서는 문 상태 동기화를 구현해보겠습니다 ~.~<br>