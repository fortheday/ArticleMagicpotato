# UMG 만능용어 '위젯'과 관련된 몇가지 중요한 개념

* 2018-04-03. magicpotato.

## 위젯은 여러가지 의미를 갖는 난해한 용어이다. 전라도의 거시기처럼.
1. UI(컨트롤)를 의미 
1. WidgetBlueprint를 의미 -컨텐츠 브라우저 우클릭으로 생성한 에셋-
   1. 위젯의 집합, 위젯 덩어리 개념
   1. 컨텐츠브라우저에서 에셋 툴팁에는 NativeParent: UMG.UserWidget으로 표시
   1. 위젯에디터 우상단에 부모클래스가 User Widget으로 표시
   1. 위젯에디팅 중인 (다른)WidgetBlueprint의 계층구조에 배치 가능
1. Component를 의미 -위젯에디터 팔레트에 나열되는 UI컨트롤들-
   1. 위젯에디팅 중인 WidgetBlueprint의 계층구조에 배치 가능
   1. 내부에서 또 다른 'Component'라는 의미가 있으므로 주의
1. UWidget 클래스 -엔진사용자가 Cpp상속받을 수 있는 Component(위젯)의 구현-
1. UUserWidget 클래스 -엔진사용자가 상속받을 수 있는 Widget(Blueprint)의 구현-
   1. 상속: Cpp클래스 상속, 위젯에디터에서 Reparenting으로 지정가능

## WidgetBlueprint를 구성하는 구조 (좀 더 정체를 파악할 필요가 있다)
1. UUserWidget (WidgetBlueprint) - Controller?
   1. UWidget (Components) - ?
      1. SWidget (Slate) - View?

## UMG의 계층구조 구성 방식, 관련용어
1. 아래로는 Child, Descendant, Inner의 용어를 혼용. 위로는 Parent, Outer 용어를 혼용.
1. UMG는 WidgetTree와 Slot(Panel=Container)을 혼용하며 계층구조를 구성한다.
1. UserWidget.WidgetTree
   1. 위젯 집합을 계층구조로 구성할 수 있도록 함
   1. 위젯에디터에서 디자이너가 구성 함.
   1. ZOrdering 역할도 함.
   1. Root는 단 하나
1. UWidget.Slot, UPanelWidget.Slots
   1. 슬롯은 소유자가 갖는 그릇. 피 소유자는 소유자의 슬롯에 담긴다.
   1. 위젯의 종류에 따라서 0 개, 한 개, 한 개 이상의 자식(위젯)을 가질 수 있다.
      1. Leap Widget은 자식을 가질 수 없다. (Image, Text같은 것)
      1. Button Widget은 한 개의 자식을 가질 수 있다.
      1. Panel은 여러 개의 자식을 가질 수 있다.
1. (Cpp)Class member <좀더 조사 필요>

## 기타정보
1. UserWidget을 상속받은 Native(Cpp)위젯은 위젯팔레트에 나열되지 않는다. (SPaletteView::BuildClassWidgetList참고)

EOF
