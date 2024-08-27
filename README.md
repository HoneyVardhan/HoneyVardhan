#Tutorial 2, Slot 1 
#complex calculator 

def evaluate(expression):
    words = expression.split()

    operators = []
    values = []

    def apply_operator():
        operator = operators.pop()
        rvalue = values.pop()
        lvalue = values.pop()

        if operator == '+':
            values.append(lvalue + rvalue)
        elif operator == '-':
            values.append(lvalue - rvalue)
        elif operator == '*':
            values.append(lvalue * rvalue)
        elif operator == '/':
            values.append(lvalue / rvalue)

    i = 0
    while i < len(words):
        word = words[i]

        if word == 'plus':
            operators.append('+')
        elif word == 'minus':
            operators.append('-')
        elif word == 'times':
            operators.append('*')
        elif word == 'divided':
            operators.append('/')
        elif word.isdigit():  # Check for numbers
            values.append(int(word))
        elif word == '(':
            operators.append('(')
        elif word == ')':
            while operators and operators[-1] != '(':
                apply_operator()
            operators.pop()  # Remove the '('

        i += 1

    while operators:
        apply_operator()

    return values[0]

# Testing
expressions = [ 
    "5 plus ( 3 times 2 )",
    "6 minus ( 6 divided 3 )"
]

for expr in expressions:
    result = evaluate(expr)
    print("Expression:", expr)
    print("Result:", result)
