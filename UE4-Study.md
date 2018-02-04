# Unreal Engine 4 Study note
* 2018-01-29. magicpotato.


# 학습방향/컨셉
> 기술지원이 가능한 언리얼 프로그래머 (그래픽디자이너, 기획자를 위함)
1. 1단계: 언리얼 사용법 학습
   1. 에디터 모든 기능 사용, 이해
   2. 모든 에셋 타입 이해
   3. 에셋별 모든 프로퍼티 값 이해
   4. 프로젝트 환경설정 내 모든 항목 이해
2. 2단계: 블루프린트, C++코딩 가능
3. 3단계: 엔진 소스코드 수정 가능 (장기)


# 최소 용어

1. 에셋: Content Browser에 등록된 것들 (배치안됨)
2. 액터: Map에 배치된 것들


# Editor 구성
1. Viewport: 씬 에디터
2. World Outliner: 맵에 배치된 모든 액터 목록
3. Details: 선택된 액터
4. Content Browser: 개발자 에셋
5. Modes: 엔진 에셋 등 **Mode라는 용어를 쓴 이유를 알아야 한다**
6. Layers: 액터 레이어 관리

# Unreal4 Folder Structure

1. No StarterPackage, Blank Project 생성
2. ContentsBrowser에서 Show in Explorer 클릭
3. 폴더 내용 확인

| Folder       | Desc | SVN |
| ---          | --- | --- | 
| Config       | ini파일들, 내 게임/에디터 기능의 세팅값들) | 버전관리 |
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
1. Forward = X
2. RIght = Y
3. Up = Z

![CoordSystem](http://usarsim.sourceforge.net/wiki/images/2/24/Figure24.jpg)


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
   


# 코드 실행순서
1. 클래스 생성자
2. 에디터 설정값 세팅
3. 클래스 BeginPlay()

