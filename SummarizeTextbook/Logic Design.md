# Logic Design

# Chapter 1 
## Logic Design의 목표
빠르고 정확하게 동작하는 디지털 시스템 만들기.

## CAD tool
왜 사용하나? synthesis...   
예전에 손으로 디자인하던 것을 대체함. 


## Simulation
- logic simulation
- timing simulation

## 예시: Read-Only Memories

# Chapter 2

- 문) pMOS, nMOS, cMOS  
답) pMOS는 1 전달, nMOS는 0 전달에 사용된다. cMOS는 둘을 합친 것. 
- 문) 왜 AND, OR 대신 NAND, NOR을 사용해서 구현할까?  
답) 필요한 트랜지스터의 개수가 AND, OR은 6개이고 NAND, NOR은 4개이다. AND, OR을 구현하려면 NAND, OR에 INVERTER를 붙여야 하는데 INVERTER에는 2개의 트랜지스터가 필요하다. 

- Boolean Cube
- Karnaugh Map
- 

# Chapter 3

## Simplification
- Q-M(퀸-맥클러스키) method
- Espresso

## Two Level implementation
- 장점: 
- S-o-P(Sum of Products)
    - ABC + A'B'C 꼴
- P-o-S(Product of Sums)
    - (A+B+C)(A'+B'+C) 꼴

## Multilevel Logic Networks
1. original AND-OR Network is given
2. Bubbles
3. redraw it as NAND / NOR Network

## Time Response in Combinational Networks
Gate delay, Timing Waveforms, Analysis of a Pulse-Shaper Circuit, Hazards and Glitch
- Hazard와 Glitch: Glitch는 원하지 않는 펄스, 이런 문제상황들을 통틀어 hazard라고 하는 듯.
- Hazard 없애기가 목표.
- 가정: 한번에 하나의 비트만 바뀌는 경우는 hazard 없애기 시도할 수 있다. (동시다발적으로 여러 비트가 바뀌어서 생기는 hazard는 피할 수 없다.) 
- Static hazard: 값이 바뀌지 말아야 하는데 펄스가 튀어서 잠깐 바뀌는 것. static 1-hazard와 static 0-hazard는 각각 정상적인 출력이 1, 0인데 거기서 펄스가 튀는 경우이다. 
- Dynamic hazard: 값이 바뀌는 건 맞는데 한번 이상 톡 튀었다 바뀌는 것. Dynamic hazard는 없애기 어렵다. 이 경우는 회로를 static hazard-free two-level circuit으로 바꾸는 게 좋다.
- redundant한 prime implicant를 추가해서 hazard를 없애야 한다.  
예시) 
$$
F(A, B, C, D) = \Sigma m(1,3,5,7,8,9,12,13)
$$


# Chapter 4 Combinational Logic Technologies

## Random Logic

## Regular Logic

## Mux(Multiplexer)

## DeMux(Demultiplexer)
