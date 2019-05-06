# Builder
기초 컴퓨터 프로그래밍 01분반 강바다 마인크래프트 개인과제입니다. 프로그램 이름 그대로 지정된 좌표에 각종 건물들을 만들어 주는 프로그램입니다. 맨 처음 실행되었을 때 가로등, 주택, 도로의 세 가지 건물 중 어느 건물을 생성할지 입력받습니다. 그리고 각각의 건물 마다 입력받아야 하는 값이 조금씩 다르고, 입력 가능한 범위가 따로 존재합니다. ('과제'에 해당하는 부분은 2번 주택이고, 1번 가로등과 3번 도로 제가 개인적으로 한 번 추가해 보았습니다) 이는 값이 너무 크거나 작은 값을 입력받거나, 불필요한 값을 입력받았을 때 건물의 모양이 심하게 틀어지는 것을 막기 위함입니다. 물론 프로그램 실행 시 '~의 폭이 ~면 안 됩니다.' 처럼 별도로 표시됩니다. 한 번 건물을 생성하고 나면 다시 초기 화면으로 돌아가는데, 사용자가 프로그램을 재실행할 필요 없이 사용자가 원하는 만큼 건물을 만들 수 있습니다. 더 이상 건물을 만들고 싶지 않다면 4를 입력하여 프로그램을 종료할 수 있습니다.


1.가로등
-------------
1을 입력받았을 때, 가로등을 생성합니다. 가로등은 울타리와 발광석을 이용한 꽤 단순한 생김새입니다. 조명을 따로 넣기가 애매해서 간단하게 만들어 봤습니다. 가로등 특성상 크게 지어질 필요가 없으므로 한 지점만의 좌표를 입력받고, 대신 높이를 입력받습니다. 그리고 방향을 지정받는데, Positive x를 동쪽으로 취급하며 이를 기준으로 동서남북을 입력받습니다. 가로등은 입력받은 방향을 바라보게 지어집니다. 알고리즘은 단순합니다. 기준점에서 방향에 따라 가로등의 머리 부분이 다른 방향으로 배치되게 한 것입니다.

2.주택
-------------
2를 입력받았을 때, 주택을 생성합니다. 주택은 두 지점의 좌표를 입력받는데, 최소 x축 폭이 19칸, z축 폭이 14칸, y축 폭이 8칸 이상이어야 생성됩니다. 이 이상으로 생성이 되지 않게 막아둔 이유는, 샘플 건물을 최대한 압축시켰을 때 저 정도의 크기가 나오기 때문입니다. 더 작게 만들 경우 건물의 원형을 유지하기 힘드므로 입력에 제한을 두었습니다. 생성되는 건물은 집 근처에 깔리는 돌 바닥까지 포함되는 건물이므로 최소 크기의 건물을 생성했을 때 주택 자체는 꽤 작게 나옵니다. 또한 Super Flat 종류의 월드에서 주택을 생성할 때에는 앞서 언급했듯이 건물이 돌바닥까지 포함하므로, '현재 밟고 있는 블록'의 y축 위치, 즉 y=3을 시작점으로 잡아야 합니다. (두 지점의 좌표를 입력받았을 때 더 작은 쪽의 좌표가 시작점이 되도록 코드를 작성했으므로 따로 시작점을 고민할 필요는 없습니다.) 주택을 생성하는 방법은 주택을 부분으로 나누어 건설하는 방법과 같습니다. 시작점을 ex, ey, ez로 잡는데 이를 xyz축의 원점이라고 보면 됩니다(이 부분은 프로그램에 구현되어 있으므로 따로 조작해줄 필요는 없습니다) 기둥의 굵기나 문의 배치, 천장의 두께 등 크기에 따라 달라질 필요가 없는 부분은 (ex , ey, ez)를 기준으로 하는 고정 좌표계를 사용합니다. 그러나 벽면의 넓이, 유리판의 배치 등 좌표에 따라 그 크기가 천차만별로 달라질 경우 (ex, ey, ez)와 함께 (sx, sy, sz)를 사용합니다. sx, sy, sz는 두 지점의 좌표를 입력받았을 때 각 성분 별로 큰 값을 가지는 것만을 모아둔 좌표입니다. 예를 들어, ( 1, 2, 4 ) 와 ( 2, 3, 3)을 입력받았을 경우 ( 1, 2, 3 ) 이 ex, ey, ez가 될 것이고 ( e-좌표 ) ( 2, 4, 3 ) 이 sx, sy, sz가 되는 것입니다. ( s - 좌표 ) 이를 for문에서 처리하면 e-좌표가 s-좌표가 같아질 때까지 블럭을 계속해서 생성한다는 형식으로 프로그래밍이 가능합니다. 그렇게 했을 때, 할당되는 공간이 커지면 건물의 벽면이나 높이도 같이 커지게 할 수 있습니다.

3.도로
-------------
3을 입력받았을 때, 도로를 생성합니다. 도로는 두 지점의 좌표를 입력받되, y좌표는 한 쪽만 입력받습니다. 도로의 두께가 2칸이어야 하는 상황은 흔치 않기 때문입니다. 또한 x폭과 z폭이 같을 경우 건물이 생성되지 않는데 이 경우 중앙선을 결정할 수 없기 때문입니다. 물론 사용자가 원하는 방향으로 생성되게 할 수도 있지만, 애초에 도로는 교차로가 아닌 이상 길게 배치하는 편이기 때문에 굳이 코드를 더 복잡하게 하고 싶지 않아서 그렇게는 하지 않았습니다.

즉, 도로를 배치했을 때 폭이 긴 쪽으로 중앙선이 생깁니다. 또한 도로의 폭이 홀수일 경우 중앙선이 1칸으로 충분하지만, 짝수일 경우 한 칸으로 중앙을 표현할 수는 없으므로 짝수를 입력받았을 때에는 중앙선의 폭이 2칸이 됩니다.
