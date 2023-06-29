# **[CS50 2020 - Lecture 2 - Arrays](https://youtu.be/tI_tIZFyKBw?t=3825)**

```java
int scores[3];
```

- a chunk of memory
- 연속된 값으로 입력된다.

<br>

```java
int scores[3];
scores[0] = 72;
scores[1] = 73;
scores[2] = 33;
```

💡 일종의 프로그래밍 관례로 0부터 인덱스를 시작한다.

<br>
- 배열을 선언할 때 "[3]"과 같은 표현을 쓰는 데, 이는 총 값의 수를 나타낸다.
- 배열에 색인을 생성할 때, 해당 메모리 청크의 특정 위치로 이동하면 유사한 숫자를 사용한다.
    - ➡️ 상대적인 위치를 참조(첫 번째, 두 번째, 세 번째)
