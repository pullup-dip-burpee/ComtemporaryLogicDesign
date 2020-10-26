# Chapter 3

## Simplification
- Q-M(퀸-맥클러스키) method
- Espresso

## Two Level implementation
- 장점: 
- SoP(Sum of Products)
    - ABC + A'B'C 꼴
- PoS(Product of Sums)
    - (A+B+C)(A'+B'+C) 꼴

------

## Two-level Simplification
용어
- implicant: sub-cube를 만들 수 있는 것. 1, don't care끼리 묶으면 됨. don't끼리만 묶는 것은 가능은 하지만 의미가 없다.  
- prime implicant: 더 이상 크게 묶을 수 없는 implicant
- essential prime implicant: 중복되는 게 없어서 반드시 들어가야 하는 prime implicant


목표  
1. implicant를 다 키워서 prime으로 만든다.
2. ON-set을 최소한의 prime 으로 덮는다. 

과정(알고리즘) - Karnaugh map 에서 minimum sum-of-product 표현 찾기
1. ON-set의 원소를 하나 고른 후 maximal grouping을 찾는다. -> prime 들을 찾게 된다. 
1. prime들 중 essential을 먼저 찾아서 포함시킨다.
2. 그 뒤 남은 것들 중 가장 큰 prime 들을 포함시킨다. 모든 ON-set들을 최소한의 prime으로 덮게 된다. 

## Two-level using NAND
OR -> NAND 변환

## Two-level using NOR
AND -> NOR 변환

------

## Multi-level Logic Network
2-level은 wire, fan-in 등이 지나치게 많아지는 문제가 있다.   
예시)
$$ x = ADF + AEF + BDF + BEF + CDF + CEF + G $$
이미 simplified 됨. 

### AND, OR을 NAND, NOR로 바꿔서 그리기
1. original AND-OR Network is given
2. Bubbles
3. redraw it as NAND / NOR Network

### Two-level과 Multi-level의 장단점?
1. gate 수는 multi-level 유리
1. fan-in은 multi-level 유리
1. wire는 multi-level 유리
1. propagation level은 two-level 유리
1. 속도는 fan-in 덕분에 multi-level이 유리할 수는 있지만 항상 그렇진 않다. propagation level로 인한 손해도 있기 때문.
------ 
더 좋은 building block?

## AOI(AND-OR-Invert) gates
AOI를 NAND, NOR로 구현하지 않고 트랜지스터 단계에서 구현하면 훨씬 더 효율적으로 할 가능성이 있다.  
예시)
트랜지스터 8개만으로 구현한 AOI

예시) $F = AB + AC' + BC'$

Xilinx에서 배포한 프로그램에 여러 라이브러리가 포함되어 있는데, AOI도 포함된다. 

### Conversion to AOI forms
A xor B: $F= A \oplus B = A'B + AB'$  
AOI form:
$F = (A'B' + AB)'$



## Time Response in Combinational Networks
Gate delay, Timing Waveforms, Analysis of a Pulse-Shaper Circuit, Hazards and Glitch
- Hazard와 Glitch: Glitch는 원하지 않는 펄스, 이런 문제상황들을 통틀어 hazard라고 하는 듯.
- Hazard 없애기가 목표.
- 가정: 한번에 하나의 비트만 바뀌는 경우는 hazard 없애기 시도할 수 있다. (동시다발적으로 여러 비트가 바뀌어서 생기는 hazard는 피할 수 없다.) 
- Static hazard: 값이 바뀌지 말아야 하는데 펄스가 튀어서 잠깐 바뀌는 것. static 1-hazard와 static 0-hazard는 각각 정상적인 출력이 1, 0인데 거기서 펄스가 튀는 경우이다. 
- Dynamic hazard: 값이 바뀌는 건 맞는데 한번 이상 톡 튀었다 바뀌는 것. Dynamic hazard는 없애기 어렵다. 이 경우는 회로를 static hazard-free two-level circuit으로 바꾸는 게 좋다.
- redundant한 prime implicant를 추가해서 hazard를 없애야 한다.  
예시) 
$F(A, B, C, D) = \Sigma m(1,3,5,7,8,9,12,13)$


## 번외: Verilog 문법

- always @ (a or b) begin ... end  
a 혹은 b의 값이 변할 때마다 ...을 실행한다. 이 때 ... 안의 lvalue는 항상 register여야 하고, wire는 안 된다. 

- assign #6 c = a ^ b  
6만큼(설정에 따라 다를 수 있지만 기본설정이면 6 ns) delay를 주면서 c = a xor b 를 할당한다. 즉, a 혹은 b의 값이 바뀌면 6 ns 뒤에 c의 값이 업데이트된다. assign문에서 좌변은 wire가 들어간다.   
procedure 문은 반드시 always문 안에 들어가야 한다. 
    ```verilog
    always @ (x1,x2,s)
        if(s==0) f=x1;
        else f=x2;
    ```

    ```verilog
    always @(x1 or x2 or s or k)
        begin
            if (s==0) f=x1;
            else f=x2;

            if(k==0) g=x2;
            else g=x1;
        end
    ```
- case
C의 switch-case 문과 비슷함. 

- casex
input에 don't care가 있는 경우 사용함.
    ```verilog
    module prime(in, isprime);
        input[3:0] in;
        output isprime;
        reg isprime;
        always @(*) begin
            casex(in)
                4'b0xx1: isprime = 1;
        end
    endmodule
    ```

## Adder 만들기
### Ripple Adder
느리다. 
### Carry-Select Adder
다음과 같이 만든다. 