# 32장 String

## 32.1 String 생성자 함수

- 표준 빌트인 객체인 String 객체는 생성자 함수 객체다.
- new 연산자와 함께 호출하여 String 인스턴스를 생성할 수 있다.
- new 연산자를 사용하지 않고 String 생성자 함수를 호출하면 String 인스턴스가 아닌 문자열을 반환한다.

```
const strObj = new String(123);
console.log(strObj);
// String {0: "1", 1: "2", 2: "3", length: 3, [[PrimitiveValue]]: "123"}

String(123);
// "123"
```

<br>

## 32.2 length 프로퍼티

- length 프로퍼티는 문자열의 문자 개수를 반환한다.

<br>

## 32.3 String 메서드

- String 객체에는 원본 String 래퍼 객체를 직접 변경하는 메서드는 존재하지 않는다. 즉 `String 객체의 메서드는 언제나 새로운 문자열을 반환한다.` 문자열은 변경 불가능한 원시값이기 때문에 String 래퍼 객체도 읽기 전용 객체로 제공된다.

### 1. string.prototype.indexOf

- 대상 문자열에서 인수로 전달받은 `문자열을 검색`하여 `첫 번째 인덱스를 반환`한다.
- 검색에 실패하면 -1 반환한다.

```
const str = 'Hello World';

str.indexOf('l');   // 2
str.indexOf('x');   // -1
```

- 2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.

```
str.indexOf('l', 3);    // 3
```

- 특정 문자열이 존재하는지 확인할 때 유용하다.
- ES6) String.prototype.includes 메서드를 사용하면 가독성이 더 좋다.

```
if (str.indexOf('Hello') !== -1) {}
if (str.includes('Hello')) {}
```

### 2. string.prototype.search

- 대상 문자열에서 인수로 전달받은 `정규 표현식`과 매치하는 문자열을 검색하여 일치하는 문자열의 `인덱스를 반환`한다.
- 검색에 실패하면 -1을 반환한다.

### 3. string.prototype.includes

- 대상 문자열에서 인수로 전달받은 `문자열이 포함되어 있는지` 확인하여 그 결과를 `true 또는 false`로 반환한다.
- 2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.

### 4. string.prototype.startsWith

- 대상 문자열에서 인수로 `전달받은 문자열로 시작하는지` 확인하여 그 결과를 `true 또는 false`로 반환한다.
- 2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.

### 5. string.prototype.endsWith

- 대상 문자열에서 인수로 `전달받은 문자열로 끝나는지` 확인하여 그 결과를 `true 또는 false`로 반환한다.
- 2번째 인수로 검색을 시작할 인덱스를 전달할 수 있다.

### 6. string.prototype.charAt

- 대상 문자열에서 인수로 `전달받은 인덱스에 위치한 문자`를 검색하여 반환한다.
- 인덱스가 문자열의 범위를 벗어난 정수인 경우 빈 문자열을 반환한다.

```
const str = 'Hello';
console.log(str.charAt(0));   // 'H'
console.log(str.charAt(5));   // ''
```

### 7. string.prototype.substring

- 대상 문자열에서 `첫 번째 인수로 전달받은 인덱스에 위치하는 문자부터 두번째 인수로 전달받은 인덱스에 위치하는 문자의 바로 이전 문자까지` `부분 문자열`을 반환한다.
- 두 번째 인수를 생략하면 첫 번째 인수로 전달한 인덱스에 위치하는 문자부터 마지막 문자까지 부분 문자열을 반환한다.
- 특징
  - 첫 번째 인수 > 두 번째 인수 : 두 인수는 교환됨
  - 인수 < 0 또는 NaN : 0으로 취급됨
  - 인수 > 문자열의 길이 : 인수는 문자열의 길이로 취급됨

```
const str = 'Hello World';

str.substring(1, 4);    // ell
str.substring(4, 1);    // ell

str.substring(1);       // 'ello World'
str.substring(1, 100);  // 'ello World'
```

### 8. string.prototype.slice

- slice 메서드는 substring 메서드와 동일하게 동작한다. 단, slice 메서드에는 `음수인 인수를 전달할 수 있다.`

```
const str = 'Hello World';

str.substring(-5);  // 'Hello World'
str.slice(-5);      // 'World'
```

### 9. string.prototype.toUpperCase

- 대상 문자열을 `모두 대문자로 변경한 문자열`을 반환한다.

### 10. string.prototype.toLowerCase

- 대상 문자열을 `모두 소문자로 변경한 문자열`을 반환한다.

### 11. string.prototype.trim

- 대상 문자열 `앞뒤에 공백 문자가 있을 경우 이를 제거한 문자열`을 반환한다.
- `trimStart`, `trimEnd`를 사용하면 대상 문자열 앞 또는 뒤에 공백 문자가 있을 경우 이를 제거한 문자열을 반환한다.

```
const str = '       foo   ';

str.trim();         // 'foo'
str.trimStart();    // 'foo   '
str.trimEnd();      // '       foo'
```

### 12. string.prototype.repeat

- 대상 문자열을 `인수로 전달받은 정수만큼 반복해 새로운 문자열`을 반환한다.
  - 인수가 0 : 빈 문자열 반환
  - 인수가 음수 : RangeError 를 발생
  - 인수 생략 : 기본값 0이 설정

```
const str = 'Hello';

str.repeat();    // ''
str.repeat(0);   // ''
str.repeat(2);   // 'HelloHello'
str.repeat(-1);  // RangeError: Invalid count value
```

### 13. string.prototype.replace

- 대상 문자열에서 `첫 번째 인수로 전달받은 문자열 또는 정규표현식을 검색하여 두번째 인수로 전달한 문자열로 치환한 문자열`을 반환한다.
- 검색된 문자열이 여럿 존재할 경우 `첫 번째로 검색된 문자열만 치환`한다.

```
const str = 'Hello world world';

str.replace('world', 'Lee');    // 'Hello Lee world'
```

- 특수한 교체 패턴을 사용할 수 있다.  
  ( $& : 검색된 문자열을 의미 )

```
const str = 'Hello world';

str.replace('world', '<strong>$&</strong>');
```

- 첫 번째 인수로 정규 표현식을 전달할 수도 있다.
- 두번째 인수로 치환 함수를 전달할 수도 있다.

### 14. string.prototype.split

- 대상 문자열에서 `첫 번째 인수로 전달받은 문자열 또는 정규표현식을 검색하여 문자열을 구분한 후, 분리된 각 문자열로 이루어진 배열`을 반환한다.
  - 인수로 빈 문자열 전달 : 각 문자를 모두 분리
  - 인수 생략 : 대상 문자열 전체를 단일 요소로 하는 배열 반환
- 두 번째 인수로 배열의 길이를 지정할 수 있다.

```
const str = 'How are you?'

str.split(' ');     // ['How', 'are', 'you?']
// \s = [\t\r\n\v\f] (여러가지 공백 문자)
str.split(/\s/);    // ['How', 'are', 'you?']

str.split('');      // ['H', 'o', 'w', ' ', 'a', 'r', 'e', ' ', 'y', 'o', 'u', '?']
str.split();        // ['How are you?']

str.split(' ', 2);  // ['How', 'are']
```
