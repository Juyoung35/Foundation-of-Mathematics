# Formal System

형식 체계(formal system) :: 추론 규칙(rules of inference) 집합을 사용해 공리로부터 정리를 연역하는 데 사용되는 공리계의 추상 구조(abstract structure)이자 형식화(formalization)된 시스템이다.  

* abstract structure : 대상, 연산, 관계의 틀을 정의함. 근본적인 수학 원리들을 들어냄.
추상 구조는 특정 표현과 관계없이 추상적인 개념으로서 존재한다.
실제 대상이나 컴퓨터 프로그램은 추상 구조를 represent, instantiate, or implement할 것이다.

## Formal Language

형식 언어(formal language) :: 알파벳(alphabet)에서 추출한 기호(symbols) 문자열로 구성된 정형식(well-formed formulas)의 집합이며,  
형식 문법(formal grammer: 생산 규칙(production rules) 또는 형성 규칙(formation rules)로 구성됨)으로 형성된다.

### 형식 언어의 두 가지 양상 (자연어와 비슷하게)

- 구문(syntax)은 언어의 모습이다. (더 형식적으로는 언어에서 유요한 발화(valid utterances)인 가능한 표현(expression)의 집합이다)
- 의미론(semantics)은 언어의 발화가 의미하는 바를 말한다. (질문의 언어 유형에 따라 다양한 방식으로 형식화됨)

### 형식 언어의 구문 - 형식 문법
형식 언어의 구문은 주로 형식 문법(formal grammar)의 개념을 통해 고려된다.  
형식 문법의 큰 두 범주는  
- 생성 문법(generative grammars: 언어의 문자열을 작성히는 방법에 대한 규칙 집합)
- 분석 문법(환원 문법; analytic grammar; reductive grammar: 문자열을 분석하여 해당 언어의 멤버인지 여부를 판별(determine)하는 방법에 대한 규칙 집합)

## Deductive System

연역 체계(?deductive system), 연역 장치(?deductive apparatus), 또는 증명 체계(?proof system; proof calculus) :: 공리를 취해 정리를 추론하는 추론 규칙. 둘 다? 형식 언어의 일부이다.  

형식 체계는, 공리의 집합과 추론 규칙의 집합이 각각 결정 가능 집합 또는 반결정 가능 집합인 경우, 재귀적(recursive)으로 열거 가능(enumerable)하다고 한다.  

theorems < well-formed formulas == formal language < symbols and strings of symbols  

* 이 말은 형식 언어 중에서도 non-theorems이 있다는 거.

형식 언어는 유한 개의 기호 문자열(단어; 정형식)의 집합으로 구성된 구문적 실체(syntactic entity)이다.  



## 형식 언어 중 유명한 녀석들

predicate calculus
propositional calculus
lambda calculus
