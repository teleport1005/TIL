## Stack
- 물건을 쌓아올리는 형식의 자료 구조
- 후입 선출 -> `Last iIn First Out`

```Java
public class MyStack {
    // 배열로 실제 데이터를 보관
    private final int[] arr = new int[16];
    private int top = -1;
```
```Java
    // 데이터 넣기
    // int x를 stack의 제일 위에 넣는다.
    public void push(int x){
        if (top == arr.length - 1){
            throw new RuntimeException("stack is full");
        }
        this.top++;
        arr[this.top] = x;
    }
```
```Java
    // 데이터 회수하기
    public int pop() {
        // 제일 위에 있는 데이터 할당
        int value = arr[this.top];
        // stack의 제일 윗칸을 줄인다.
        this.top--;
        return value;
    }
```
```Java
    // 비어있는지 확인하기
    public boolean inEmpty() {
        return this.top == -1;
    }
```

### 괄호 검사
- 

### 깊이 우선 탐색 (DFS)
- 