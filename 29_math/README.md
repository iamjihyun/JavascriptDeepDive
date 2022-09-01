# 23장 Math

- 표준 빌트인 객체.
- 생성자 함수가 아니다.
- `정적 프로퍼티`와 `정적 메서드`만 제공한다.

## 23.1 Math 프로퍼티

### 1) Math.PI

- 원주율 PI값(`π` = 약 3.1415926535)을 반환

<br />

## 23.2 Math 메서드

### 1) Math.abs

- 인수로 전달된 숫자의 `절대값`을 반환
- 절대값은 반드시 0 또는 양수이어야 한다.

```
Math.abs(-1);           // 1
Math.abs('-1');         // 1
Math.abs('');           // 0
Math.abs([]);           // 0
Math.abs(null);         // 0
Math.abs(undefined);    // NaN
Math.abs({});           // NaN
Math.abs('string');     // NaN
Math.abs();             // NaN
```

### 2) Math.round

- 인수로 전달된 숫자의 소수점 이하를 `반올림한 정수`를 반환

### 3) Math.ceil

- 인수로 전달된 숫자의 소수점 이하를 `올림한 정수`를 반환

### 4) Math.floor

- 인수로 전달된 숫자의 소수점 이하를 `내림한 정수`를 반환

### 5) Math.sqrt

- 인수로 전달된 숫자의 `제곱근`을 반환

```
Math.sqrt(9);       // 3
Math.sqrt(-9);      // NaN
Math.sqrt(0);       // 0
Math.sqrt();        // NaN
```

### 6) Math.random

- `임의의 난수`(랜덤 숫자)를 반환
- 0 <= Math.random() < 1 (0 이상 1미만의 실수)

예제) 1~10 범위의 랜덤 정수 구하기

```
const random = Math.floor(Math.random()*10) + 1);
console.log(random);
```

해설)

- 0 <= Math.random() < 1
- 0 <= Math.random()\*10 < 10
- 1 <= Math.random()\*10) + 1 < 11
- 1 <= Math.floor(Math.random()\*10) + 1) <= 10
- 1~10 범위의 정수 반환

### 7) Math.pow

- 첫 번째 인수를 밑으로, 두번째 인수를 지수로 `거듭제곱`한 결과를 반환

```
Math.pow(2, 8);     // 256
Math.pow(2, -1);    // 0.5
Math.pow(2);        // NaN
```

- Math.pow 메서드 대신 ES7에서 도입된 `지수연산자` 사용 권장

```
2 ** 2 ** 2;                // 16
Math.pow(Math.pow(2,2),2);  // 16
```

### 8) Math.max

- 전달받은 인수 중에서 `가장 큰 수`를 반환
- 인수가 전달되지 않으면 -Infinity 를 반환

### 9) Math.min

- 전달받은 인수 중에서 `가장 작은 수`를 반환
- 인수가 전달되지 않으면 Infinity 를 반환
