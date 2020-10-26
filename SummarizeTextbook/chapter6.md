# Chapter 6 Sequential Logic Design
Sequential Logic = Compinational Logic + Memory

- memory
- clocks
- flip-flops

## 6.1 Sequential Logic Elements

## Two inverters
가장 기본적인 메모리. 

## SR Latch
SR은 Set, Reset을 의미함. 항상 두 개의 입력(S, R)과 두 개의 출력(Q, Q')를 가짐. 두 개의 출력은 서로 상보관계. 단, S=1, R=1은 금지된 입력.   
- 특성표(characteristic table)  
    q 는 직전 상태
    | S | R |  Q  |  Q' |
    |---|---|:---:|:---:|
    | 0 | 0 |  q  |  q' |
    | 0 | 1 |  0  |  1  |
    | 1 | 0 |  1  |  0  |
    | 1 | 1 |  x  |  x  |

- 회로
![SRlatch_nor](.\images\SRlatch.png)

## RS Latch

## JK Latch
- RS Latch의 단점 보완

## Flip-Flop

## Data Flip-Flop

## 6.2 Timing Methodologies


## 6.3 Registers