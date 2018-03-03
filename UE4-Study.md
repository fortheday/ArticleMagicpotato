# Unreal Engine 4 Study note
* 2018-01-29. magicpotato.

# 공부방법
> 언리얼 엔진을 공부하는 방법에 대한 가이드라인

1. ~완전히 새로 배운다고 생각해야 한다. 용어도 의심없이 받아들여야 한다.~
   언리얼이 처음인 경우 다양한 형태의 강좌를 여러개 볼 수 밖에 없다. 공홈 문서만 보라는 사람들은 언리얼3 이전부터 엔진을 써 본 사람이 많은 것 같다. 1달가량 언리얼을 공부하는 도중 느낀 점은 언리얼 엔진은 존카막같은 테크니컬 엔지니어가 만든 레거시를 끌고 가는 느낌이 강하다. (앤더슨 헤일스버그같은 사람이 .NET, C#을 설계한 것과는 반대편에 있는 느낌) 기술, 성능 같은것은 훌륭하겠지만, 소프트웨어 구조나 모듈 레벨에서 볼 때 정돈된 엔진이 아니다. 좋은 예시로 TMap.FindRef()함수가 적절한데, 이 것은 GetValueByKey()같은 이름을 가져야 한다.

1. 문서가 이해되지 않으면 문서가 불친절하게 작성되었을 가능성이 높다. 반드시 직접 테스트하거나 코딩해 봐야 한다.

1. 훑어보고 → 해보고(까먹고) → 한번 더 보는 정도로 학습하는게 효율적이다.
   > 양이 많고, 생소한 용어나 개념이 많다.
   > 분량이 많으므로 조급해 하지 말고, 꼭꼭 씹어먹으며 소화하자. 익히고 써보고를 반복.
1. 학습중인 강의 주제에만 집중한다.
   > 궁금한 것들이 처음에는 어차피 빠르고 쉽게 파악되지 않기 때문이다.

1. 프로그래머는 다음 순서대로 익힌다.
   1. 아티스트로서 언리얼 에디터를 다루는 법 (No코딩)
   2. 스크립터로서 언리얼 에디터를 다루는 법 (블루프린트)
   3. 언리얼 에디터상에서 만들 수 있는 C++ 클래스등의 코딩 방법
   4. 위 단계 학습중에 **프로그램적 구조**에 대한 의문은 미뤄두자. (비효율적이다)
   5. 언리얼 에디터의 소스를 클론받아 빌드하고 개선하는 법 <가능한 늦게>

1. 학습분야
   1. 메인창내의 모든 탭의 목록과 용도
   2. 모든 리소스 타입의 목록과 용도 + 연관 서브에디터들 (메쉬창, 매터리얼창, 블루프린트창 등등)
     1. 모든 에셋 타입 이해
        1. 에셋별 프로퍼티 값 이해 (한 에셋별로 완전격파는 어렵다. 점진적으로 공부하자)
   3. 게임모드, 프로젝트 환경설정 이해
   4. 프로젝트 폴더 구성 이해 → 쿠킹 폴더 구성 이해 → 엔진 폴더 구성 이해
..... **TODO**

1. 학습자료
   1. 언리얼 에디터의 전반적 기능을 다루는 가장 **얇은** 책 한권을 '지도'로 삼는다.
      > 추천하는 책을 봤는데도 설명이 난해하다. 단지 '목차'용도로만 쓰고 아래 자료로 공부.
   2. [네이버카페-입문강의](http://cafe.naver.com/unrealenginekr/735)
      > UMG강의는 흐름이 복잡한편. 그때그때 따라하든가, 연관관계를 그리면서 공부하길 권장. 조급하다고 배속을 올리면 자막만 보느라 화면내용을 놓칠 수 있다. 마우스커서와 맥락을 집중하면서 볼 것. 모든 영상을 볼 필요는 없다. 어떠 강의는 논점이 흐트러지면서 중구난방으로 설명해서 따라가기 어렵다.
   3. [언리얼서밋-중급강의](http://replay.unrealsummit.co.kr/)
      1. [엔진 개념 등](http://replay.unrealsummit.co.kr/data/summit2017/unrealsummit018.pdf)
      1. [언리얼엔진4 시작하기](http://replay.unrealsummit.co.kr/data/ue_start.pdf)
      1. 레퍼런스만 알면 언리얼 엔진이 제대로 보인다
         [영상](http://replay.unrealsummit.co.kr/v1.html) 
         [PDF](http://replay.unrealsummit.co.kr/data2017/session01.pdf)
      1. [언리얼이 쉬워지는 6가지 핵심 개념](http://replay.unrealsummit.co.kr/data/summit2016/2016_02.pdf)
      1. [언리얼 튜토리얼만 쌓여가는 유니티 개발자를 위한 조언](http://replay.unrealsummit.co.kr/data/summit2017/unrealsummit018.pdf)
      1. [모바일 개발 설정과 패키징](http://replay.unrealsummit.co.kr/data/summit2015/2015_02.pdf)
      1. [UMG 사용가이드](http://replay.unrealsummit.co.kr/data/summit2015/2015_10.pdf)
   4. [언리얼공식 문서](https://docs.unrealengine.com/latest/KOR/)
      1. 공홈에 필요한 내용은 다 있지만, 문서가 정돈되어 있지 않고 원작자가 원작자를 위한 문서화를 한 것 같은 정도의 수준이다. 이해가 안 될 경우 독자의 잘못이 아닐 가능성이 높다. 코딩을 직접 해보고 시간이 좀 흘러야 "아 이게 이걸 말하는 거였구나" 같은 수준의 문서들이 있다는 것을 알고 봐야한다.


# 최소 용어

1. 에셋: Content Browser에 등록된 것들 (배치안됨)
2. 액터: Map에 배치된 것들
3. PBR: 표면을 물리적으로 정의한 체계로 매터리얼을 구성하는 것
4. SubUV: 고전 스프라이트 텍스쳐 (NxN으로 잘라서 사용하는 용도 - 2D, 이펙트)
5. 라이트매스: 정적 라이팅 시스템 (라이트맵 빌더?)

# Editor 구성
1. Viewport: 씬 에디터
2. World Outliner: 맵에 배치된 모든 액터 목록
3. Details: 선택된 액터
4. Content Browser: 개발자 에셋
5. Modes: 엔진 에셋 등 **todo: Mode라는 용어를 쓴 이유를 알아야 한다**
6. Layers: 액터 레이어 관리


# Unreal4 Folder Structure

1. No StarterPackage, Blank Project 생성
2. ContentsBrowser에서 Show in Explorer 클릭
3. 폴더 내용 확인

| Folder       | Desc | SVN |
| ---          | --- | --- | 
| Config       | ini파일들, 내 게임/에디터 기능의 세팅값들 | 버전관리 |
| Content      | uasset, umap 등 게임 에셋들) | 버전관리 |
| Intermediate | 빌드 | 삭제 |
| Saved        | 자동저장 | 삭제 |


# Gameplay Framework 개요 (GameMode) [UE Link](https://docs.unrealengine.com/latest/INT/Gameplay/Framework/index.html)

> 유니티를 쓸 때 매니저급 싱글톤들을 만들어야 한다. Hierarchy에 싱글톤을 배치하지 않아도 Play를 누르면 편의상 자동 생성하는 것 처럼 언리얼에는 이런것들이 XXXBase의 이름으로 이미 존재한다. 유니티에서 직접 만들어야 하는것을 언리얼에서는 **분석**하고 상속받아서 쓰는 것 같다.

1. No StarterPackage, Blank Project 생성
2. World Outliner의 모든 액터 삭제
3. Play
4. World Outliner에 자동추가된 런타임 객체들 확인
   * 이것들은 GameMode에 따라 달라진다.
     * Project Settings - Maps&Modes
     * World Settings - GameMode Override


## Framework Class Relationships
![Framework Class Relationships](https://docs.unrealengine.com/latest/images/Gameplay/Framework/QuickReference/GameFramework.jpg)


# 좌표계: 왼손
![CoordSystem](http://usarsim.sourceforge.net/wiki/images/2/24/Figure24.jpg)
1. Forward = X
2. RIght = Y
3. Up = Z


# 단위
1. 1 UnrealUnit => 1cm
2. 중력가속도 0.98 => 980


# World Outliner 주요개념
1. Folder: 단순 정리용
2. Group: 일괄 TRS 에디트용
3. Layer: ~~카메라 필터링등에 이용~~ (TODO: 좀 더 확인)
4. Attach: 계층구조 구성
* 오브젝트 배치는 Modes패널이 Place(Shift+1) 상태여야 한다. (폴리지 상태로 불가능)


# 조명 세팅
1. Sky Sphere / Sky light(Ambient light) / Atmospheric fog
   1. Sky Sphere.Directional light Actor에 Directional Light 설정가능
2. 라이트 종류
   1. Static: 라이트맵으로 이용
   2. Stationary: 이동불가, 밝기/색/OnOff 제어가능
   3. Movable: 동적 라이트, 간접광 불가
3. Swarm Agent: 라이트 빌더
4. Lightmass Importance Volume
   1. 반사광 처리를 고려할 영역을 지정할 때 사용 (라이트 빌드 시간 최적화)


# Material / Editor
1. 언리얼은 매터리얼 단위를 기본으로 사용 (텍스쳐는 기본단위 아님)
2. Material을 상속받아 Material Instance를 사용할 수 있다.
3. Material
   1. 매터리얼에서 TextureSample(T)를 BaseColor로 끌어다 쓰는 방식
   2. 에디터에서 특정 노드 우클릭 후 **Convert to Parameter**로 속성 노출
   3. Parameter는 Material Instance 더블 클릭 후 에디터에서 수정
   4. MeshActor에 지정된 Material의 Parameter는 Details창에 노출되지 않는다.
   5. 즉, 베리에이션 수 만큼의 Material Instance를 만들어야 한다.


# Static Mesh Asset / Editor
1. FBX, OBJ 드래그&드랍 또는 우클릭 Import To로 해당 에셋 추가
2. 더블클릭으로 Static Mesh Editor 열기
3. Static Mesh Editor
   * 매터리얼, LOD, 콜리전 헐/충돌방식, 소켓 등 설정


# Audio Asset
1. 사운드 파일 드래그&드랍 또는 우클릭 Import To로 해당 에셋 추가
2. (씬에 배치된)Ambient Sound Actor에 Sound Wave Asset을 지정해서 사용하는 방식


# Landscape & Foliage
1. Landscape: 심시티 지형 편집기 개념 (Shift+3)
   1. 사용시 Landscape, LandscapeGizmoActiveActor가 하나씩 배치된다.
   2. 전용 매터리얼을 만들면 Landscape.Paint.TargetLayers에서 사용가능
      1. Landscape Layer Blend 노드를 갖는 매터리얼을 생성
         1. Layers를 구성하고 노드를 입력한다.
         2. 레이어 핵심파라미터: Layer Name, BlentType
2. Foliage: Static Mesh Asset 분무기 개념 (풀심기 툴) (Shift+4)
   1. Foliage 팔레트에 StaticMesh들을 등록한 다음 지형 위에 흩뿌린다.


# [Cinematics with Sequencer](https://www.youtube.com/watch?v=uEnfMV-4afA&index=1&list=PLZlv_N0_O1gaiA_sfpjATUprVW7B9FcK1)
> 시네마틱 도중에 블루프린트로 제어하는 등의 내용은 없다.


# Blueprint Class (따라해보기)
1. 레벨에 StaticMesh, PointLight, SoundCue 를 하나씩 배치한다.
2. 모두 선택 후 메인 툴바에서 Blueprint → **Convert selected Components to Blueprint Class** 선택
3. BP 에디터에서 각 컴포넌트의 기본값을 세팅한다.
4. 메인 에디터 File → Save All
5. BPC 여러개 배치
   1. 배치된 BPC Instance의 Details를 확인
   2. Root, Component 개념 확인


# 캐릭터/애니메이션 (1)
> UE4에서 기본 제공하는 Owen 캐릭터를 Reference Viewer로 확인해 보자.
1. 필수 구성요소
   1. Skeletal Mesh: 본, 메시, 가중치등을 가짐. Skeleton에 의해 제어됨 (fbx)
   2. Skeleton: Skeletal Mesh에 적용되는 뼈대. Animation Sequence에 의해 제어됨 (fbx)
   3. Animation Sequence: Skeleton에 대한 애니메이션 정보 (키 프레임 위치, 회전, 스케일) (fbx)
2. 추가 구성요소
   1. Physics asset: Skeleton과 연동, Ragdoll로 작동하게 하거나 ray처리 가능(?)
   2. Animation Blueprint
3. 페르소나 에디터
   > 연관에셋 중 아무거나 더블클릭 해서 열고 전환 가능.
   1. 스켈레톤: 스켈레톤 계층 구조를 확인, 관절 테스트, 소켓 추가 등
      1. [스켈레톤 에셋 강좌](https://www.youtube.com/watch?v=FDbpHamn2eY&list=PLZlv_N0_O1gbwdyIm78w42fZ1t8dDClsI&index=1)
         1. 임포트, 에셋 설명, 리타게팅, 소켓(무기슬롯), 애니노티(이벤트→블루프린트), 애니커브(AniState에서 커브값 받아서 블루프린트 사용)
   2. 메시: LOD 설정, 물리/천 설정, 매터리얼 설정 등
   3. 애니메이션: 애니메이션 설정, 소켓/노티파이 설정, 각 시퀀스 편집 등
      1. 그래프편집: 애니메이션 블루프린트 편집 (애니메이션간 블렌드, 이벤트 등 제어)
   4. 물리: 물리 설정


# 애니메이션 창 (2)
1. 편집 뷰
   1. Notifies: [노티파이](https://www.youtube.com/watch?v=per6KmuvRlQ&index=5&list=PLZlv_N0_O1gbwdyIm78w42fZ1t8dDClsI)
                [다른거](https://www.unrealengine.com/ko/blog/crash-course-in-animation-notifies)
   2. Curves:
   3. Tracks: 하나의 본마다 TRS를 갖는다. (Transform,Rotate,Scale)
   4. Timeline: 화면 맨 아래 좁은 영역이 타임라인이다. 우클릭 메뉴 가능.
2. 키 추가 방법
   > 키 추가 팁: 0프레임, 마지막 프레임에서 +Key 버튼을 2번씩 누르면 초기값 키가 생성된다.
   1. Timeline에서 프레임을 선택
   2. Skeleton Tree에서 건드릴 본을 선택
   3. 툴바의 +Key 버튼 (단축키 s)
   4. 뷰포트에서 수정
   5. 툴바 Apply 버튼


# [파티클](https://www.youtube.com/watch?v=OXK2Xbd7D9w&index=1&list=PLZlv_N0_O1gYDLyB3LVfjYIcbBe8NqR8t)
1. 메인용어
   1. 파티클시스템: 이미터의 집합. 파티클을 표현
   2. 이미터: 모듈의 집합. 입자타입별 생성-처리-소멸을 관장 / 왼쪽에서 오른쪽으로 실행
   3. 모듈: 입자 타입의 각 처리단계를 관장 (생성, 색상변화, 크기변화 등). Required/Spawn은 필수모듈 / 위에서 아래로 실행
      1. 타입데이터모듈: 이미터당 1개만(검은바에 위치) 가능. 어느 종류의 파티클을 만들지 통제.
      2. Distribution: 분포. 추상적 의미로 사용되었으므로 '모듈기능 처리시, 시간에 따른 (용도별)값' 세팅으로 보자.
2. 서브용어
   1. Cascade: 파티클 시스템 에디터
   2. 이미터 액터: 파티클시스템을 갖는 액터
   3. 파티클시스템 컴포넌트: 블루프린트(클래스?)의 구성요소로 사용하는 파티클시스템(의 랩퍼?)


# 네트워크
1. 용어
   1. 리플리케이션: 액터 동기화, 변수 동기화, RPC호출등을 뜻함
   2. Authority: 수정권한 같은 개념. 내 캐릭터의 변수 수정권한은 서버가 갖는다. HUD/UI 수정 권한은 내가 갖는다.
2. 참고
   > 대충 훑어보면 MMO를 만들 때 언리얼 서버를 쓰지는 않는 것 같다. '룸'당 하나의 서버가 떠야 하는 개념. '연관성'이라는 개념이 있는데 MMO에서 사용 가능한 수준인지 살펴보자.
   1. [mmo capabilities of UE4?](https://forums.unrealengine.com/community/general-discussion/41479-mmo-capabilities-of-ue4)
   2. [데디케이트 서버 관련 이야기1](http://lab.gamecodi.com/board/zboard.php?id=GAMECODILAB_QnA_etc&no=5084)
   3. [데이케이트 서버 관련 이야기2](http://www.gamecodi.com/board/zboard.php?id=GAMECODI_Talkdev&no=3135)
3. 주의사항
   1. 블루프린트에서 노드아이콘을 염두해야 한다. (서버모양은 서버에서만 실행, 모니터+번개는 서버에서 실행 아예 안함)
   2. ReplicationNotify는 블루프린트에서만 작동한다. C++코딩시 직접 노티를 날려줘야 함.



# 블루프린트 Hello World
1. 메인툴바 → Blueprints → Open Level Blueprint
2. `Event Tick` 노드의 exec ▷를 드래그, 빈 공간에 드랍
3. `Print String`을 찾아서 선택 (Search창에 `print string` 입력)
4. `Print String`의 `In String`값을 `Hello world` 로 변경
5. `Play` 클릭 후 뷰포트 확인


# 블루프린트 편집
1. Alt-클릭: 와이어 삭제


# 블루프린트 추가공부 (미완성)
1. 블루프린트 작성시 사용가능한 액터/클래스들의 목록 (PlayerController 등)
2. 기본 컴포넌트/자료형 목록 (Transform 등)


# 코드 실행순서
1. 클래스 생성자
2. 에디터 설정값 세팅
3. 클래스 BeginPlay()


# C++ 코딩(컨텐츠레벨) 팁
1. UFUNCTION() 이용시 [FunctionName]_Implementation 에 구현해야 한다.
2. 


# 컴포넌트 개념 (미완성)
```
Modes.Place-Basic.EmptyActor를 하나 배치한 뒤, Details창을 2개로 연다.
Details의 구성목록 중 Actor(Instance)와 DefaultSceneRoot를 열어놓고 비교해 본다.
만들어진 Actor의 Details에서 Add Component를 누르고 Audio를 추가하자.
Details의 구성목록 중 Audio를 DefaultSceneRoot로 드래그 드랍해서 Root를 교체해보자.
여전히 Actor(Instanc)의 Details 표시항목은 똑같다.
* Actor의 Details 표시항목은 Inherited컴포넌트의 것을 가져온다.
* Actor는 Rendering, Actor, HLOD 프로퍼티 카테고리를 추가로 갖는다.

Fog처럼 씬글로벌 개념인 애들은 컴포넌트 추가가 아예 안된다. Geomerty도 안된다.
나머지 대분은 컴포넌트 추가가 된다.

네이티브 컴포넌트(C++에서만?)라는 개념이 있다.
```


# 개인메모
  1. 한번 더 깊게 공부: 파티클, 액터애니메이션, 시네마틱, 사운드에셋구조, UMG편집 별도공부
                        BehaviourTree, StreamingMap/서브레벨, 빌드자동화
  2. 물리용어
     - damping 감쇠(회복력)
     - friction 마찰력
     - restitution 탄성(회복력)
     - impulse 충격량

  3. 코딩할 때 인텔리센스, 파라미터 리스트를 끄고 학습(산만해지고, 헤더를 안 찾아보게 된다)


# 개인메모2 (횡스크롤 액션 하려다 만 것 기록)
```
1. 3인칭 프로젝트의 마네킹을 가져옴.
2. 마네킹BP의 SprintArm 컴포넌트 Pitch조정이 안되서 CemraSettings.InheritPitch 해제
3. ProjectSetting.DefaultModes = GameMode_SideFight(↑GameModeBase)
   DefaultPawnClass = MannequinBP
4. 맵의 진행방향을 X축으로 돌려서 제작 (PlayerStart.Yaw = 90 안함)

5. ProjectSetting.Engine-Input.AxisMapping에 SideFightForward 추가 (A:-1, D:+1)
6. 마네킹BP에 InputAxis-SideFightForward를 AddMovementInput.Scale에 연결 (Dir:1,0,0) 이동됨.

7. 씬상의 카메라를 뷰타겟으로 하는것에서 Reference얻는걸 버벅임.
   7.1. 아웃라이너에서 선택한 상태에서 블루프린트에서 우클릭하면 됨.
   7.2. 레벨BP에서 추가해야 한다. 마네킹BP에서는 추가 불가능.

8. 애니메이션 '이벤트'라는 용어가 아니다. 'Notify'이다. (한참 헤멤)
9. 애니노티는 각 애니 시퀀스에서 발생시킨다.
10. 액터에서 애니노티를 받으려면 AnimBP에서 한 번 포워딩 해 줘야 한다.
11. 마네킹BP.ClassSettings.Interface에 BluePrintInterface(BPI) 추가 가능.
12. 인터페이스 구현은 빨간색 노드. BPI는 우클릭.AddEvent 밑에 있다.
13. 호출은 2가지. Message는 조용히 실패. Function Call은 실패시 에러.
14. AnimNotify을 상속받아서 애니메이션의 세부 값을 받아올 수 있다.
15. AnimNotify도 Interface를 통해서 Actor로 접근해야 한다.

16. 단순히 PlayAnimation을 실행하면 애니메이션 관리가 깨져서 멈춰버린다.
17. AnimBP.AnimGraph 및 Functions/Variables를 이해해야 한다.
18. CharacterComponent에서는 Velocity,IsFalling을 업데이트하고 Transform업데이트만 한다.
19. AnimBP에서 Velocity/IsFalling을 가져와서 애니메이션 FSM에 적용한다.
20. 애니FSM에 Idle-Walk-Run → JumpStart~Loop~End의 세팅이 되어있다. (메카님처럼)
21. 따라서 시퀀스를 껴넣고 싶으면 FSM을 업데이트 해야한다.
22. 또한 CharacterBP에 신규 시퀀스와 연결될 파라미터를 업데이트해줘야 한다.
23. 또한 AnimBP에서 파라미터를 가져다가 사용하도록 작성할 수 있다.
24. 방식1) CharBP에서 AnimBP의 파라미터를 건드리는 방식
25. 방식2) AnimBP에서 CharBP의 파라미터를 가져오는 방식

26. 감을 잡았으므로 여기서 잠정중단.
```

# 개인메모3 (UnrealCodingEnv)
```
1. Contents 폴더에서 C++Class를 추가해도 C++Classes(PRJ/Source/Module/Public&Private)로 간다.
2. 언리얼 에디터에서 MyActor를 만들면 엄청 오래걸린다.
3. 언리얼 에디터에서 MyActor 지우는법을 모르겠다.
4. MyActor를 직접 지운 후 VC++에서 재빌드 해야 에디터에서 사라진다.
   (UnrealCodingEnv/Intermediate/Build/Win64/UE4Editor/Development/UnrealCodingEnv?)
5. gen경로: UnrealCodingEnv/Intermediate/Build/Win64/UE4Editor/Inc/UnrealCodingEnv
```

# C++ Version (조사중)
1. XCode 6.3, Clang (Apple LLVM Compiler Version 6.1)에서 C++14 완벽지원.
2. XCode 9 에서 C++17이 어느정도 지원되는지 모르겠다. [링크](https://forums.developer.apple.com/thread/79555)
3. NDK r16은 C++14까지 완벽지원 하는듯. C++17작업중이라고 함.
   [링크1](https://android-developers.googleblog.com/2017/11/update-on-kotlin-for-android.html)
   [링크2](https://www.phoronix.com/scan.php?page=news_item&px=Android-NDK-r16)
   

# Gameplay Framework 관련 메모 [UE Link](https://docs.unrealengine.com/latest/INT/Gameplay/Framework/index.html)
1. 

# 언리얼 자체 라이브러리 (TArray 등) 관련 메모
