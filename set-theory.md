**Definition** _집합_ 은 집합에 대한 다음 공리들을 만족시키는 대상의 모임이다.  
A _set_ is a collection of objects satisfying a certain set of axioms.  

$`
\begin{aligned}
&set :: collection<object> := by \\
&\qquad axioms...
\end{aligned}
`$

---

집합에 있는 각 대상은 집합의 _원소_ 라고 불린다.  
Each object in the set is called an _element_ of the set.  

$`
\begin{aligned}
&element :: x, x \in A
\end{aligned}
`$

---

_멤버쉽 속성_ 은 가장 기본적인 집합론적 속성이다.  
우린 이걸 $`\in`$으로 표시합니다.  
The _membership property_ is the most basic set-theoritic property.  
We denote it by $`\in`$, thus we read $`X \in Y`$ as "$`X`$ is an element of $`Y`$", "$`X`$ is a member of $`Y`$" or "$`X`$ belongs to $`Y`$".  

---

### 외연공리(Axiom of Existence)
$`\forall X \forall Y (\forall a (a \in X \iff a \in Y) \implies X = Y)`$  
두 집합의 모든 원소가 같다면 두 집합은 같다.  
다양한 집합들의 유일성을 보이고, 거기에 이름을 붙일 수 있음.  

### 존재 공리(axiom of existence) 또는 공집합 공리(axiom of empty set)
$`\exists X \forall a (\neg (a \in X))`$
공집합이 존재한다.  
무한 공리와 분류 공리꼴로부터 유도될 수 있음  

### 분류 공리꼴 (axiom schema of specification 또는 axiom schema of separation)
Let $`P(x)`$ be a property of $`x`$,  
$`\forall X \exists Y \forall a (a \in Y \iff (a \in X \land P(a)))`$  
$`P(a)`$는 $`x > 0`$, $`x \in B`$ 등이 될 수 있으며, 주어진 집합에서 $`\{x \in Z | x > 0\}`$ 등의 부분집합을 만들 수 있다는 것이다.  
서로 다른 성질 $`P(x)`$마다 공리가 다르다고 봐야 하기 때문에 '공리꼴'이라고 함.  
(ZFC는 1차 논리로 기술되기 때문에 2차 논리와 달리 술어 $`P`$에 양화사를 적용할 수 없다.)  

### 짝 공리 (axiom of pairing)
$`\forall a \forall b \exists X (a \in X \land b \in X)`$  
집합 $`A`$, $`B`$가 있으면 그 둘을 원소로 갖는 집합 $`\{A, B\}`$ 등이 존재한다. ($`\{A, B, C, D, ...\} 같은 집합도 상관 없음`$)  
다른 공리로 유도될 수 있음.  

### 합집합 공리 (axiom of the union)
$`\forall X \exists U \forall a (\exists b (b \in X \land a \in b) \implies a \in U)`$  
합집합이 존재한다.  

### 멱집합 공리 (axiom of power set)
$`\forall X \exists P \forall Y (\forall a (a \in Y \implies a \in X) \implies Y \in P)`$  
임의의 집합 $`X`$에 대해, $`X`$의 부분집합들을 다 모아놓은 집합인 멱집합이 존재한다.  

### 무한 공리 (axiom of infinity)
$`\forall`$ 집합 $`x`$, Let $`S(x) = x \cup \{x\}`$  
$`\exists I (\emptyset \in I \land (\forall x (x \in I \implies S(x) \in I)))`$  
공집합을 원소로 가지고, $`x`$를 원소로 가진다면 $`S(x)`$도 항상 원소로 가지는, 집합 $`I`$가 존재한다.  
자연수 집합의 존재성을 보장. 자연수 집합 $`N`$은 이러한 성질을 만족하는 집합(귀납적 집합; inductive set)들 중 가장 크기가 작은 집합으로 정의된다.  
수학적 귀납법의 타당성도 이러한 자연수 집합의 정의로부터 바로 유도된다.  
