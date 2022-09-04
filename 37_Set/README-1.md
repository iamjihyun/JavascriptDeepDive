# 37장 Set과 Map

## 37.1 Set

- Set 객체는 중복되지 않는 유일한 값들의 집합이다.
- 배열과 유사하지만 다음과 같은 차이가 있다.
  | 구분 | 배열 | Set 객체 |
  | ----------------------- | ---- | -------- |
  | 동일한 값을 `중복`하여 포함 | O | X |
  | 요소 `순서`에 의미 | O | X |
  | `인덱스`로 요소에 접근 | O | X |

### 1. Set 객체의 생성

- Set 객체는 Set 생성자 함수로 생성한다.
- Set 생성자 함수에 인수를 전달하지 않으면 빈 Set 객체가 생성된다.
- Set 생성자 함수는 이터러블을 인수로 전달받아 Set 객체를 생성한다. 이때 이터러블의 중복된 값은 Set 객체에 요소로 저장되지 않는다.

```
const set1 = new Set([1,2,3,3]);
console.log(set1);      // Set(3) {1,2,3}

const set2 = new Set('hello');
console.log(set2);      // Set(4) {'h', 'e', 'l', 'o'}
```

### 2. 요소 개수 확인

- Set.prototype.`size` 프로퍼티를 사용한다.

```
const { size } = new Set([1,2,3,3]);
console.log(size);      // 3
```

### 3. 요소 추가

- Set.prototype.`add` 메서드를 사용한다.

```
const set = new Set();
console.log(set);       // Set(0) {}

set.add(1);
console.log(set);       // Set(1) {1}
```

- add 메서드는 새로운 요소가 추가된 Set 객체를 반환한다. add 메서드를 호출한 후에 add 메서드를 연속적으로 호출할 수 있다.

```
const set = new Set();

set.add(1).add(2);
console.log(set);       // Set(2) {1, 2}
```

- Set 객체는 자바스크립트의 모든 값을 요소로 저장할 수 있다.

### 4. 요소 존재 여부 확인

- Set.prototype.`has` 메서드를 사용한다.
- has 메서드는 특정 요소의 존재 여부를 나타내는 `불리언` 값을 반환한다.

```
const set = new Set([1, 2, 3]);

console.log(set.has(2));       // true
console.log(set.has(4));       // false
```

### 5. 요소 삭제

- Set.prototype.`delete` 메서드를 사용한다.
- delete 메서드는 삭제 성공 여부를 나타내는 `불리언` 값을 반환한다.
- delete 메서드에는 인덱스가 아니라 `삭제하려는 요소값을 인수로 전달`해야 한다. (인덱스 갖지 않음)

```
const set = new Set([1, 2, 3]);

set.delete(2);      // true
console.log(set);   // Set(2) {1, 3}
```

- 존재하지 않는 요소를 삭제하려 하면 에러없이 무시된다.
- 불리언 값을 반환하므로 연속적으로 호출할 수 없다.

### 6. 요소 일괄 삭제

- Set.prototype.`clear` 메서드를 사용한다.
- clear 메서드는 언제나 undefined를 반환한다.

```
const set = new Set([1, 2, 3]);

set.clear();        // undefined
console.log(set);   // Set(0) {}
```

### 7. 요소 순회

- Set.prototype.`forEach` 메서드를 사용한다.
- Array.prototyle.forEact 메서드와 유사
  - 첫 번째 인수 : 현재 순회중인 요소값
  - 두 번째 인수 : 현재 순회중인 요소값
  - 세 번째 인수 : 현재 순회중인 Set 객체 자체

```
const set = new Set([1, 2, 3]);

set.forEach((v,v2,set)=> console.log(v,v2,set));
/*
1 1 Set(3) {1, 2, 3}
2 2 Set(3) {1, 2, 3}
3 3 Set(3) {1, 2, 3}
*/
```

- Set 객체는 이터러블이다. 따라서 `for...of 문`으로 순회할 수 있으며, `스프레드 문법`과 `배열 디스트럭처링`의 대상이 될 수도 있다.

### 8. 집합 연산

- Set 객체의 특성은 수학적 집합의 특성과 일치한다.
- Set을 통해 교집합, 합집합, 차집합, 여집합 등을 구현할 수 있다.
