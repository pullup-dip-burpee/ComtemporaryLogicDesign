# Chapter 2

## Transistors
- 문) pMOS, nMOS, cMOS 용도와 차이는? 
- 답) pMOS는 1 전달, nMOS는 0 전달에 사용된다. cMOS는 둘을 합친 것. 
- 문) 왜 AND, OR 대신 NAND, NOR을 사용해서 구현할까?  
- 답) 필요한 트랜지스터의 개수가 AND, OR은 6개이고 NAND, NOR은 4개이다. AND, OR을 구현하려면 NAND, OR에 INVERTER를 붙여야 하는데 INVERTER에는 2개의 트랜지스터가 필요하다. 


## Boolean Logic
예시
|A|B|C||F|
|---|---|---|---|---|
|0|0|0||0|
|0|0|1||0|
|0|1|0||0|
|0|1|1||1|
|1|0|0||0|
|1|0|1||1|
|1|1|0||1|
|1|1|1||1|


- canonical form
    - minterm과 Maxterm 
    - SoP(Sum-of-Products)  
    예시: $F = ABC + A'BC + AB'C + ABC'$
    - PoS(Product-of-Sums)  
    예시: $F = (A'+B'+C')(A+B'+C')(A'+B+C')(A'+B'+C)$
- (minimized) two level form  
canonical form을 최대한 간단하게 만든다. 
- multilevel form

## Simplification(Minimal Solution 찾기)
------
Minimal solution을 자동으로 찾는 알고리즘이 없다. 다만 휴리스틱은 있다. 수업에선 주로 손으로 찾는 알고리즘을 다룬다. 

### uniting theorem
$A(B' + B) = A$을 의미. Simplification 에서 몹시 중요하다.  
예시) $F = A'B' + AB' = (A'+A)B' = B'$

### Boolean Cube와 Karnaugh Map
진리표 상에서 한 bit만 다른 경우 이어준다. 이 경우를 인접(adjacent)한다고 하고, 인접한 것들은 하나의 묶음으로 합칠 수 있다. 다만 한 묶음에 들어있는 노드의 개수가 $2^n$개가 되어야 한다. 2개 1개 합쳐서 3개 이런 식은 안 되고, 2개씩 2쌍이 인접해서 하나의 4개 묶음으로 묶는다는 건 가능하다. $2^n$ 짜리 묶음을 가장 크게 만드는 게 목표.


Boolean Cube를 2차원 상으로 납작하게 그린 것을 Karnaugh Map이라고 한다. 
- ON-set, OFF-set, DC-set


목표: 어떻게 하면 가장 크게 묶으면서 묶음의 개수를 줄일까? 
