**dkstpwls/dkstpwls** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

1. 계산기 클래스(‘Calculator’)를 다음 조건을 만족하도록 구현하라. (30점)
조건1. 스택(Stack)을 활용하여 기본적인 사칙연산을 하도록 구현하라. (5점)
조건2. 괄호 처리를 지원하며 괄호의 쌍의 수가 맞지 않으면 계산이 돌아가지 않도록 조건1에서 사용된 스택이 아닌 다른 스택을 사용하여 구현하라 (10점)
조건3. 예외 처리를 해야하는 부분이 있다면 예외 처리가 가능하도록 구현하라. (5점)
조건4. 클래스의 형식을 반드시 만족(생성자, 소멸자 등 구현) (10점)

2. 1에서 만든 기본 계산기 클래스를 상속하여 공학용 계산기 클래스(‘EngineerCalculator’)를 구현하라. (40점)
  조건1. math 모듈을 이용하여 삼각함수(sin, cos, tan) 계산이 가능해야 하며 공학용 계산에서 일반적으로 사용되는 상수를 사용할 수 있어야 한다. (5점)
  조건2. Numpy 모듈을 이용하여 행렬계산이 가능하도록 구현하라. (15점)
조건3. 팩토리얼(n!)을 재귀 방식을 사용하여 함수로 구현하라. (5점)
조건4. matplotlib을 이용하여 그래프를 작성할 수 있도록 구현하라. (15점)

위 조건을 만족하는 계산기 클래스 코드를 작성해보았다.

마지막 부분에 #으로 주석처리된 부분을 삭제하하고 영어로 입력된 코드를 실행하면 각 부분에 맞는 계산을 사용할 수 있다.

다만 여기서 조건 1.에 해당하는 상수를 pi,e 로 한정하여 사용하였는데 그 외 상수가 있는지는 자세히 모르겠다.

각 부분에 대한 주석은 python docstring으로 처리하였으니 확인하면 된다.

그리고 가끔 if 조건문 부분에서 python docstring을 사용했을 때 실행이 안되는 오류가 발생했던 부분이 있는데 해결 못한부분은 주석으로 달았다
