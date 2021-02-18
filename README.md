# Study_For_Game
 게임프로그래밍에 필요한것들 공부하기
<br>
<br>
<br>
<br>

## 피타고라스의 정리<br>
상식(?)이므로 굳이 정리를 설명하진 않겠다.
<br>

![피타고라스](https://user-images.githubusercontent.com/43705434/108397930-d5d49000-725b-11eb-857e-d866645d6d2e.png)
<br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;				b(100, 80)<br>
<br>
<br>
a(20, 20)
<br>
<br>

**_EX)_**<br>
a에서 b까지 오브젝트가 이동해야 할때 **iTween.MoveTo(obj, Destination, time);** 을 자주 사용한다고 한다.<br>
이때 time 값을 어떻게 구할 것인가?<br>
<오브젝트는 40/sec로 일정하게 이동한다.><br>

이런 경우에 피타고라스의 정리를 이용해서 a와 b 사이의 거리를 구하고 해당 거리를 40/sec 로 나누어주면<br>
적절한 time 값을 구할 수 있을 것이다.<br>
<br>

a와 b 사이의 거리를 c라고 할때 피타고라스 정리에 의해 **c = √(60² + 80²)** 가 성립되며 **c = √10000 = 100**이 된다.<br>
고로 적절한 time 값은 **100 / 40 = 2.5**초라는 것을 알아낼 수 있다.<br>

Unity에서는 피타고라스를 이용하는 **Vector3.Distance** 함수를 이용해서 간단한게 오브젝트간의 거리를 구할 수 있다.<br>
(두 벡터의 차를 구한 후 해당 벡터의 길이를 구함)<br>
<br>


## 선형대수학<br>
선형 + 대수의 의미를 갖는데 자세히 살펴보자.<br>
<br>
선형이라는 의미는 x^2 이나 x^3이 아닌 2x, 3x 처럼 직선을 이루는 것을 의미한다.<br>
즉, 어떤 데이터의 발전은 직선을 따라서만 오르거나 내릴 수 있다고 생각하면 된다.<br>

**<선형에 대한 증명>**<br>
함수 와 임의의 수 에 대해 아래와 같은 식이 성립할 때 함수 는 선형이라고 한다.<br>
> 조건 1: f(x+y) = f(x) + f(y);<br>
> 조건 2: f(ax) = af(x);
<br>

예)<br>
f(x) = 5x<br>
g(x) = 2x²<br>
h(x) = 2x + 4<br>

f(x+y) = 5x + 5y = f(x) + f(y)<br>
f(ax) = 5ax = af(x)<br>
위 조건을 만족하므로 선형<br>

g(x+y) = 2(x+y)² = 2x² + 4xy + 2y²<br>
g(ax) = 2(ax)² = 2a²x²<br>
위 조건을 만족하지 못함.<br>

h(x+y) = 2(x+y) + 4 = 2x + 2y + 4<br>
h(x) + h(y) = 2x + 4 + 2y + 4 = 2x + 2y + 8<br>

h(ax) = 2ax + 4<br>
ah(x) = a(2x + 4) = 2ax + 4a<br>
위 조건을 만족하지 못함.<br>

즉, 다항함수에 대해서는 이차함수 이상의 고차함수는 선형성을 가질 수 없으며<br>
일차함수의 경우에도 원점을 지날 경우에만(y절편이 0일 경우에만) 선형성을 가짐을 알 수 있다.<br>

Algebra(대수)는 큰 수가 아니라 어떤 다른 것이 수를 대신한다는 것이다.<br>
프로그래밍을 할때 항상 변수를 사용하기 때문에, 대수를 사용하고 있던 것.<br>

**결론적으로 선형대수학은 선형성을 띄는 즉 선형방정식의 해를 구하기 위한 학문이라고 할 수 있다.<br>
<벡터 공간, 벡터, 선형 변환, 행렬, 연립 선형 방정식 등을 연구하는 대수학의 한 분야>**<br>
<br>


## 벡터<br>
<img src="https://user-images.githubusercontent.com/43705434/108397929-d4a36300-725b-11eb-89ca-a6cbd1d5c637.jpg" width="500" height="300">
<br>

**개념**<br>
보통 교과서에는 벡터를 '크기와 방향을 가진 양'으로 정의하고, 크기만 갖고 방향은 없는 양을<br>
스칼라라고 정의한다. 하지만 벡터의 이해를 좀더 쉽게하기 위해 '수의 순서쌍'으로 설명할 수 있다.<br>
집합은 순서를 생각하지 않는다. A = {1, a, 3}와 B = {a, 3, 1}은 같은 집합으로 여겨진다.<br>
하지만 벡터는 순서쌍이기 때문에 순서가 매우 중요하다. 고로 벡터A = (1, a, 3)와 벡터B = (a, 3, 1)는<br>
서로다른 벡터로 여겨진다.<br>

벡터의 원소갯수에 따라서 2차원 3차원 ... n차원 벡터로 분류한다. (1차원벡터는 사실상 스칼라)<br>
위에서 설명한 A벡터 같은 경우 3차원 벡터이다.<br>

