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


# 코드 실행순서

1. 클래스 생성자
2. 에디터 설정값 세팅
3. 클래스 BeginPlay()

