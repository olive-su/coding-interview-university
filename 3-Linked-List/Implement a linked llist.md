# LinkedList

- Implement (I did with tail pointer & without):
  - [x] size() - returns number of data elements in list
  - [x] empty() - bool returns true if empty
  - [x] value_at(index) - returns the value of the nth item (starting at 0 for first)
  - [x] push_front(value) - adds an item to the front of the list
  - [x] pop_front() - remove front item and return its value
  - [x] push_back(value) - adds an item at the end
  - [x] pop_back() - removes end item and returns its value
  - [x] front() - get value of front item
  - [x] back() - get value of end item
  - [x] insert(index, value) - insert value at index, so current item at that index is pointed to by new item at index
  - [x] erase(index) - removes node at given index
  - [x] value_n_from_end(n) - returns the value of the node at nth position from the end of the list
  - [x] reverse() - reverses the list
  - [x] remove_value(value) - removes the first item in the list with this value
  - [ ] Doubly-linked List
    - [Description (video)](https://www.coursera.org/lecture/data-structures/doubly-linked-lists-jpGKD)
    - No need to implement

<br>

<br>

---

## 🤔 설계 고려사항

- 자료형은 `int`로 한정한다.
- 맨 처음 생성자를 통해 초기화 링크드 리스트가 생성된다.

<br>

<br>

```java
import java.util.*;

public class ImplLinkedList {
    private LinkedList<Integer> LinkedList;

    public ImplLinkedList() {
        LinkedList = new LinkedList<>();
    }

    public int size() {
        return LinkedList.size();
    }

    public boolean empty() {
        return LinkedList.size() == 0;
    }

    /**
     * 입력 인덱스가 범위 밖이면 'IndexOutOfBoundsException' 에러 발생
     */
    public int value_at(int index) {
        if (index >= 0 || index < size()){
            return LinkedList.get(index);
        } else {
            throw new IndexOutOfBoundsException();
        }
    }

    public void push_front(int value) {
        LinkedList<Integer> newLinkedList = new LinkedList<>();
        newLinkedList.push(value);

        for (int e : LinkedList)
            newLinkedList.push(e);

        LinkedList = newLinkedList;
    }

    /**
     * 링크드 리스트가 비었을 경우 'NullPointerException' 에러 발생
     */
    public int pop_front() {
        if (empty()){
            throw new NullPointerException();
        }
        return LinkedList.pollFirst();
    }

    public void push_back(int value){
        LinkedList.push(value);
    }

    /**
     * 링크드 리스트가 비었을 경우 'NullPointerException' 에러 발생
     */
    public int pop_back() {
        if (empty()){
            throw new NullPointerException();
        }
        return LinkedList.poll();
    }

    /**
     * 링크드 리스트가 비었을 경우 'NullPointerException' 에러 발생
     */
    public int front() {
        if (empty()){
            throw new NullPointerException();
        }
        return LinkedList.peekFirst();
    }

    /**
     * 링크드 리스트가 비었을 경우 'NullPointerException' 에러 발생
     */
    public int back() {
        if (empty()){
            throw new NullPointerException();
        }
        return LinkedList.peek();
    }

    /**
     * 입력 인덱스가 범위 밖이면 'IndexOutOfBoundsException' 에러 발생
     */
    public void insert(int index, int value) {
        if (index >= 0 || index < size()){
            LinkedList<> newLinkedList = new LinkedList<Integer>();

            for (int i = 0; i < index; i++) {
                newLinkedList.push(LinkedList.get(i));
            }

            newLinkedList.add(index, value);

            for (int i = index; i <= size(); i++) {
                newLinkedList.push(LinkedList.get(i));
            }
            LinkedList = newLinkedList;

        } else {
            throw new IndexOutOfBoundsException();
        }
    }

    /**
     * 입력 인덱스가 범위 밖이면 'IndexOutOfBoundsException' 에러 발생
     */
    public void erase(int index) {
        if (index >= 0 || index < size()){
            LinkedList.remove(index);
        } else {
            throw new IndexOutOfBoundsException();
        }
    }

    /**
     * 0번째 요소부터 가능 -> 0번째 요소 : 마지막 요소
     * 입력 인덱스가 범위 밖이면 'IndexOutOfBoundsException' 에러 발생
     */
    public int value_v_from_end(int n) {
        if (n >= 0 || n < size()){
            return LinkedList.get(size() - 1 - n);
        } else {
            throw new IndexOutOfBoundsException();
        }
    }

    public LinkedList<Integer> reverse() {
        LinkedList<Integer> newLinkedList = new LinkedList<>();

        for (int e : LinkedList)
            newLinkedList.add(0, e);

        return newLinkedList;
    }

    /**
     * 값이 없으면 아무것도 수행하지 않음
     * 다중 값 존재 시, 맨 앞 요소 제거
     */
    public void remove_value(int value) {
        for (int e : LinkedList){
            if (e == value)
                LinkedList.remove(e);
        }
    }
}

```
