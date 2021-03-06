
# 그래픽 컬러 처리

## 감마 수정

### 감마 수정

모니터 표면의 인점을 자극하여 밝게 혹은 어둡게 하는 것은 전자총에서 나가는 전자빔의 양, 즉 전자빔의 세기에 따라 좌우된다. 그러나 인점의 명도는 전자빔의 세기에 대해 비선형적인 반응을 보인다. 인점의 명도와 회색도와의 관계를 수식으로 표현하면

B = αδ<sup>γ</sup>

B는 인점의 명도를 나타낸다. 우변의 α는 비례상수를, δ는 정규화 회색도를 의미한다. 정규화 회색도는 최대값이 1이 되게 하는 것이다. 명도 B가 회색도 δ에 정비례하려면 승수γ가 1이어야 하지만, 실제로 그렇지 못하다는 데 문제가 있다. 감마 값은 사용된 인의 종류나 화면에 입혀진 모습 등에 따라 달라진다. 따라서 측정에 의해 구할 수 밖에 없지만 일반적으로 1.7 ~ 2.8의 값을 갖는다.

**감마 수정** 은 모니터의 이러한 문제를 수정하기 위한 작업을 말한다. 원래의 회색도를 γ라고 가정하자. 원래 회색도에 γ의 제곱이 곱해져서 왜곡이 일어나는 것은 물리적인 현상이므로 그대로 놓아둔다. 대신 사용자가 입력한 회색도 값에 1/γ 제곱을 미리 곱하여 수정된 입력 값으로 프레임 버퍼에 저장하면 된다. 이렇게 하면 나중에 왜곡에 의해 여기서 2.5승이 가해질 때 원래 값이 복원되기 때문이다. 이 과정을 수식으로 표현하면 다음과 같다.

B = α(δ′)<sup>γ</sup>  
B = α(δ<sup>1/γ</sup>)<sup>γ</sup>  
B = α(δ)

감마 값은 모니터의 종류에 따라 다르다. 이 경우 감마 수정은 하드웨어 또는 소프트웨어에 의해 이루어진다. 실리콘 그래픽스사느 컴퓨터나 애플사의 매킨토시 컴퓨터의 모니터에는 감마 수정을 자동으로 실행하는 하드웨어가 따로 내장되어 있다. 이는 하드웨어 스스로 실행하는 것으로, **하드웨어 감마** 라 불리며 1/γ = 1/1.4의 감마 수정을 갖는다.

일반적인 IBM PC에는 하드웨어 감마 수정 기능이 없다. 따라서 소프트웨어에 의해 감마 수정을 가해야 하며, 이를 **시스템 감마** 라 한다. IMB PC의 시스템 감마는 2.5정도로 1/γ = 1/2.5의 감마 수정을 가해야 한다. 소프트웨어적인 감마 수정은 실제로 감마 보기표를 이용한다.

IBM PC 도 그래픽 하드웨어 감마 수정을 행하는 그래픽 카드 종류가 있는데, 이때는 각별히 주의해야 한다. 만약 매킨토시 모니터의 감마를 2.5로 설정하려면 시스템 감마를 1.8로 해야 한다. 이미 하드웨어 감마 1.4가 있기 때문이다. 이 경우 총체적인 감마 수정은 (1/1.8)×(1/1.4) = 1/2.5에 의해 결정된다.

**파일 감마** 는 파일 자체에 해당 그림의 감마를 저장한 것이다. 만약 포토샵에서 스캐너를 동작시키는 과정에서 감마 파라미터를 1.8로 설정하면 스캔된 영상의 회색도에 1/1.8승이 곱해진 값을 기준으로 화면에 디스플레이 된다. 또 이 그림을 파일에 저장하면 곱해진 값으로 저장된다.
