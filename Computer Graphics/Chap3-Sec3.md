# 그래픽 컬러 처리

## 컬러 모드

### RGB 컬러 모드

**컬러 모드** 와 컬러 모델과는 별개의 개념이다. 프레임 버퍼의 내용이 R, G, B 값을 직접 담고 있는 경우를 **RGB 컬러 모드** 라 한다. 프레임 버퍼가 직접 R, G, B 값을 담고 있으므로, 이 모드에서는 화소별로 프레임 버퍼 값이 그대로 화면에 뿌려진다.

RGB 컬러 모드에서 화소당 8비트를 할애한다면 2<sup>8</sup> = 256가지의 색을 표현할 수 있다. 이 경우 R, G, B별 색의 세기는 [0, 255] 범위의 숫자로 표현된다. 만약 화소당 16비트를 할애한다면 R, G, B 각각에 5비트를 할애하고, 나머지 1비트를 미사용으로 가져갈 수도 있다. 그러나 이 경우 대개 G에 6비트를 할애한다. 우리 눈이 녹색에 대해 민감하기 때문에 녹색의 컬러 값을 더욱 자세히 표현하기 위해서다.

화소당 비트 수가 증가할수록 색 표현의 정밀도는 커지지만 그 만큰 프레임 버퍼 메모리의 용량도 증가한다. 색의 다양함을 표현하기 위한 트루 컬러, 풀 컬러, 하이 컬러 등의 용어는 과장 광고로 인해 고유의 의미가 사실상 거의 상실된 상태이다.

### 인덱스 컬러 모드

RGB 컬러 모드에 대응 되는 것이 **인덱스 컬러 모드** 다. 이 모드에서 프레임 버퍼의 비트 값은 R, G, B 컬러 값이 아니라 컬러 보기표(CLUT)의 첫 칼럼인 인덱스 값을 의미한다. 실제 색은 컬러 보기표의 둘째 칼럼에 있는 비트 값에 좌우된다.

컬러 보기표는 R, G, B별로 존재한다. 물론 이를 위해서는 그래픽 카드내에 컬러 보기표를 저장하기 위한 별도의 메모리가 필요하다.

인덱스 컬러 모드를 사용하면 컬러의 정밀도를 높일 수 있는 장점이 있다.

| 프레임 버퍼(RGB) | 보기표(R) | 보기표(G) | 보기표(B) |
| :-------------   | :-------: | :-------: | :-------: |
| 000(0)           | 00011100  | 11000000  | 10010011  |
| 001(1)           | 11001001  | 00010100  | 01011100  |
| 010(2)           | 10010000  | 10010011  | 00010101  |
| 011(3)           | 00110001  | 00111001  | 00110000  |
| 100(4)           | 11110101  | 01010011  | 11001111  |
| 101(5)           | 01011000  | 10110100  | 10110101  |
| 110(6)           | 00100011  | 01010101  | 01011100  |
| 111(7)           | 10111100  | 11111100  | 11111001  |
[표 1] 컬러 보기표

표와 칼럼같이 R, G, B에 각각 8비트를 할애하면, 색 표현의 정밀도는 2<sup>3</sup> 에서 2<sup>24</sup> 으로 증가한다. 하지만 한 화면에 1,600만 컬러를 동시에 보여줄 수 없다. 1,600만 컬러 중에서 8가지 색의 비트 값만이 선택된다. 그 이유는 프레임 버퍼가 표현할 수 잇는 인덱스의 숫자가 8가지로 제한되어있기 때문이다. 결과적으로 선택할 수 잇는 컬러의 종류가 다양해질 뿐, 한 화면에 동시에 보일수 있는 컬러의 개수는 여전히 8가지임에 유의해야 한다.

인덱스 컬러 모드는 적은 프레임 버퍼 용량으로 다양한 컬러를 표현하기 위해 고안된 것이다. 웹 브라우저에 인덱스 컬러 모드가 주로 사용되는 것은 이 때문이다. 웹 브라우저는 고급 컴퓨터는 물론 저급한 성능의 컴퓨터에도 돌아가야 하고, 일반적으로 저급 컴퓨터의 프레임 버퍼 용량은 제한적이기 때문이다.

그래픽 파일 중 인덱스 컬러 모드를 지원하는 형식은 PNG, BMP, TGA, TIFF 등의 확장자로 끝나는 파일로, 이들 파일은 내부에 컬러 팔레트 값을 포함하고 있다.
### 컬러 팔레트

인덱스 컬러 모드에서 컬러 보기표가 나타내는 색의 집합을 **컬러 팔레트** 라 한다. 인덱스 컬러 모드에서는 프레임 버퍼 내용은 인덱스일 뿐 실제 컬러를 의미하지 않는다. 즉, 동일한 프레임 버퍼 내용이 팔레트 내용에 따라 다르게 사상되어 컬러 표현이 달라질 수 있음을 뜻한다. 인덱스 컬러 모드는 그림의 색조가 유사할 때 효과적이다. 청개구리의 예를 들어 R, G, B 각 3비트를 할애한 프레임 버퍼를 가정해보자. 만약 RGB 컬러 모드를 사용한다면 적색과 청색 성분은 거의 없을 것이다. 때문에 R, B 비트 값은 항상 000이 된다. 결국 녹색 3비트만으로 그림을 표현해야 하므로 가능한 녹색의 수는 2<sup>3</sup> = 8가지가 된다. 원래 프레임 버퍼가 표현 할 수 있는 색의 수는 2<sup>9</sup>(=512)가지 임에도 불구하고 그 중의 극히 일부만 활용 되는 것이다.  
인덱스 컬러 모드를 사용하면 2<sup>9</sup>가지가 모두 인덱스로 작용한다. 이 인덱스에 다양한 녹색 계통의 색만을 할당함으로써 더욱 자세한 표현이 가능해진다.
