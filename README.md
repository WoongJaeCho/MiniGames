# Camel UP

평소 즐겨하는 보드게임 중 하나인 카멜업을 자바스크립트로 구현 하겠다.

1. 게임의 개요
  - 낙타 경마를 소재로 한 게임이다.
  - 낙타는 5가지 색깔이 있다. 해당하는 색의 주사위를 랜덤으로 굴려 해당하는 숫자 칸 만큼 전진한다.
  - 낙타는 서로 탈 수 있으며, 아래의 낙타가 움직이면 위의 낙타도 같이 움직이게 된다.
    
  - 플레이어는 해당 라운드의 1등말에 배팅, 주사위 돌리기, 타일 놓기, 최종 1등 낙타, 꼴지 낙타에 배팅할 수 있다.
  - 배팅에 성공하면 해당하는 코인을 얻을 수 있고, 실패시 코인을 잃는다.
  - 1등말이 골인지점에 도착하면, 게임은 종료되고, 코인이 가장 많은 플레이어가 승리한다.

2. 게임 준비 
  - 게임 보드 1번 트랙 ~ 16번 트랙
  - 낙타 색깔 5가지 ( green, yellow, red, blue, white )
  - 배팅 타일   
3. 낙타의 이동
  - 주사위 색깔에 따라 해당 낙타 이동
  - 먼저 도착한 낙타 위에 나중에 도착한 낙타가 업힐 수 있다.
  - 아래 낙타가 이동하면 위의 낙타는 같이 움직인다.
  - 위의 낙타가 순서상 앞선다.   
4. 라운드 구성
  - 플레이어는 본인 차례에 4가지 행동을 할 수 있다.
    (1) 배팅 타일 가져오기
    (2) 사막 타일 놓기
    (3) 주사위 드롭
    (4) 최종 승부 예측
  - 한 라운드는 낙타의 이동이 한번씩 완료되면 해당 라운드가 종료된다.
    한 라운드 종료 후 배팅 결과, 주사위 드롭 에 따른 코인을 획득하거나 잃게된다.      
5. 배팅
  - 낙타의 순위에 따라 배팅 금액을 획득하거나 잃게된다.
6. 게임 종료
  - 1등 낙타가 결승선을 통과하면 게임은 종료된다.
  - 코인이 가장 많은 플레이어가 우승한다. ( 코인의 수가 같으면 공동우승 )

//---------- 진행 순서 ------------//
[1] 보드판 제작
[2] 주사위 던지기
  [2-1] 주사위 색깔별 한번씩만 나오기.
  [2-2] 모든 주사위 나온 후 초기화.
[3] 낙타 옮기기
  [3-1] 처음 시작 낙타 놓기
  [3-2] 우선 한마리씩 움직이기
[4] 아래의 낙타 움직일 경우 위의 낙타 같이 움직이기
  - 아래의 낙타가 움직이면서 위에 같이 이동하는 낙타의 포지션까지 같이 바꿔줘야 하기때문에 시간이 걸림.
[5] 플레이어 턴 적용
[6] 카드 드래그 해서 플레이어 공간으로 옮기기
  [6-1] 한 플레이어에게 카드 들어가게 만들기.
  - appendChild 기능과 비슷하게 없애지 않고 복사만 할 수 있을까?
  -> (복사할 객체).cloneNode(true) -> true 가 없으면 content가 복사가 안된다.
    (옮길 부모).before/.after() 사용하여 해결 (구글링) -> 자식의 요소가 아닌 형제의 요소로 들어간다.
  -> 복사만 하여, appendChild 사용함.
  [6-2] 다른 플레이어에게 카드 들어가게 만들기.
  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@ [6-3] 자신의 턴에만 카드 들어가게 만들기 @@@@@@@@@@@@@@[처리 못함]@@@@@@@@@@@@@
  [6-4] 카드 점수 낮추기 5 -> 3 -> 2 -> ''
  -> '' 일때 setAttribute('draggable','false') 사용하여 드래그 막아 놓음.   
[7] 5마리 낙타 모두 움직인 후 보드판 초기화
[8] 초기화 후 코인 계산
  [8-1] 1등마 찾아서 카드 가진 플레이어 코인 증가
  [8-2] 2등마 찾아서 카드 가진 플레이어 코인 증가
  [8-3] 카드 가진 수 만큼 플레이어 코인 감소
[9] 주사위 코인 증가
//---------- 현재 진행 ------------//
[10] 1등 낙타 골인 
[11] 최종 계산 후 코인 비교
[12] 우승 플레이어 출력

[13] 최종 1등 / 꼴등 낙타 배팅 화면  
[14] 주사위 애니메이션 구현
[15] 낙타 이동 자연스럽게 한칸씩 움직이기
