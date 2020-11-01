# Chapter 4 Combinational Logic Technologies

## Random Logic vs. Regular Logic
Random Logic은 기본 게이트 등의 low level building block들로 만든 회로다. 구현을 이해하기 어렵고, 작은 변화로 cost가 크게 바뀔 수 있고, 구현도 너무 어렵다는 단점이 있다.   
Regular Logic은 이미 만들어진 regular한 building block들을 잘 활용해서 만든다.   

------
## Encoder와 Decoder
암호화 / 비암호화? 디지털화 / 아날로그화? 이런 식으로 번역할 수도 있겠는데 아무튼 Encoder는 $2^n$개의 input을 $n$개의 output으로 변환하고, Decoder는 $n$ 개의 input을 $2^n$ 개의 output으로 변환한다.  


## Mux(Multiplexer)

$2^n$ 개의 data input 중 하나를 골라서 1개의 output에 내보내는 것으로, 2-to-1 Mux, 4-to-1 Mux, 8-to-1 Mux 등을 만들 수 있다. $2^n$ 개의 data input들이 있을 때, 이들 중 무엇을 내보낼지 결정하는 $n$개의 control input이 필요하다. multiplexer라고도 부르고 selector라고도 부른다. 
- input: n개의 control input과 $2^n$개의 data input
- output: data input 중 선택된 1개  

8:1 Mux를 만드는 방법은 
1) 그냥 만들기 
2) 4:1 Mux 2개와 2:1 Mux 하나를 사용해 만들기 
3) 2:1 Mux 4개와 4:1 Mux 하나를 사용해 만들기




### 예시: Mux로 Full Adder 만들기
Full Adder: input으로 A, B, Cin 받아서 output인 Cout과 Sum으로 표기. 아래 진리표와 같음. 
| A   | B   | Cin |   |Cout | Sum |
|:---:|:---:|:---:|---|:---:|:---:|
|  0  |  0  |  0  |   | 0 | 0 |
|  0  |  0  |  1  |   | 0 | 1 |
|  0  |  1  |  0  |   | 0 | 1 |
|  0  |  1  |  1  |   | 1 | 0 |
|  1  |  0  |  0  |   | 0 | 1 |
|  1  |  0  |  1  |   | 1 | 0 |
|  1  |  1  |  0  |   | 1 | 0 |
|  1  |  1  |  1  |   | 1 | 1 |

Mux를 사용해서 구현할 경우 TTL 패키지가 2개(Mux 패키지 하나, inverter 패키지 하나)만 있으면 된다는 장점. 그냥 게이트들로만 구현할 경우 패키지가 4, 5개는 필요하다. 

## 4.3 Two-Level and Multilevel Logic

### 예시: Mux로 7-segment display 만들기
- 
진리표:

### CLB application

------
## Demux(Demultiplexer) 
Mux의 반대이다. data input은 1개이고, output은 $2^n$ 개이다. control input은 $n$개가 필요하다. 1-to-2 Demux, 2-to-4 Demux, 3-to-8 Demux 등이 있다. Decoder라고도 한다. 
- input: 1개의 data input, $n$개의 control input
- output: $2^n$개의 output. 이 중 하나를 사용.  

Decorder는 minterm generator로 사용된다. 가령 data input에 "1", control input S2, S1, S0에 각각 A, B, C를 둔다면 output 값인 0-7은 A'B'C'(m0)부터 ABC(m7)까지의 minterm에 대응한다. 

------
## ROM, PAL, PLA

| AND | OR |  |
|---|:---:|---:|
| fixed | fixed | ROM |
| fixed | prog. | PROM|
| prog. | fixed | PAL |
| prog. | prog. | PLA |

## ROM
programmable하지 않다. 
## PLA(programmable logic array)
AND와 OR 둘 다 programmable하다. shared product term을 활용할 수 있다는 장점이 있다. 
## PAL(programmable array logic)
PLA와 이름이 헷갈리는데, Program And onLy로 외우면 쉽다. PLA와 비교해서는 shared product term을 활용할 수 없다는 단점이 있다. 하지만 programmable connection은 저항이 커서 신호 전달이 좀 더 느리고, PAL은 AND만 programmable하므로, PLA보다 속도가 빠르다. 

## 예시: BCD-TO-GRAY-CODE
그레이 코드(gray code)는 이진법 부호의 일종으로, 연속된 수가 1개의 비트만 다른 특징을 지닌다.
- input: A, B, C, D
- output: W, X, Y, Z

| A | B   | C   | D |   | W | X | Y | Z | 
|:---: |:---:|:---:|:---:|---|:---:|:---:|:---:|:---:|
| 0 |  0  |  0  |  0  |   | 0 | 0 | 0 | 0 |
| 0 |  0  |  0  |  1  |   | 0 | 1 |  |  |
| 0 |  0  |  1  |  0  |   | 0 | 1 |  |  |
| 0 |  0  |  1  |  1  |   | 1 | 0 |  |  |
| 0 |  1  |  0  |  0  |   | 0 | 1 |  |  |
| 0 |  1  |  0  |  1  |   | 1 | 0 |  |  |
| 0 |  1  |  1  |  0  |   | 1 | 0 |  |  |
| 0 |  1  |  1  |  1  |   | 1 | 1 |  |  |
| 1 |  0  |  0  |  0  |   | 0 | 0 |  |  |
| 1 |  0  |  0  |  1  |   | 0 | 1 |  |  |
| 1 |  0  |  1  |  0  |   | 0 | 1 |  |  |
| 1 |  0  |  1  |  1  |   | 1 | 0 |  |  |
| 1 |  1  |  0  |  0  |   | 0 | 1 |  |  |
| 1 |  1  |  0  |  1  |   | 1 | 0 |  |  |
| 1 |  1  |  1  |  0  |   | 1 | 0 |  |  |
| 1 |  1  |  1  |  1  |   | 1 | 1 |  |  |


## 4.4 Non-Gate Logic
### Tri-State Outputs
- 저항(impedence)이 무한대인 상태 High impedence -> Z로 나타냄.
- OE(Output Enable)라는 input을 사용함
- 하나 이상의 게이트가 같은 output wire에 연결될 수 있도록 함. 

### Tri-state gates로 경제적인 Mux 만들기
![TristateMux](./images/TristateGatesMux.png)

위 그림을 보면, SelectInput이 0일때는 input0이, SelectInput이 1일 때는 Input1이 F에 들어간다. 

### Open-collector Ouptuts and Wired Logic
- Open-Collector NAND gate
- 여러 개 게이트를 하나의 output wire에 연결할 수 있다. pullup resistor를 사용한다. 
- 아래 그림에서, A와 B가 전부 연결되어야 F가 GND 0 V에 연결되고 0의 값을 가진다. 둘 중 하나라도 열려 있다면 GND와 연결되지 않고 위의 +와 연결된다. 
![OpenCollectorNand](./images/OpenCollectorNand.png)

- 이를 통해서 wire 하나에 다 연결하는 wired-AND를 구현할 수 있다. 
