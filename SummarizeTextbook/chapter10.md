# Chapter 10: Case Studies in Sequential Logic Design

## Factoring

- Sequential Logic 잘 디자인하는 순서
    - sample input/output을 몇 개 쓰면서 문제 스펙을 잘 이해해본다.
    - states와 transition의 sequence를 쓴다. 
    - missing transition들을 채워넣는다.
    - I/O 동작까지 체크한다. 

### Finite String Pattern Recognizer
- 문제 스펙: 010 패턴이 들어오면 1을 출력하고 100이 들어오면 그때부터는 0만 출력한다. 단, Reset이 들어오면 초기화한다. 




그냥 만들면 state 7개~8개 필요, 복잡. 

Factoring 하면 state 3개로 처리할 수 있다. 

### Digital Combinational Lock
- 문제 스펙: 10진수 숫자 3자리를 비밀번호로 받아서 맞으면 UNLOCK, 틀리면 ERROR 출력. 

- 
### 과제 5 중에서
- 문제 스펙: 


### Static RAM
- SRAM은 빠르나 대용량 힘들다. DRAM은 장단점이 반대. 

- 1024 * 4 organization. SRAM Cell이 1024 * 4개 있다. Cell 하나당 transistor가 6개 필요하다. 

- Word Enable 하면 읽는다. 
