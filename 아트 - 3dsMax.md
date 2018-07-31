# 3dsMax StudyNode


## 맥스강좌
1. [MinSoo Kang](https://www.youtube.com/playlist?list=PLMQNGoRCimQWorSNZgaJ1kbxzVaRZgXaX)


## 핵심요약
1. 맥스는 모델링, 애니메이션, 물리처리 종합툴
1. 설치 후, 단축키와 단위 설정을 가장 먼저 한다. Customize-UserInterface/Units에서 설정. (1격자 = 10Units)
1. 작업의 핵심은 EditablePoly조작과 다양한 Modifiers 이용 및 스택관리
1. 작업내내 균등한 사각형 폴리곤 형태를 유지해야 이후의 작업이 매끄럽다.
1. 툴바의 ReferenceCoordinateSystem 콤보리스트 활용 (작업 좌표계 타입)
1. 커맨드 판넬 구조: 만들기 | 수정하기 | 계층 | 모션 | 디스플레이 | 설정

## 단축키 설정

| 단축키 | 기능 설명 |
| --- | --- |
| Z | 오브젝트 포커싱 |
| Ctrl+Shift+Z | 모든 오브젝트 포커싱 |
| G | 그리드 표시 토글 |
| J | 오브젝트 선택 개미선 토글 |
| F4 | 오브젝트 엣지 표시 토글 |
| F3 | 와이어프레임 표시 토글 |
| 8 | 렌더 배경색 |
| 9 | 렌더 |
| Alt+W | 1 뷰포트 전체화면 토글 |
| Alt+X | X Ray |
| Ctrl+X | 전문가 모드 |
| Alt+휠드래그 | Dolly |
| Ctrl+Alt+휠드래그 | 마이크로 줌 |
| Ctrl+우클릭 | 뷰포트 메뉴 - 모델링 primitives |
| Shift+우클릭 | 뷰포트 메뉴 - 스냅 |
| Alt+우클릭 | 뷰포트 메뉴 - 애니메이션 |
| Ctrl+Alt+우클릭 | 뷰포트 메뉴 라이트/렌더 |
| Shift+드래그 | 오브젝트 복사 |
| Spacebar | Selection LOCK Toggle |
| F2 | 언랩 면 표시 토글 |
| M | 머티리얼 편집기 |


## 뷰포트
| 기능 | 기능 설명 |
| --- | --- |
| [+] | 뷰포트 설정 |
| HOME | 뷰포트 구석에서 우클릭 후 HOME 또는 집모양 아이콘 |

## EditablePoly
1. 1, 2, 3, 4, 5로 Edit 단위 변경
1. Vertex
   1. Collapse : 점 합치기 - 선택된 것
   1. Weld : 점 합치기 - 전역
1. Edge
   1. Bridge - 면 2개의 엣지 사이를 메꾼다.
   1. Edge를 마주보게 선택 후 Connect - 갈라놓음
1. Border
   1. Cap - 구멍 메꾸기 (Alt+P)
   1. Spherify - 구 형태로 (?)
1. Polygon
   1. Shift드래그로 면 생성
1. 팁
   1. 값 창에서 우클릭시 0으로 리셋
   1. 모디파이어 적용시 Ctrl+PageUp/Dn으로 범위 확대/축소
1. 기법들
   1. 점-점 Connect
   1. Line -> 베지어 -> Attach -> Surface
   1. Line -> Lathe
   1. Plane -> Displace Heightmap
   1. Loop / Ring
   1. SwiftLoop = Ring+Loop
   1. Vertex Break = Edge Split
   1. Extrude + = Bevel
   1. Connect는 새 폴리곤을 만든다. 따라서 같은 평면에 있어야 한다.
   1. Object, 폴리곤에 Line은 어태치 불가

## 모디파이어 탭
1. Shift 드래그: 이동
1. Ctrl 드래그: 인스턴스 (우클릭 메뉴로 복제 가능)
1. Pin: 다른 오브젝트를 선택해도 기존 것 계속 수정
1. SelectionSet -> Use Pivot Points -> Add Modifier

## 계층구조 탭
1. 피봇만 처리 가능
1. Mirror대신 Symmetry 사용할 것

## UV언렙 메모
> CheckPattern으로 뷰포트의 면 체커가 정사각형으로 나와야 한다. 잘 안되면 UV Editor에서 Freeform 누르고 수동 보정
1. 언랩
   1. 면 선택
   1. Pelt 클릭
      1. Start Pelt
   1. 릴렉스 세팅 - Face
   1. Start Relax
   1. Connect
1. UV맵상에 모두 배치
   1. Seam을 Alt-클릭시 심 삭제
1. Render UV Template
1. 저장

## 성욱팁
1. 근접작업: ViportClipping 우측의 Near/Far 세팅
1. Chamber: 곡면
1. 엣지 선택상태에서 Ctrl+1 => 버텍스 선택으로 전환됨
1. 엣지 선택상태에서 x스케일: 동일 간격으로 위치 보정
1. 버텍스 Constraint: None/Edge 이동제한 Shift+X
1. 굴뚝 작업: 그냥 떨어진채로 작업.
1. 로우폴(뼈대) -> 하이폴(디테일) 방향으로 제작
1. Cut으로 엣지 추가

