**dkstpwls/dkstpwls** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.
class Calculator:
    """
    계산기 클래스

    메서드:
        __init__(): 생성자 메서드.
        is_operator(token): 주어진 토큰이 산술 연산자인지 확인합니다.
        precedence(operator): 주어진 연산자의 우선순위를 반환합니다.
        infix_to_postfix(infix_expression): 중위 표현식을 후위 표기법으로 변환합니다.
        evaluate_postfix(postfix_expression): 후위 표현식을 평가합니다.
        calculate(expression): 산술 표현식을 파싱하고 결과를 계산합니다.
    """

    def __init__(self):
        """Calculator 클래스의 인스턴스를 초기화."""
        pass

    def is_operator(self, token):
        """
        주어진 토큰이 산술 연산자인지 확인

        매개변수:
            token (str): 확인할 토큰

        반환값:
            bool: 토큰이 연산자이면 True, 그렇지 않으면 False
        """
        return token in {'+', '-', '*', '/'}

    def precedence(self, operator):
        """
        주어진 연산자의 우선순위를 반환

        매개변수:
            operator (str): 우선순위를 확인할 연산자

        반환값:
            int: 우선순위 값
        """
        if operator in {'+', '-'}:
            return 1
        elif operator in {'*', '/'}:
            return 2
        else:
            return 0

    def infix_to_postfix(self, infix_expression):
        """
        중위 표현식을 후위 표기법으로 변환

        매개변수:
            infix_expression (list): 중위 표현식의 토큰을 포함하는 리스트

        반환값:
            list: 후위 표현식의 토큰을 포함하는 리스트
        """
        postfix_expression = []
        operator_stack = []
        paren_stack = []

        for token in infix_expression:
            if token.isdigit() or (token[0] == '-' and token[1:].isdigit()):
                postfix_expression.append(float(token))
            elif token == '(':
                operator_stack.append(token)
                paren_stack.append(token)
            elif token == ')':
                while operator_stack and operator_stack[-1] != '(':
                    postfix_expression.append(operator_stack.pop())
                operator_stack.pop()
                if paren_stack:
                    paren_stack.pop()
                else:
                    raise ValueError("괄호 불일치 오류")
            elif self.is_operator(token):
                while operator_stack and self.precedence(operator_stack[-1]) >= self.precedence(token):
                    postfix_expression.append(operator_stack.pop())
                operator_stack.append(token)

        while operator_stack:
            postfix_expression.append(operator_stack.pop())

        if paren_stack:
            raise ValueError("괄호 불일치 오류")

        return postfix_expression

    def evaluate_postfix(self, postfix_expression):
        """
        후위 표현식을 평가

        매개변수:
            postfix_expression (list): 후위 표현식의 토큰을 포함하는 리스트

        반환값:
            float: 산술 표현식의 결과
        """
        operand_stack = []

        for token in postfix_expression:
            if isinstance(token, float):
                operand_stack.append(token)
            elif self.is_operator(token):
                if len(operand_stack) < 2:
                    raise ValueError("연산자 {}에 대한 피연산자가 충분하지 않습니다".format(token))
                else:
                    b = operand_stack.pop()
                    a = operand_stack.pop()
                    if token == '+':
                        result = a + b
                    elif token == '-':
                        result = a - b
                    elif token == '*':
                        result = a * b
                    elif token == '/':
                        if b == 0:
                            raise ValueError("0으로 나눌 수 없습니다")
                        result = a / b
                    operand_stack.append(result)

        if len(operand_stack) == 1:
            return operand_stack[0]
        else:
            raise ValueError("잘못된 표현식입니다")

    def calculate(self, expression):
        """
        산술 표현식을 파싱하고 결과를 계산

        매개변수:
            expression (str): 평가할 산술 표현식

        반환값:
            float: 산술 표현식의 결과

        예외:
            ValueError: 표현식에 오류가 있는 경우 발생
        """
        try:
            infix_expression = expression.split()
            postfix_expression = self.infix_to_postfix(infix_expression)
            result = self.evaluate_postfix(postfix_expression)
            return result
        except ValueError as e:
            raise ValueError("표현식 오류: {}".format(e))

# 사용 예시
calculator = Calculator()
expression = input("계산할 식을 입력하세요. (예: 3 + 4 * ( 2 - 1 ) ) : ")
try:
    result = calculator.calculate(expression) # 예외처리 부분
    print("계산 결과:", result)
except ValueError as e:
    print("오류 발생:", e)
