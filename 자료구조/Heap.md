# 힙(Heap)과 우선순위 큐(Priority Queue)

## 1. 우선순위 큐란?

힙에 대해 살펴보기 전 우선순위 큐에 대해 먼저 살펴보자. 우선순위 큐을 먼저 살펴보는 이유는 힙이
우선순위 큐를 구현하기 위해 고안된 완전 이진 트리 형태의 자료구조이기 때문이다.

- 큐(Queue): 먼저 들어오는 데이터가 먼저 나가는 FIFO 형식의 자료구조
- 우선순위 큐(Priority Queue): 먼저 들어온 데이터가 아니라, 우선순위가 높은 데이터가 먼저 나감

우선순위 큐는 배열, 연결 리스트, 힙으로 구현이 가능하다. 이 중 힙으로 구현하는 것이 가장 효율적이다.

![우선순위 큐 구현 비교](https://velog.velcdn.com/images%2Fyanghl98%2Fpost%2Fc64db4c9-6151-4c26-9f06-bb2b9193168a%2Fimage.png)

우선순위 큐의 사용 사례는 아래와 같다.

- 시물레이션 시스템
- 네트워크 트래픽 제어
- 운영 체제에서의 작업 스케쥴링

---

## 2. 힙이란?

- 완전 이진 트리의 일종
- 여러 값 중, 최대값과 최소값을 빠르게 찾아내도록 만들어진 자료구조
- 일종의 반정렬 상태(느슨한 정렬 상태)를 유지
  - 큰 값이 상위 레벨에 있고 작은 값이 하위 레벨에 있다는 정도
- 중복된 값을 허용(이진 탐색 트리에서는 중복된 값을 허용하지 않음)

---

## 3. 힙의 종류

![힙의 종류](https://gmlwjd9405.github.io/images/data-structure-heap/types-of-heap.png)

1. 최대 힙(max heap)
   - 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리
2. 최소 힙(min heap)
   - 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리

---

## 4. 힙 구현하기

힙을 구현 하기 전 몇 가지 사항을 짚고 넘어가자.

- 힙을 저장하는 표준적인 자료구조로 **배열**을 이용한다.
- 구현을 쉽게 하기 위해 배열의 첫 번째 인덱스인 0은 사용되지 않는다.
- 특정 위치의 노드 번호는 새로운 노드가 추가되어도 변하지 않는다.
- 부모 노드와 자식 노드의 관계

  - 왼쪽 자식의 인덱스 = (부모의 인덱스) \* 2
  - 오른쪽 자식의 인덱스 = (부모의 인덱스) \* 2 + 1
  - 부모의 인덱스 = Math.floor(자식의 인덱스 / 2)

    ![부모 노드와 자식 노드의 관계](https://gmlwjd9405.github.io/images/data-structure-heap/heap-index-parent-child.png)

위의 내용을 바탕으로 최소 힙을 구현한다.

---

### 4-1. 힙의 기본 구조

```javascript
class Heap {
  constructor() {
    this.heap = [null];
  }
}
```

`this.heap`을 배열로 이용하여 선언을 하고 첫 번째 요소는 `null`로 저장한다.

---

### 4-2. 힙에 요소 추가하기

```javascript
class Heap {
  // ...
  push(value) {
    this.heap.push(value);
    let cur_index = this.heap.length - 1;
    let parents_index = Math.floor(cur_index / 2);

    while (cur_index !== 1 && this.heap[parents_index] > value) {
      [this.heap[parents_index], this.heap[cur_index]] = [
        this.heap[cur_index],
        this.heap[parents_index],
      ];
      cur_index = parents_index;
      parents_index = Math.floor(cur_index / 2);
    }
  }
}
```

최소 힙은 부모 노드가 제일 작아야 한다. 현재 노드와 부모 노드의 값을 비교하여 부모 노드의 값이 크다면
그 둘을 서로 바꾸어 준다.

만약 현재 노드의 인덱스가 1이거나 현재 노드가 부모 노드 보다 값이 작다면 반복문 더 이상 실행되지 않는다.

---

### 4-3. 힙에 요소 제거하기

```javascript
class Heap {
  // ...
  pop() {
    // 1.
    const value = this.heap[1];

    // 2.
    if (this.heap.length <= 2) this.heap = [null];
    else this.heap[1] = this.heap.pop();

    let cur_index = 1;
    let left_index = cur_index * 2;
    let right_index = cur_index * 2 + 1;

    // 3. 루트만 있는 상황
    if (!this.heap[left_index]) return value;
    // 4. 왼쪽 자식 하나만 있는 상황
    if (!this.heap[right_index]) {
      if (this.heap[left_index] < this.heap[cur_index]) {
        [this.heap[left_index], this.heap[cur_index]] = [
          this.heap[cur_index],
          this.heap[left_index],
        ];
      }
      return value;
    }

    // 5. 왼쪽 자식과 오른쪽 자식이 모두 있는 경우
    while (
      // 6.
      this.heap[left_index] < this.heap[cur_index] ||
      this.heap[right_index] < this.heap[cur_index]
    ) {
      // 7.
      let min_index =
        this.heap[left_index] > this.heap[right_index]
          ? right_index
          : left_index;
      // 8.
      [this.heap[min_index], this.heap[cur_index]] = [
        this.heap[cur_index],
        this.heap[min_index],
      ];
      // 9.
      cur_index = min_index;
      left_index = cur_index * 2;
      right_index = cur_index * 2 + 1;
    }
    return value;
  }
}
```

1. 가장 작은 요소는 항상 `this.heap[1]`에 위치한다. 이를 `value`에 할당한다.
2. 가정 먼저해야 할 과정은 배열의 `this.heap`의 마지막 요소를 `root`위치에 배치하는 것이다.
3. 루트만 있는 상황
   - 요소의 이동 없이 바로 `value`를 반환한다.
4. 왼쪽 자식 하나만 있는 상황
   - 왼쪽 자식의 값과 현재 인덱스의 값을 비교하여 왼쪽 자식의 값이 더 작으면 두 개의 값을 서로 바꾼다.
5. 왼쪽 자식과 오른쪽 자식이 모두 있는 경우
   - 아래의 반복문을 실행한다.
6. 왼쪽 자식과 오른쪽 자식의 값 중 하나라도 현재 인덱스의 값 보다 작으면 반복문을 계속 실행된다.
   즉, 부모의 값이 자식들의 값 보다 작아져야 반복문은 종료된다.
7. 왼쪽 자식과 오른쪽 자식의 값을 비교하여 더 작은 값을 가지는 인덱스를 `min_index`에 할당한다. 이때 오른쪽 자식의
   값이 없다면 비교 값은 항상 `false`가 되므로 이점을 유의해야 한다.
8. 부모의 값과 자식의 값(더 작은)을 비교하여 부모의 값 보다 자식의 값이 더 작으면 두 개의 값을 서로 바꾼다.
9. 다음 비교를 위해 각각의 값들을 바꾼다.

---

## 참고

[[자료구조] 힙(heap)이란](https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)  
[[자료구조] 우선순위 큐와 힙 (Priority Queue & Heap)](https://suyeon96.tistory.com/31)  
[[자료구조] JS로 구현하는 HEAP](https://velog.io/@longroadhome/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-JS%EB%A1%9C-%EA%B5%AC%ED%98%84%ED%95%98%EB%8A%94-HEAP)
