## 2.1 Basics

### 2.1.1 Types, Terms and Formulas

- base types: `bool`, `nat`, `int`
- type constructors: `list`, `set`. // ex) `nat list`. 타입 컨스트럭터 postfix에 적힘.
- function types: `⇒`
- type variables: `` `a ``, `` `b `` // like ML
// postfix priority > `⇒`
`t :: τ` 타입표기, `t`는 `τ`의 항(term)이다.
// infix symbols `(+)`, `(*)`, syntactic sugar. `x + y` == `(+) x y`

#### basic constructs from fp
- `(if b then t1 else t2)`
- `(let x = t in u)`
- `(case t of pat1 ⇒ t1 | ... | patn ⇒ tn)`
// 다른 constructs 안에 있을 시 괄호 필수

####  λ-abstractions
`λx. x` // 항등함수
- formulas: bool 타입의 항이다. `True`, `False` 상수와 `¬`, `∧`, `∨`, `-→` 논리연결사 있음.
- equality: 이 또한 infix function이고 `` `a ⇒ `a ⇒ bool ``임. formulas와도 작동함 (iff로써)
- quantifiers: `∀x. P` and `∃x. P`

#### type constraint
`t :: τ` as in `m + (n::nat)`

#### universal quantifier ` Ʌ` and the implication `=⇒`
논리적으로는 각각 HOL의 ∀, −→의 counterparts임.  
그러나 isabelle에서는 다르게 동작함.  

// `A1 =⇒ A2 =⇒ A3` == `A1 =⇒ (A2 =⇒ A3)`  
// `[[ A1; . . .; An ]] =⇒ A` == `A1 =⇒ . . . =⇒ An =⇒ A`  
inference rule 표기법은 $`\frac{A1 ... An}{A}`$

### 2.1.2 Theories
프로그래밍 언어에서의 모듈과 비슷함.
```
theory T
imports T1 . . . T n
begin
definitions, theorems and proofs
end
```

### 2.1.3 quotation marks
`begin`, `datatype`과 같은 키워드와의 구분을 위해서 HOL 관련 항과 타입들은 `"..."` 쌍따옴표 안에 들어가야 함.

## 2.2 types `bool`, `nat` and `list`

### 2.2.1 type `bool`
```
datatype bool = True | False
```

```
fun conj :: "bool ⇒ bool ⇒ bool" where
  "conj True True = True" |
  "conj _ _ = False"
```

### 2.2.2 type `nat`

```
datatype nat = 0 | Suc nat
```

proof of `add m 0 = m`

```
lemma add_02: "add m 0 = m"
  apply (induction m)
  apply (auto)
done
```

`induction` 취하면서 두 개의 subgoal이 생성됨:  
1. `add 0 0 = 0`
2. `Ʌm. add m 0 = m =⇒ add (Suc m) 0 = Suc m`

// "add m 0 = m"은 IH(induction hypothesis) 가설로 사용 가능.?

`Ʌm`은 "for an arbitrary but fixed m"  

`thm add_02`는 `add ?m 0 = ?m`을 보여준다. 여기서 자유변수 `m`이 unknown `?m`으로 대체되었다.  
unknown 변수는 instantiated될 수 있다.  

// 용어 - 증명된 명제에 대해 `lemma`, `theorem`, `rule`를 교환 가능하게 쓸 수 있음.  

// `Suc x = x`에서는 `x`가 `nat`인걸 자동적으로 추론하지만 `x + 0 = x`에서는 못한다.  
그러니 `x + 0 = (x::nat)`으로 type constraint를 걸어주자.  

### 2.2.3 type `list`

```
datatype `a list = Nil | Cons `a "`a list"
```

// `` `a ``로 인한 다형성
// `Nil`과 `Cons`라는 두 개의 컨스트럭터

```
fun app :: "`a list ⇒ `a list ⇒ `a list" where
  "app Nil ys = ys" |
  "app (Cons x xs) ys = Cons x (app xs ys)"
```

```
fun rev :: "`a list ⇒ `a list" where
  "rev Nil = Nil" |
  "rev (Cons x xs) = app (rev xs) (Cons x Nil)"
```

// 꿀팁 - `value` 커맨드를 통해 항을 평가할 수 있음.  

Lists를 위한 structural induction: 속성 P가 리스트 요소들 모두에게 적용되는지 증명하려면 'base case P Nil'을 증명후, 'inductive case P (Cons x xs)`를 증명하면 된다.  

### 2.2.4 증명 과정

```
theorem rev_rev [simp]: "rev(rev xs) = xs"
```

대괄호 안에 `simp`를 넣으면서 simplification rule 적용시킬 때 얘도 적용되나봄.

```
apply (induction xs)
// 1. rev (rev Nil) = Nil
apply(auto) // subgoal 1 is proved.
// 2. Ʌx1 xs. rev (rev xs) = xs =⇒ rev (rev (Cons x1 xs)) = Cons x1 xs
  lemma rev_app [simp]: "rev (app xs ys) = app (rev ys) (rev xs)"
    apply (induction xs)
    // rev_app-1. rev (app Nil ys) = app (rev ys) (rev Nil)
    //          rev ys = app (rev ys) Nil
      lemma app_Nil2 [simp]: "app xs Nil = xs"
        apply (induction xs)
        apply (auto)
      done
    apply(app_Nil2)???
    // rev_app-2. Ʌx1 xs. rev (app xs ys) = app (rev ys) (rev xs) =⇒ app (app (rev ys) (rev xs)) (Cons x1 Nil) = app (rev ys) (app (rev xs) (Cons x1 Nil))
      lemma app_assoc [simp]: "app (app xs ys) zs = app xs (app ys zs)"
        apply (induction xs)
        apply (auto)
      done
    apply (app_assoc)???
  apply (rev_app)???
```

### 신텍스 슈가

- `[]` == `Nil`
- `x # xs` == `Cons x xs`
- `[x1, ..., xn]` == `x1 # ... # xn # []`
- `xs @ ys` == `app xs ys`

```
fun map :: "(`a ⇒ `b) ⇒ `a list ⇒ `b list where
  "map f Nil = Nil" |
  "map f (Cons x xs) = Cons (f x) (map f xs)"
```

### 2.2.6 types `int` and `real`

세 강제 함수(coerce functions)  

```
int :: nat ⇒ int
real :: nat ⇒ real
real_of_int :: int ⇒ real
```

대충 컴파일러가 타입 강제시킨다는 얘기.

## 2.3 type and function definitions

```
type_synonym string = "char list"
```

```
// axiom of extensionality
extension: A = B <-> A ⊆ B & B ⊆ A
// axiom of existence

