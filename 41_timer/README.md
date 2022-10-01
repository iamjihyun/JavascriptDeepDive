# 41장 타이머

## 41.1 호출 츠케줄링

- 함수를 명시적으로 호출하면 함수가 즉시 실행된다.
- 만약 함수를 일정 시간이 경과된 이후에 호출되도록 함수 호출을 예약하려면 타이머 함수를 사용한다 -> 호출 스케줄링

- 타이머를 생성할 수 있는 타이머 함수 : setTimeout / setInterval
- 타이머를 제거할 수 있는 타이머 함수 : clearTimeout / clearInterval
- 타이머는 ECMAScript 사양에 정의된 빌트인 함수가 아니다. 호스트 객체다 (자바스크립트 실행환경에서 추가로 제공되는 객체 ex. DOM, fetch 등)
- 자바스크립트 엔진은 싱글 스레드로 동작하기 때문에 setTimeout과 setInterval은 비동기 처리 방식으로 동작한다.

<br />

## 41.2 타이머 함수

### setTimeout / clearTimeout

- setTimeout 함수는 두번째 인수로 전달받은 시간(ms)으로 `단 한 번 동작하는 타이머`를 생성한다. 타이머가 만료되면 첫번째 인수로 전달받은 콜백함수가 호출된다.

- `setTimeout(func[, delay, param1, param2, ...])`;
- func : 타이머가 만료된 뒤 호출될 콜백함수
- delay : 타이머 만료시간(ms). 생략할 경우 기본값 0 지정.  
  단, delay가 4ms 이하인 경우 최소 지연시간 4ms가 지정됨
- params : 콜백함수에 전달해야 할 인수가 존재하는 경우 전달함

- setTimeout 함수는 생성된 타이머를 식별할 수 있는 고유한 타이머 id를 반환한다. (브라우저 환경: 숫자, Node.js 환경: 객체)
- 타이머id 를 clearTimeout 함수의 인수로 전달하여 타이머를 취소할 수 있다.

```
const timerId = setTimeout(() => console.log('Hi'), 1000);
clearTimeout(timerId);
```

### setInterval / clearInterval

- setInterval 함수는 두번째 인수로 전달받은 시간(ms)으로 `반복 동작하는 타이머`를 생성한다. 이후 타이머가 만료될 때마다 첫 번째 인수로 전달받은 콜백함수가 호출된다. 이는 타이머가 취소될 때까지 계속된다.

- `setInterval(func[, delay, param1, param2, ...])`;

- setInterval 함수는 생성된 타이머를 식별할 수 있는 고유한 타이머 id를 반환한다.
- 타이머id 를 clearInterval 함수의 인수로 전달하여 타이머를 취소할 수 있다.

```
let count = 1;
const timeoutId = setInterval(() => {
    console.log(count);    // 1 2 3 4 5
    if (count++ === 5) clearInterval(timerId);
}, 1000);
```

<br />

## 41.3 디바운스와 스로틀

- 디바운스와 스로틀은 짧은 시간 간격으로 연속해서 발생하는 이벤트를 그룹화해서 과도한 이벤트 핸들러의 호출을 방지하는 프로그래밍 기법
- 예제 참고 : https://webclub.tistory.com/607
