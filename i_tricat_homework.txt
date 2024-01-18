import math
import numpy as np
import matplotlib.pyplot as plt
"""파이썬 내장함수 사용"""

class Calculator:
    """
    Calculator 클래스는 기본적인 수학 연산 및 중위 표기법을 후위 표기법으로 변환하는 기능을 제공합니다.

    

    메소드:
        is_operator(token): 주어진 토큰이 연산자인지 확인합니다.
        precedence(operator): 연산자의 우선순위를 반환합니다.
        infix_to_postfix(infix_expression): 중위 표기법을 후위 표기법으로 변환합니다. 예시로 a + (b * c) / d
        evaluate_postfix(postfix_expression): 후위 표기법을 평가합니다. 예시로 a b c * +
        calculate(expression): 수학 표현식을 구문 분석하고 계산합니다.

    사용 예시:
        calculator = Calculator()
        result = calculator.calculate("3 + 4 * (2 - 1)")
        print(result)
    """
    def __init__(self):
        pass

    def is_operator(self, token):
        return token in {'+', '-', '*', '/'}
        """
        주어진 토큰이 연산자인지 확인합니다.

        매개변수:
            token (str): 확인할 토큰.

        반환값:
            bool: 토큰이 연산자이면 True, 그렇지 않으면 False.
        """

    def precedence(self, operator):
        if operator in {'+', '-'}:
            return 1
        elif operator in {'*', '/'}:
            return 2
        else:
            return 0
        """
        연산자의 우선순위를 반환합니다.

        매개변수:
            operator (str): 우선순위를 확인할 연산자.

        반환값:
            int: 연산자의 우선순위.
        """
    def infix_to_postfix(self, infix_expression):
        postfix_expression = []
        operator_stack = []
        paren_stack = []
        for token in infix_expression:
            if token.replace('.', '', 1).isdigit() or (token[0] == '-' and token[1:].replace('.', '', 1).isdigit()):
                postfix_expression.append(float(token))
            elif token in {'pi', 'e'}:
                postfix_expression.append(token)
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
                    raise ValueError("Mismatched parentheses")
            elif self.is_operator(token):
                while operator_stack and self.precedence(operator_stack[-1]) >= self.precedence(token):
                    postfix_expression.append(operator_stack.pop())
                operator_stack.append(token)

        while operator_stack:
            postfix_expression.append(operator_stack.pop())

        if paren_stack:
            raise ValueError("Mismatched parentheses")

        return postfix_expression

        """
        중위 표기법을 후위 표기법으로 변환합니다.

        매개변수:
            infix_expression (list): 변환할 중위 표기법의 토큰 리스트.

        반환값:
            list: 후위 표기법으로 변환된 토큰 리스트.
        """
    def evaluate_postfix(self, postfix_expression):
        operand_stack = []

        for token in postfix_expression:
            if isinstance(token, float) or token in {'pi', 'e'}:
                if token == 'pi':
                    operand_stack.append(math.pi)
                elif token == 'e':
                    operand_stack.append(math.e)
                else:
                    operand_stack.append(token)  
            elif self.is_operator(token):
                if len(operand_stack) < 2:
                    raise ValueError("Not enough operands for operator {}".format(token))
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
                            raise ValueError("Cannot divide by zero")
                        result = a / b
                    operand_stack.append(result)
    #위 부분은 사칙연산에 관한 코드이다
    
        if len(operand_stack) == 1:
            return operand_stack[0]
        else:
            raise ValueError("Invalid expression")

    def calculate(self, expression):
        try:
            infix_expression = expression.split()
            postfix_expression = self.infix_to_postfix(infix_expression)
            result = self.evaluate_postfix(postfix_expression)
            return result
        except ValueError as e:
            raise ValueError("Error in expression: {}".format(e))
        """
        수학 표현식을 구문 분석하고 계산합니다.

        매개변수:
            expression (str): 계산할 수학 표현식.

        반환값:
            float: 계산 결과.
        """

class EngineeringCalculator(Calculator):
    def __init__(self):
        super().__init__()

    def square_root(self, num):
        return math.sqrt(num)

    def sine(self, angle_degrees):
        return math.sin(math.radians(angle_degrees))

    def cosine(self, angle_degrees):
        return math.cos(math.radians(angle_degrees))

    def tangent(self, angle_degrees):
        return math.tan(math.radians(angle_degrees))

    def factorial(self, n):                                                   
    
        if n == 0 or n == 1:
            return 1
        else:
            return n * self.factorial(n - 1)

    def pi(self):
        return math.pi

    def euler_number(self):
        return math.e

    def matrix_multiply(self, matrix_a, matrix_b):
        return np.dot(matrix_a, matrix_b)
    """행렬에 대한 코드"""

    def plot_function(self, func, start, end, step=0.1):
        x_values = np.arange(start, end + step, step)
        y_values = [func(x) for x in x_values]

        plt.plot(x_values, y_values)
        plt.xlabel('x')
        plt.ylabel('y')
        plt.title('Graph of the Function')
        plt.grid(True)
        plt.show()
    """
    그래프를 만드는 코드
    """
engineer_calc = EngineeringCalculator()
"""
아래 계산식은 한글로 된 부분을 제외한
영어로 입력된 코드에 # 부분을 제거하고 코드를 실행해야한다
각 부분에 맞는 행렬, 그래프 등의 계산을 적어놓았다.
"""
#사칙연산 계산기
#calculator = Calculator()
#expression = input("계산할 식을 입력하세요. (예: 3 + 4 * ( 2 - 1 ) ) : ")
#try:
    #result = calculator.calculate(expression) # 예외처리 부분
    #print("계산 결과:", result)
#except ValueError as e:
    #print("오류 발생:", e)

#숫자 입력 받아 팩토리얼 계산
#number = int(input("팩토리얼을 계산할 숫자를 입력하세요: "))
#factorial_result = engineer_calc.factorial(number)
#print(f"{number}의 팩토리얼은 {factorial_result}입니다.")

#함수 그래프 그리기(각 항목은 값을 입력해야함)
#calculator_instance.plot_function(math.cos, 0, 2 * math.pi)

#행렬 생성 계산 예시
#matrix_a = np.array([[1, 2], [3, 4]])
#matrix_b = np.array([[5, 6], [7, 8]])
#result_matrix = np.dot(matrix_a, matrix_b)
#print("Matrix A:")
#print(matrix_a)
#print("Matrix B:")
#print(matrix_b)
#print("Result of Matrix Multiplication:")
#print(result_matrix)
