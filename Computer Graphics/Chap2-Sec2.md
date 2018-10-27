# 컴퓨터 그래픽스 2장

## 컬러모니터

### 래스터장치

래스터 장치에서의 화면은 화소로 구성되어있다. 여기서 **래스터(Raster)** 는 '화소'를 의미한다.

컬러 모니터는 R,G,B 색을 띤 인점으로 구성되어 있으며, 인점 배열 방식에 따라 두 가지로 구분된다.

- 트라이어드 : 삼각형 내부 3개의 인점이 모여서 한 화소를 구성, 이 경우 서로 엇갈려서 구성됨
- 스트라이프 : 좌우로 나란한 4개의 인점이 모여서 한 화소를 구성한다.

래스터 장치의 선명도, 즉 해상도는 화소수에 의해 결정된다. 예를 들어 1,024 × 768 해상도에서 가로 방향 화소 수는 1,024개, 세로 방향 화소 수는 768개다.

### 섀도마스크

컬러 모니터에는 3개의 전자총이 사용된다. 전자총과 화면 사이에는 **섀도 마스크**(Shadow Mask)가 있고, 여기에는 아주 미세한 구멍들이 뚫려있다.
각 전자총이 정확히 해당 색상의 인점을 맞추도록 되어 있다.   
섀도마스크가 없을 경우 전자빔이 휘어 동일 화소 또는 인접 화소의 다른 인점을 자극 할 수도 있기 때문에 섀도 마스크 기술은 화면의 선명와 직결된다고 할 수 있다.

### 주사선

래스터 장치는 화소보다 작은 단위로 분할하여 한 화소의 아래쪽은 밝게, 가운데는 어둡게 할 수는 없다.

화면의 가로 방향 화소를 따라 진행하는 선을 **주사선** 이라 한다. 따라서 1,024 × 768 해상도에서 주사선 수는 768개가 된다.

### 인터레이싱

주사선이 화면을 반쪽씩 교대로 그려내는 것을 **인터레이싱** 이라고 한다.  즉, 1번 주사선, 3번 주사선, ..., 화면의 끝까지 내려와서 이제 2번 주사선, 4번 주사선, ..., 화면의 끝까지 주사하는 것을 뜻한다. 전체 화면을 초당 30번 재생하도록 요구 될 때 인터레이싱 방식에서는 반쪽 화면을 60번 주사한다.(60Hz)  
반면 **논-인터레이싱** 에서는 실제로 전체 화면을 30번 주사한다.  
전체 화면을 30번 주사하는 것과 반쪽화면을 60번 주사하는 것은 하드웨어로서는 비슷한 부담이다.

인터레이싱 방식의 중요성은 재생 속도에 있다. 논-인터레이싱을 사용하면 모든 주사선을 이어서 주사하며 내려오기 때문에 화면 재생속도가 느리다. 그로 인하여 첫번째 화면과 둘째 화면 사이의 시간 간격이 길어져 화면에 깜빡거림이 발생한다.  
반면 인터레이싱 방식에서는 화면 내용을 반쪽 영상에 불과하지만 두 배 속도로 뿌려지기 때문에 화면이 매우 부드럽게 느껴진다.

### 스캔 변환

스캔 변환 혹은 래스터 변환이라 불리는 이 일련의 과정은 래스터 장치에서 필수 작업이다.  
임의의 두 점이 있을 때 화면의 어떤 화소가 선분의 양 끝점에 해당하는지, 내부의 선은 어떤 화소들을 사용하여 표현할 것인지를 결정해야 한다. 이처럼 물체의 수학적 표현으로부터 화면 화소 단위의 표현으로 변환하는 과정을 스캔 변환 또는 래스터 변환이라고 한다.

### 프레임버퍼

**프레임 버퍼** 는 컬러 버퍼 혹은 비디오 메모리라고도 부른다.  
래스터 장치의 화면 그림은 프레임 버퍼에 저장되어있다. 이는 그래픽 프로세서에 내장된 메모리로서 화소당 밝기, 즉 색상을 저장하는 곳이다.  
화소당 1비트를 할애하는 프레임 버퍼로, 백색은 비트 값 1로 흑색은 비트 값 0으로 표시할 수 있다.  
그림이 바뀔 경우, 호스트 컴퓨터는 프레임 버퍼의 내용을 바꾸기만 하면 비디오컨트롤러가 바뀐 내용을 화면에 뿌리게 된다.  
프레임 버퍼의 용량은 색상의 종류와 연관되어있다. 화소당 1비트를 할애할 경우 흑백 정보만 저장하지만 화소당 3비트를 할애할 경우 각각의 비트 값을 R, G, B값으로 해석할 수 있고 색깔을 표현할 수 있다. 3비트는 1비트 프레임 버퍼를 나란히 나열하여 표시할 수 있으며, 이 경우 1비트 프레임 각각을 비트 평면이라고 한다.

### 비디오 컨트롤러

**비디오 컨트롤러** 란 프레임 버퍼에 저장된 내용을 화면에 뿌리는 역할을 하는 장치로 비디오 컨트롤러 내부에 **DA 변환기(DAC)** 가 내장되어 있기 때문에 전자빔이 어떤 화소를 주사할 때 프레임 버퍼의 디지털 비트 값에 비례하는 아날로그 전압으로 변환시켜 해당 화소의 밝기를 조절할 수 있다.

### 회색도

9비트 프레임 버퍼에는 R, G, B를 각각 3비트씩 할애할 수 있다. 예를 들어 R, 즉 적색의 밝기를 세분하여 000부터 111사이의 값으로 할당할 수 있다. 주어진 색상의 밝기를 **회색도** 라 한다.  
화소당 24비트를 할애한 프레임 버퍼의 경우 R, G, B를 각각 8비트씩 할애할 수 있고, 밝기는 10진수 0부터 255까지 256(=2<sup>8</sup>)로 구분할 수 있다.  결과적으로 24비트 프레임 버퍼로 나타낼 수 있는 색상의 수는 256×256×256≒1,600만 정도 표시할 수 있는데 사람의 눈은 대략 35만 가지 정도의 색을 구별할 수 있기 때문에 1,600만 가지 이상의 색을 풀 컬러라 부르기도 한다.

### 해상도

프레임 버퍼의 용량은 해상도와도 연관되어 있다. 예를 들어 1,024×768 해상도의 그림은 1,024×768개의 화소로 구성되어 있다. 화소당 24비트를 할애하면 프레임 버퍼의 용량은 1,024×768×24bit≒2.4MB가 된다.