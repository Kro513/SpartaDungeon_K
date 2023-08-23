# 스파르타던전 개인과제
08.18.~08.23.
## 기본 목표
1. 게임 시작 화면
2. 상태창
3. 인벤토리
## 최종 구현
1. 게임 시작화면
2. 상태창 (아이템 능력치 반영 구현 실패)
3. 인벤토리 (인벤토리 창은 만들었으나 장착관리와 아이템 정보 반영 구현 실패)
### 장착 관리 구현 계획
장비착용 함수를 만들고, 한번 불릴 때 마다 *-1을 해주어 if문을 사용해 양수일 경우 착용중, 음수일 경우 미착용으로 구현하려고 했음.
### 내가 생각하는 장착 관리 구현 실패 이유
1.매개변수 선언에 대한 이해도가 낮아 뭘 넣어야 하는지 모름.

2.함수의 위치가 어디로 들어가야하는지 모름 (함수를 만들었으나 막상 불러오는곳에선 현재 컨텍스트에 없다고 오류 발생)

3.CheckValidInput의 switch문에서 case를 어떻게 설정해야 장착관리창에서 떠나지 않고 장착만 관리 할수 있는지에 대한 이해도 부족.

4.장비가 착용되었을때 상태창에 반영하는 방법을 모름.
## 개선해야할 방향
우선 코드가 전체적으로 어떻게 흘러가고 서로 어떤식으로 작용하는지에 대한 이해가 필요하다고 느낌.

함수를 만드는데 있어서 필요한 요소나, 함수가 어디에 있어야, 어떻게 만들어야 내가 원하는대로 정상적으로 작동하는지에 대한 더 자세한 공부가 필요함.

문제가 생겼을때 도움을 청하는것이 아직 어려움. 조금 더 용기를 내서 물어봐야 할것 같음.
## 중간에 생겼던 문제
github에 올리는 과정중 이전 파일들이 덮어 씌워지면서 일부가 날아가는 현상이 발생.

아직 git을 사용하는것이 어렵다.