예시를 들어 설명해보자면, 과일가게에서 복숭아, 파인애플, 오렌지를 판다고 가정했을때<br>
매번 장부에 오늘의 판매량 : 복숭아 3개, 파인애플 4개, 오렌지 2개 라고 적는것은 불편할 것이다.<br>
고로 나름대로 순서를 정해 오늘의 판매량 : (3, 4, 2)라고 간단하게 적을 수 있을 것이다.<br>
여기서 중요한것은 '순서'이다. 이런식으로 첫번째 성분, 두번째 성분.. 각자 의미를 두고 순서를 정해서<br>
수를 나열한 순서쌍을 벡터라고 할 수 있다.<br>

**다른 해석**<br>
벡터는 화살표라 생각하면 좋다.<br>
화살표는 길이와 방향을 갖는데, 여기서 길이가 속도나 위치로 해석될 수 있다. <2차원 벡터를 예로 설명><br>
-> Unity에서 사용하는 Transform 역시 3차원 벡터의 개념이다.<br>
<br>

## 벡터의 연산<br>

> 같은 차원의 벡터끼리만 계산이 가능하다. !!
<br>

**벡터의 덧셈**<br>
단순히 각 요소들을 더해주면 된다.<br>
a벡터 + b벡터 = (a.x + b.x, a.y + b.y) <br>

평행사변형을 만들고 가로지르는것을 상상하면 쉽다.<br>
<img src="https://user-images.githubusercontent.com/43705434/108397932-d5d49000-725b-11eb-8b12-d3ff622bd147.png" width="500" height="300">
<br>

또 다른 관점에서 살펴보면 두 벡터의 합은 서로 다른 방향의 두 힘이 충돌했을 때의<br> 
그 합쳐진 힘의 진행 방향으로 해석될 수도 있다<br>
<img src="https://user-images.githubusercontent.com/43705434/108397935-d66d2680-725b-11eb-9298-0d7fdcef45ee.png" width="500" height="300">
<br>
<br>
<br>

**벡터의 뺄셈**<br>
a벡터 - b벡터 = (a.x - b.x, a.y - b.y)<br>
a벡터 + -b벡터<br>
<img src="https://user-images.githubusercontent.com/43705434/108397936-d705bd00-725b-11eb-9d11-c19fc881dd10.png" width="500" height="300">
<br>

**벡터 스칼라곱셈**<br>
a벡터 x 3 = (a.x * 3, a.y * 3)<br>

> 벡터간 나눗셈이란 개념은 없고 곱셈은 내적, 외적 2가지로 설명할 수 있다. (추후 설명)
<br>

**벡터의 길이**<br>
(x, y) 2차원 벡터를 화살표로 표현했을때 이 화살표의 길이는 피타고라스의 정리를 이용해서 구할 수 있다.<br>
이러한 벡터의 길이를 ||V|| 로 표현한다.<br>
Vector3 a;<br>
a.magnitude(); // 벡터의 길이를 반환<br>
<br>

**벡터의 단위화**<br>
Normalize(단위화)란 벡터의 길이를 1로 만들어서 순수히 방향만 나타내게끔 하는 것이다.<br>
V / ||V|| 의 과정을 통해서 진행된다. => (x / ||V||, y / ||V||) 길이가 1이 되는 단위벡터가 됨.<br>
Vector3 a;<br>
a.normalize(); // 단위벡터를 반환<br>


//타겟위치로 프레임마다 이동시키는 코드<br>

```c#
void Update()
{
	Move();
}

void Move()
{
	Vector3 dir = target.position - gameObejct.transform.position; //각 벡터를 원점에서 뻗어나오는 화살표라고 생각할때
	//-> (벡터의 뺄셈 그림 참조) target.position + -gameObejct.transform.position 로 설명할 수 있으므로
	//위와 같이 현재위치에서 타겟까지의 방향과 거리를 가진 벡터를 추출할 수 있다.
	dir.Normalzie(); //단위벡터로 만들어 방향만을 추출
	dir *= speed * Time.deltaTime; //speed * Time.deltaTime을 통해 1프레임 동안 이동할 거리를 결정
	gameObejct.transform.position += dir; //이동
}
```
<br>

### 벡터와 좌표<br>
벡터의 표현법과 좌표의 표현법이 같다는 것은 이미 눈치를 채고 있을 것이다. <br>
다시 말하면 (3, 1)은 2차원 벡터를 뜻하기도 하지만, 좌표평면위의 한 점 을 뜻한다. <br>
또한 (1, 4, 3)은 3차원 벡터를 뜻하기도 하지만, 공간좌표에서의 한 점 을 뜻하기도 한다. <br>
<br>
![3차원 좌표](https://user-images.githubusercontent.com/43705434/108397938-d705bd00-725b-11eb-9494-c212cef9b673.png)

> 해당 3차원 벡터를 통해 유니티에서 좌표계를 나타낼 수 있다.<br>
<br>

### 참조링크<br>
https://blog.daum.net/eigenvalue/10856412 <br>
https://wergia.tistory.com/161 <br>
https://wergia.tistory.com/209 <br>
