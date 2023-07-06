# Arrays

### Implement a vector (mutable array with automatic resizing)

- [x] Practice coding using arrays and pointers, and pointer math to jump to an index instead of using indexing.

- [x] New raw data array with allocated memory
  - can allocate int array under the hood, just not use its features
  - start with 16, or if starting number is greater, use power of 2 - 16, 32, 64, 128
- [x] size() - number of items
- [x] capacity() - number of items it can hold
- [x] is_empty()
- [x] at(index) - returns item at given index, blows up if index out of bounds
- [x] push(item)
- [x] insert(index, item) - inserts item at index, shifts that index's value and trailing elements to the right
- [x] prepend(item) - can use insert above at index 0
- [x] pop() - remove from end, return value
- [x] delete(index) - delete item at index, shifting all trailing elements left
- [x] remove(item) - looks for value and removes index holding it (even if in multiple places)
- [x] find(item) - looks for value and returns first index with that value, -1 if not found
- [x] resize(new_capacity) // private function

  - when you reach capacity, resize to double the size
  - when popping an item, if size is 1/4 of capacity, resize to half

- [x] Time
  - O(1) to add/remove at end (amortized for allocations for more space), index, or update
  - O(n) to insert/remove elsewhere
- [x] Space
  - contiguous in memory, so proximity helps performance
  - space needed = (array capacity, which is >= n) \* size of item, but even if 2n, still O(n)

<br>

<br>

---

## 🤔 설계 고려사항

- 자료형은 `int`로 한정한다.
- 맨 처음 생성자를 통해 초기화 벡터가 생성된다.

> New raw data array with allocated memory
>
> - can allocate int array under the hood, just not use its features
> - start with 16, or if starting number is greater, use power of 2 - 16, 32, 64, 128

- java의 `ArrayList` 를 사용하지 않고 정적 배열 형태로 동적 가변 배열을 구현한다.
- 기본 원소의 개수는 16부터 시작한다.
- 그 밖의 디테일한 구현 사항들은 문서화 주석으로 함수 정의문 위에 기록한다.
- :warning: 주의사항
  - 삽입 시, 배열 확장 고려
  - 삭제 시, 배열 축소 고려

<br>

<br>

```java
public class Arrays {
    private int[] vector;
    private int elemCnt = 0;

    public Arrays(){
        vector = new int[16];
    }

    public int size(){
        return elemCnt;
    }

    public int capacity(){
        return vector.length - size();
    }

    /**
     * @return 비어있으면 True(1), 요소가 있으면 False(0)
     */
    public boolean is_empty(){
        return elemCnt == 0;
    }

    /**
     * 입력 인덱스가 범위 밖이면 'IndexOutOfBoundsException' 에러 발생
     */
    public int at(int index){
        if (index >= 0 || index < size()){
                return vector[index];
        } else {
            throw new IndexOutOfBoundsException();
        }
    }

    public void push(int item){
        if (capacity() == 0){
            resize(size() * 2);
        }
        vector[elemCnt++] = item;
    }

    /**
     * 입력 인덱스가 범위 밖이면 'IndexOutOfBoundsException' 에러 발생
     */
    public void insert(int index, int item){
        if (index < size()){
            int[] newVector = new int[vector.length];

            if (capacity() == 0) {
                resize(size() * 2);
            }

            for (int i = 0; i < index; i++) {
                newVector[i] = vector[i];
            }
            newVector[index] = item;
            for (int i = index + 1; i < size() + 1; i++) {
                newVector[i] = vector[i - 1];
            }

            elemCnt++;
            vector = newVector;
        } else {
            throw new IndexOutOfBoundsException();
        }
    }

    public void prepend(int item){
        if (capacity() == 0){
            resize(size() * 2);
        }

        int[] newVector = new int[vector.length];

        for (int i = 0; i < size(); i++){
            newVector[i + 1] = vector[i];
        }
        newVector[0] = item;

        elemCnt++;
        vector = newVector;
    }

    /**
     * 벡터가 비었을 경우 'NullPointerException' 에러 발생
     */
    public int pop(){
        int rst;

        if (is_empty()){
            throw new NullPointerException();
        }

        rst = vector[elemCnt - 1];
        vector[elemCnt--] = 0;

        if (size() / 4 == vector.length){
            resize(size() / 4);
        }

        return rst;
    }

    /**
     * 입력 인덱스가 범위 밖이면 'IndexOutOfBoundsException' 에러 발생
     */
    public void delete(int index){
        if (index < size()){
            for (int i = index; i < size(); i++){
                vector[i] = vector[i + 1];
            }

            elemCnt--;

            if (size() / 4 == vector.length){
                resize(size() / 4);
            }
        } else {
            throw new IndexOutOfBoundsException();
        }
    }

    /**
     * item이 존재하는 모든 인덱스 위치의 원소 삭제
     */
    public void remove(int item){
        for (int i = 0; i < size(); i++) {
            if (vector[i] == item){
                delete(i);
            }
        }
    }

    /**
     * item이 벡터 내에 없으면 -1 리턴
     */
    public int find(int item){
        for (int i = 0; i < size(); i++) {
            return i;
        }
        return -1;
    }

    private void resize(int new_capacity){
        int[] newVector = new int[new_capacity];

        for (int i = 0; i < size(); i++) {
            newVector[i] = vector[i];
        }
        vector = newVector;
    }

    // test
    public static void main(String[] args) {
        Arrays tmpVector = new Arrays();
        System.out.println("test 1:" + tmpVector.size());
        System.out.println("test 2:" + tmpVector.capacity());
        System.out.println("test 3:" + tmpVector.is_empty());
        tmpVector.push(3);
        tmpVector.push(4);
        System.out.println("test 4:" + tmpVector.at(0)); // 3
        System.out.println("test 5:" + tmpVector.at(1)); // 4
        tmpVector.insert(0, 2);
        tmpVector.prepend(1);
        System.out.println("test 6:" + java.util.Arrays.toString(tmpVector.vector)); // [1, 2, 3, 4, ...]
        System.out.println("test 7:" + tmpVector.pop());
        tmpVector.delete(0);
        tmpVector.remove(2);
        System.out.println("test 8:" + tmpVector.find(3)); // 0
    }
}
```
