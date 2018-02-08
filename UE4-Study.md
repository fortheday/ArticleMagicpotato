# Unreal Engine 4 Study note
* 2018-01-29. magicpotato.

# 공부방법 (매우 중요)
> 언리얼 엔진을 공부하는 방법에 대한 가이드라인

1. 완전히 새로 배운다고 생각해야 한다. 용어도 의심없이 받아들여야 한다.
   > '유니티 프로그래머를 위한 언리얼'강의같은 건 도움이 안된다.
2. 훑어보고 → 해보고(까먹고) → 한번 더 보는 정도로 학습하는게 효율적이다.
   > 양이 많고, 생소한 용어나 개념이 많기 때문.
3. 학습중인 강의 주제에만 집중한다.
   > 궁금한 것들이 처음에는 어차피 빠르고 쉽게 파악되지 않기 때문이다.

4. 프로그래머는 다음 순서대로 익힌다.
   1. 아티스트로서 언리얼 에디터를 다루는 법 (No코딩)
   2. 스크립터로서 언리얼 에디터를 다루는 법 (블루프린트)
   3. 언리얼 에디터상에서 만들 수 있는 C++ 클래스등의 코딩 방법
   4. 위 단계 학습중에 **프로그램적 구조**에 대한 의문은 미뤄두자. (비효율적이다)
   5. 언리얼 에디터의 소스를 클론받아 빌드하고 개선하는 법 <가능한 늦게>

5. 학습분야
   1. 메인창내의 모든 탭의 목록과 용도
   2. 모든 리소스 타입의 목록과 용도 + 연관 서브에디터들 (메쉬창, 매터리얼창, 블루프린트창 등등)
     1. 모든 에셋 타입 이해
        1. 에셋별 프로퍼티 값 이해 (한 에셋별로 완전격파는 어렵다. 점진적으로 공부하자)
   3. 게임모드, 프로젝트 환경설정 이해
   4. 프로젝트 폴더 구성 이해 → 쿠킹 폴더 구성 이해 → 엔진 폴더 구성 이해
..... **TODO**

6. 학습자료
   1. 언리얼 에디터의 전반적 기능을 다루는 가장 **얇은** 책 한권을 '지도'로 삼는다.
      > 추천하는 책을 봤는데도 설명이 난해하다. 단지 '목차'용도로만 쓰고 아래 자료로 공부.
   2. [네이버카페-입문강의](http://cafe.naver.com/unrealenginekr/735)
   3. [언리얼서밋-중급강의](http://replay.unrealsummit.co.kr/)
   4. [언리얼공식 문서](https://docs.unrealengine.com/latest/KOR/)



# 최소 용어

1. 에셋: Content Browser에 등록된 것들 (배치안됨)
2. 액터: Map에 배치된 것들
3. PBR: 표면을 물리적으로 정의한 체계로 매터리얼을 구성하는 것
4. SubUV: 고전 스프라이트 텍스쳐 (NxN으로 잘라서 사용하는 용도 - 2D, 이펙트)

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


# Gameplay Framework (GameMode) [UE Link](https://docs.unrealengine.com/latest/INT/Gameplay/Framework/index.html)

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
   2. 메시: LOD 설정, 물리/천 설정, 매터리얼 설정 등
   3. 애니메이션: 애니메이션 설정, 소켓/노티파이 설정, 각 시퀀스 편집 등
      1. 그래프편집: 애니메이션 블루프린트 편집 (애니메이션간 블렌드, 이벤트 등 제어)
   4. 물리: 물리 설정


# 애니메이션 창 (2)
1. 편집 뷰
   1. Notifies: 노티파이
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
  1. 한번 더 깊게 공부: 파티클, 액터애니메이션, 시네마틱, 사운드에셋구조 별도공부
  2. 물리용어
     - damping 감쇠(회복력)
     - friction 마찰력
     - restitution 탄성(회복력)
     - impulse 충격량
