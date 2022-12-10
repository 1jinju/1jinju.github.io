---
layout: post
title: 멀티플레이어 네트워크 동기화 4
subtitle: Unity
cover-img: /assets/img/black.jpg
thumbnail-img: https://blog.kakaocdn.net/dn/XtmvO/btrR9G3mUEt/UNHBOKks0dcPF87jpBqeDk/img.png
share-img: /assets/img/black.jpg
tags: [컴공, unity, 멀티플레이어, 네트워크 동기화]
---

저번에 하던 문 상태 동기화를 마무리해보겠습니다.<br>
이 시리즈의 마지막 글입니다 ㅎㅎ<br>
<br>

# 2. 문 상태 동기화(2/2)

## Player
프로젝트 뷰에서 마우스 오른쪽 버튼을 눌러 InteractScript.cs를 만듭니다.<br>
```cs
// InteractScript.cs

using UnityEngine;
using Unity.Netcode;

public class InteractScript : NetworkBehaviour
{
    public float interactDiastance = 5f;
    public GameObject Door;
    void Start()
    {
    }

    void Update()
    {
    	// 로컬 플레이어가 아니면 return되어 if 문 아래 코드가 동작하지 않음
        if (!IsLocalPlayer)
        {
            return;
        }

        if (Input.GetKeyDown(KeyCode.F))
        {
            Ray ray = new Ray(transform.position, transform.forward);
            RaycastHit hit;
            if (Physics.Raycast(ray, out hit, interactDiastance))
            {
                Debug.Log(hit.collider);
                if (hit.collider.CompareTag("Door"))
                {
                    hit.collider.transform.GetComponent<DoorCtrl>().ToggleServerRpc();
                }
            }
        }
    }
}
```
Raycast는 어떤 위치에서 광선을 발사하여 그 광선에 닿는 물체가 있는지 검사하는 방식입니다.<br>
InteractScript에 연결된 물체(Player)에서 forward 방향, 즉 (0, 0, 1)로 광선을 발사하여 충돌을 검사하고 있습니다.<br>
<br>

광선을 발사한 위치와 광선에 닿은 물체 사이 거리가 InteractDistance보다 작고 광선에 닿는 물체의 태그가 Door이면,<br>
그 물체의 컴포넌트에서 DoorCtrl를 찾아 그 안에 있는 ToggleServerRpc 함수를 실행합니다.<br>
뒤에 나오겠지만 ToggleServerRpc 함수는 문의 상태를 바꿔주는 함수입니다.<br>
<br>
 

따라서, 전체적으로 동작하는 방식은 다음과 같습니다.<br>
플레이어가 F키를 눌렀을 때 문과 플레이어가 일정 거리 안에 있으면 문이 열립니다.<br>
<br>

프로젝트 뷰의 Player 프리팹을 더블 클릭하여 Player 프리팹에 **InteractScript** 컴포넌트를 추가합니다.<br>
<br>

![Door 프리팹](https://blog.kakaocdn.net/dn/XtmvO/btrR9G3mUEt/UNHBOKks0dcPF87jpBqeDk/img.png)
<br>

## Door
DoorCtrl.cs을 만들어서 Door 프리팹에 컴포넌트로 추가합니다.<br>
![DoorCtrl.cs](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc3iNnA%2FbtrR8JzK3Zf%2F40GH7FUmcKIiG0PcVhGfD1%2Fimg.png)
 
```cs
// DoorCtrl.cs

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Unity.Netcode;

public class DoorCtrl : NetworkBehaviour
{
    public float doorOpenAngle = -90f;
    public float doorCloseAngle = 0f;
    public float smoot = 2f;

    public NetworkVariable<bool> open = new NetworkVariable<bool>();

    void Start()
    {
        open.Value = false;
    }

    void Update()
    {
        if (IsClient && IsOwner)
        {
            Act();
        }
    }

    [ServerRpc(RequireOwnership = false)]
    public void ToggleServerRpc()
    {
        open.Value = !open.Value;
    }

    public void Act()
    {
        if (open.Value) // 문 열기
        {
            Quaternion targetRotation = Quaternion.Euler(0, doorOpenAngle, 0);
            this.transform.localRotation = Quaternion.Slerp(transform.localRotation, targetRotation, smoot * Time.deltaTime);
        }
        else
        {
            Quaternion targetRotation2 = Quaternion.Euler(0, doorCloseAngle, 0);
            this.transform.localRotation = Quaternion.Slerp(transform.localRotation, targetRotation2, smoot * Time.deltaTime);
        }
    }
}
```
참고: [NetworkVariable | Unity Multiplayer Networking (unity3d.com)]

[NetworkVariable | Unity Multiplayer Networking (unity3d.com)]: https://docs-multiplayer.unity3d.com/netcode/current/basics/networkvariable/index.html


이 DoorCtrl.cs은 ToggleServerRpc()가 실행될 때마다 서버에서 현재 open.Value의 값을 받아 반대로 바꿔줍니다.<br>
문이 열려 있다면 닫힌 상태로 만들어주고, 닫혀 있다면 열린 상태로 만들어주는 것입니다.<br>
<br>
 

Act()는 사원수(Quaternion)을 써서 문을 회전시키는 역할을 합니다.<br>
Update()에서는 프레임마다 계속 Act()를 호출하여, 문이 닫히거나 열리는 게 플레이어 눈에 보이게 됩니다.<br>
사원수 개념은 나중에 정리해서 올려보겠습니다!<br>
<br>

이 스크립트를 작성하는 부분이 가장 어려웠습니다 .. <br>
호스트에서 문을 열면 클라이언트에서도 같이 문이 열리는데, 클라이언트에서는 문이 아예 안 열리거나 열리더라도 호스트 쪽에서는 문이 열리는 게 안 보여서 ..<br>
SyncVar를 사용하려고 했었는데 잘 안 되더라구요 ㅠㅠ<br>
NetworkVariable을 사용하면 매우 잘 동작합니다 ^^<br>
<br>
 

이제 Door 프리팹에서 Tag를 Untagged에서 Door로 바꿔줍니다.<br>

![Tag 추가](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FL4kNd%2FbtrR9dG9ft5%2FwRhTEsNKmD5Q4nMyQYdR11%2Fimg.png)


 
마지막으로, Door 프리팹에 **Box Collider**를 추가합니다.<br>
둘 중 하나의 Box Collider에만 isTrigger에 체크를 해줍니다.<br><br>

![Box Collider 추가](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnGO5e%2FbtrSahow5x6%2FOeou0uigbjfd0pltMgNwt1%2Fimg.png)
 


## 실행
빌드를 하고 각 클라이언트에서 문 동기화가 되는지 확인해보겠습니다.<br>

![실행 화면](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fye4cm%2FbtrR8s6a1dv%2FcjQkx5jNYQ1Xqug19K0tR0%2Fimg.png)

동기화가 잘 되고 있는 것을 확인할 수 있습니다.<br>
근데 문 열리는 모양새가 좀 이상한데 이건 문 열리는 중심축을 바꿔주면 될 것 같습니다 ㅎㅎ<br>
<br>
 

hlapi가 사라지면서 안 되던 부분들을 netcode를 사용해서 해결해보았습니다.<br>
저는 거의 한 달 넘게 헤맸는데 이 글을 보시는 분들은 후다닥 해결하고 재밌는 게임 만드셨으면 좋겠습니다!<br>