#include <iostream>
#include <string>
#include <sstream>
#include <cmath>
#include <stack>

using namespace std;

// Функция для проверки, является ли символ оператором
bool isOperator(char c) {
    return c == '+' || c == '-' || c == '*' || c == '/' || c == '^';
}

// Функция для вычисления приоритета операторов
int getPriority(char op) {
    if (op == '^') {
        return 3;
    } else if (op == '*' || op == '/') {
        return 2;
    } else if (op == '+' || op == '-') {
        return 1;
    } else {
        return 0;
    }
}

// Функция для преобразования инфиксного выражения в постфиксное
string infixToPostfix(const string& infix) {
    string postfix;
    stack<char> operatorStack;

    for (char c : infix) {
        if (isdigit(c)) {
            postfix += c;
        } else if (c == '(') {
            operatorStack.push(c);
        } else if (c == ')') {
            while (!operatorStack.empty() && operatorStack.top() != '(') {
                postfix += operatorStack.top();
                operatorStack.pop();
            }
            if (!operatorStack.empty()) {
                operatorStack.pop(); // Удаляем '('
            }
        } else if (isOperator(c)) {
            while (!operatorStack.empty() && getPriority(c) <= getPriority(operatorStack.top())) {
                postfix += operatorStack.top();
                operatorStack.pop();
            }
            operatorStack.push(c);
        }
    }

    while (!operatorStack.empty()) {
        postfix += operatorStack.top();
        operatorStack.pop();
    }

    return postfix;
}

// Функция для вычисления постфиксного выражения
double evaluatePostfix(const string& postfix) {
    stack<double> operandStack;

    for (char c : postfix) {
        if (isdigit(c)) {
            operandStack.push(c - '0');
        } else if (isOperator(c)) {
            double operand2 = operandStack.top();
            operandStack.pop();
            double operand1 = operandStack.top();
            operandStack.pop();

            switch (c) {
                case '+':
                    operandStack.push(operand1 + operand2);
                    break;
                case '-':
                    operandStack.push(operand1 - operand2);
                    break;
                case '*':
                    operandStack.push(operand1 * operand2);
                    break;
                case '/':
                    operandStack.push(operand1 / operand2);
                    break;
                case '^':
                    operandStack.push(pow(operand1, operand2));
                    break;
            }
        }
    }

    return operandStack.top();
}

int main() {
    string expression;

    cout << "Введите математическое выражение: ";
    getline(cin, expression);

    string postfix = infixToPostfix(expression);
    double result = evaluatePostfix(postfix);

    cout << "Результат: " << result << endl;

    return 0;
}
