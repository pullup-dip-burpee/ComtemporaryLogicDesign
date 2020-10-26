# Chapter 5 Case Studies in Combinational Logic Design

## 5.1 Design Procedure
1. Understand the Problem
    - 문제를 정확히 이해하고 구체화시킨다. Input과 output을 파악하고, Block diagram 등을 그린다. 
2. Formulate in a Standard Representation
    - truth table이나 waveform diagram 등을 그린다. 
3. Choose an Implementation
    - ROM, PAL, PLA, mux, decoder, basic gate 등으로 구현한다. 
4. Apply the Design Procedure

## 5.2 A Simple Process Line-Control Problem
컨베이어 벨트에 막대기들이 들어오는데, 센서 세 개를 사용해서 적정길이인지 파악해보자. 들어오는 막대기들은 적정길이 +- 10%, 통과기준은 +-5%. 
1. 문제 구체화: 이상적인 길이를 100이라고 가정하고, 95~105 길이는 통과, 이걸 넘어가면 불통과라고 하자. input은 센서 세 개인데, 각각 A, B, C라고 하자. A를 길이 0에(여기서 모든 막대기 시작 부분이 있다고 가정), B를 95에, C를 105에 맞춰 둔다. 그러면 ABC'면 통과다. Too short는 AB'C', Too long은 ABC이다. 

2. standard representation으로 formulate한다. 
3. 생략
4. 생략

## 5.3 Telephone Keypad Decoder
1 2 3 -> R1  
4 5 6 -> R2  
7 8 9 -> R3  
\* 0 # -> R4  

C1 C2 C3

위와 같은 4행 3열의 telephone keypad 있다고 하자. 할 일은 이 키패드의 버튼이 눌리면 그걸 decode하는 combinational circuit을 만드는 것이다. 각 버튼은 4-bit binary number로 decoded 되어야 한다. 10과 15는 *와 #에 대응한다. 


1. Ynderstand the problem.  
이 circuit은 뭘 하는가?  
    - 입력: Row, Column이 신호로 들어온가. R1~R4, C1~C3이라고 하자. 
    - 출력: 눌린 key의 값. 즉, 4bit binary number로 decode 된 값.
    - 기타: 동시에 두 개 이상의 버튼이 눌리는 경우는 무시하자. 
2. Formulate in a standard representation.  
Truth table을 쓴다면 $2^7 = 128$ 개의 row가 필요하다. 다른 방법을 쓰자. Hardware description language인 verilog.

```verilog
module keypaddecoder(R1, R2, R3, R4, C1, C2, C3, K8, K4, K2, K1, KP);
    input   R1, R2, R3, R4, C1, C2, C3;
    output  K8, K4, K2, K1, KP;
    reg[3:0] key;

    always @(R1, R2, R3, R4, C1, C2, C3) begin
        if (R1 & C1) key = 1;   // 0001
        if (R1 & C2) key = 2;   // 0010
        if (R1 & C3) key = 3;   // 0011
        if (R2 & C1) key = 4;   // 0100
        if (R2 & C2) key = 5;   // 0101
        if (R2 & C3) key = 6;   // 0110
        if (R3 & C1) key = 7;   // 0111
        if (R3 & C2) key = 8;   // 1000
        if (R3 & C3) key = 9;   // 1001
        if (R4 & C1) key = 10;  // 1010
        if (R4 & C2) key = 0;   // 0000
        if (R4 & C3) key = 15;  // 1111
        KP = ((R1 + R2 + R3 + R4) == 3b'001)
            && ((C1 + C2 + C3) == 3'b001);
    end
    
    assign K8 = key[3];
    assign K4 = key[2];
    assign K2 = key[1];
    assign K1 = key[0];

endmodule
```
여기서 KP는 한 번에 하나의 버튼만 눌러졌는가를 검사한다. 

3. Implementation target.

4. Implementation procedure.

## 5.4 Leap Year Calculation
윤년임을 파악할 수 있도록. 4로 나누어떨어지는지와 100으로 나누어떨어지는지, 400으로 나누어떨어지는지 세 가지 경우 생각하면 돤다.  
인코딩이 중요하다. BCD인지 바이너리인지. 

- divided by 4
- divided by 100
- divided by 400

## 5.5 Logic Function Unit
- 1, 0, and, or, nand, nor, xor, nxor 8가지 연산

## Number System
### Two's complement
- one's complement에 비해 왜 +, - 연산이 더 빠른가?
    + one's complement는 carry가 발생할 경우 한 번의 추가적인 덧셈이 더 필요하다.
- one's complement에 비해 표현 범위가 왜 하나 더 많은가? 
    + 가령 4비트면 1111도 사용할 수 있다. 

----
## 5.6 Adder Design

## Ripple-carry adder
- critical delay

## Carry-lookahead Circuits
- time과 space의 tradeoff 중 space를 좀 더 써서 time을 줄인다. carry를 먼저 계산

## Carry-select Adder


## BCD Adder Design

- BCD 수 두 개를 더해서 BCD 결과가 나오게 한다. 0~9를 표시하는 데에는 4bit이 필요하므로 operand A, B는 각각 4bit이다. 
- 가령 A = 4'b1000, B = 4'b1000이면 이 둘을 더한 A+B는 10000이 아니라 0001 0110으로 표시한다. 
![BCDAdder](./images/BCDadder.png)
- 위의 그림에서 A1, A2는 각각 11XX, 1X1X 패턴과 매칭하는지를, 그리고 A3과 B3의 FA(full adder)의 CO(Carry out)는 더한 결과가 16 이상인지를 감지하는데, 셋 중 하나라도 참이면 Carry가 발생한 것이므로 Cout으로 묶는다.
- 이걸 다시 2번째 열의 두 FA에 더해주는 이유는 보정을 위해서이다. 가령, A = 1001, B = 1001이라고 하면 둘을 더하면 18(5'b10010)이 되는데 여기서 10(4'b1010)을 빼주면 8(4'b1000)이 된다. 

예시) 9 + 9
|   |   |   |   |   |   |
|---|---|---|---|---|---|
|  A|   |  1|  0|  0|  1| 
| +B|   |  1|  0|  0|  1| 
|  =|  1|  0|  0|  1|  0|
|  -|   |  1|  0|  1|  0|
|  =|   |  1|  0|  0|  0|


## 5.7 Arithmetic Logic Unit Design

## 5.8 Combinational Multiplier

