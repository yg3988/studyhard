# 투상 변환과 뷰 포트 변환

## 투상

### 투상

**투상** 은 3차원 물체를 화면으로 사상하기 위한 작업으로, 일명 **가시 변환** 이라고도 한다. 즉, 모델 좌표계, 전역 좌표계, 시점 좌표계를 순차적으로 거친 다각형 정점 좌표를 2차원 투상면으로 사상시키는 과정을 말한다.

관찰자 위치인 시점좌표계 원점을 **투상 중심** 이라 한다. 또 투상 중심으로 부터 물체 곳곳을 향한 선들을 **투상선** 이라 한다.  
카메라가 바라보는 방향을 **시선** 이라 한다. 카메라 설정 방법에 따라서 시선은 전역 좌표계 원점을 향하기도 하고, 임의 위치의 초점을 향하기도 한다. 물체 영상이 맺히는 역할을 하는 **투상면** 은 일반적으로 시선에 수직으로 놓인다. 결국 투상 중심에서 물체 정점을 향한 투상선이 투상면과 만나는 곳에 해당 정점이 **투상** 된다.

### 평행 투상

**평행 투상** 은 시점이 물체로부터 무한대의 거리에 있다고 간주하여 투상선을 나란히 가져가는 방법을 말한다. 이는 태양이 지구로부터 워낙 먼 거리에 있기 때문에 태양에서 지구로 향한 빛은 모두 평행 광선이라는 점과 비슷하다. 시점으로부터의 거리와는 무관하게 같은 길이의 물체는 같은 길이로 투상된다. 평행 투상은 다시 정사 투상, 축측 투상, 경사 투상 등으로 나뉜다.

**정사 투상** 은 평면도, 입면도, 측면도 등을 말한다. 모델 좌표계의 주축인 x, y, z에 의해 형성되는 x-y, y-z, z-x를 **주 평면** 이라 하면, 정사 투상의 투상면은 주 평면 중 하나와 나란히 놓이게 된다. 즉, 한쪽 면만 보인다.  
정사 투상에서 투상선은 투상면과 직교한다. 투상면에 맺힌 모습이 원래 물체의 길이를 정확히 보존하기 때문에 공학도면에 주로 사용된다. 그러나 투상선이 반드시 투상면과 직교해야 하므로 정사 투상에서의 시점 위치는 제한된다.

**축측 투상** 은 정사 투상이 물체의 한쪽 면만 보이는데 반해 한꺼번에 여러 면을 보여준다. 이 투상은 투상선이 투상면과 직교하다는 점에서는 정사 투상과 같지만 투상면이 반드시 주 평면들과 나란하지 않다는 점에서는 다르다. 투상면이 임의의 위치에 놓일 때를 **삼각**, 2개의 주평면에 대해서 대칭적으로 놓일 때를 **양각**, 3개의 주 평면이 만나는 모서리에서 모든 평면에 대해 대칭적으로 놓일 때를 **등각** 이라 부른다.  
축측 투상의 결과는 일반적으로 물체의 실제 모습이 아니다. 즉, 실제 길이가 보존되지 않으며 각 축의 방향으로 서로 다른 축소율을 보인다. 세 축 방향 모두 서로 다른 축소율을 보이는 것이 삼각 투상이며, 두 축에 대해서 동일한 축소율을 보이는 것이 양각 투상, 세 축 모두 동일한 축소율을 보이는 것이 등각 투상이다.

**경사 투상** 은 투상선이 나란하다는 점에서는 평행 투상에 속하지만 투상선이 투상면과 직교하지 않는다는 특징이 있다. 예를 들자면 고개를 돌리지 않고 눈동자만 돌려서 왼쪽 및 오른쪽 물체를 보는 것과도 비슷하다. 투상면은 시선에 수직이지만 투상면의 위치가 좌우로 비켜서 있다. 투상선끼리는 평행하다.

### 원근 투상

**원근 투상** 은 시점이 물체로 부터 유한한 거리에 있다고 간주하여 모든 투상선이 시점에서 출발하여 방사선 모양으로 퍼져가는 방법이다. 이는 카메라나 사람의 눈이 실제로 물체를 포착하는 방법이다. 원근 투상에서는 크기가 동일한 물체라도 시점으로부터 멀면 작게 보이고, 가까우면 크게 보인다. 따라서 물체의 원근감이 드러난다.

곧게 뚫린 도로를 길 가운데에 서서 보면 멀리 한점에서 만나듯이 원근 투상의 결과 실제 평행한 선이 만나게 된다. 이처럼 시점 높이에서 평행선이 만나는 점을 **소실점** 이라 한다. 소실점 수에 따라 원근 투상을 **일점 투상**, **이점 투상**, **삼점 투상** 등으로 나누기도 한다.

우리 눈이나 카메라가 물체를 포착하는 방법이 원근 변환이라는 점에서, 원근 변환의 결과는 매우 사실적으로 느껴진다. 직선을 원근 변환하면 결과도 직선이 되며, 평면을 원근 변환하면 결과도 평면이 된다. 어파인 변환과 원근 변환의 공통점은 변환 이전의 각과 거리가 변환 이후에 보존되지 않는 점이다. 그러나 어파인 변환과는 달리 원근 변환에서는 물체 정점 간의 거리에 대한 축소율까지도 달라진다.