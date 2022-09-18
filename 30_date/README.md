# Date

날짜와 시간을 위한 메서드를 제공하는 빌트인 객체이자 생성자 함수

**UTC(GMT)는 국제표준시, KST는 한국표준시**

## Date 생성자 함수

`Date` 생성자 함수로 생성한 `Date`객체는 내부적으로 날짜와 시간을 나타내는 정수값을 가진다.

예) 모든 시간의 기점인 1970년 1월 1일 0시를 나타내는 `date`객체는 내부적으로 정수값 0을 가진다.

### 객체 생성 방법

- `new Date()`

인수 없이 호출 하면 현재 날짜와 시간을 가지는 `Date`객체 반환

`Date`객체를 콘솔에 출력하면 날짜와 시간 정보를 출력한다

생성자 함수를 new 연산자 없이 호출하면 날짜와 시간 정보를 나타내는 문자열 반환

- `new Date(milliseconds)`

밀리초를 인수로 전달하면 1970년 1월 1일 기점으로 밀리초 만큼 결과한 날짜와 시간을 나타내는 객체 반환

- `new Date(dateString)`

날짜와 시간을 나타내는 문자열을 인수로 전달하면 지정된 날짜와 시간을 나타내는 `Date` 객체 반환

인수로 전달한 문자열은 `Date.parse` 메서드에 의해 해석 가능한 형식이어야 한다.

- `new Date(*year,*month,day,hour,minute,second,millisecond)`

위 인수들을 인수로 전달하면 지정된 날짜와 시간을 나타내는 `Date` 객체를 반환

이 때 연, 월은 필수이고 월은 0부터 시작이다.

## `Date` 메서드

- `Date.now`

1970년 1월 1일 기점으로 경과한 밀리초를 숫자로 반환

- `Date.parse`

인수로 전달된 지정 시간(`new Dat(dateString)`)까지의 밀리초를 숫자로 반환

- `Date.UTC`

`Date.parse` 와 같지만 인수가 로컬타임이 아닌 UTC로 인식된다.

- `Date.prototype.getFullYear` `Date.prototype.getMonth` `Date.prototype.getDate`

`Date` 객체의 연도,월, 일을 나타내는 정수 반환

- `Date.prototype.setFullYear` `Date.prototype.setMonth` `Date.prototype.setDate`

`Date` 객체의 연도, 월, 일을 나타내는 정수 설정

- `Date.prototype.getDay`

`Date` 객체의 요일을 나타내는 정수 반환 0-6  0: 일요일

- `Date.prototype.getHours` `Date.prototype.getMinutes` `Date.prototype.getSeconds` `Date.prototype.getMillseconds`

`Date` 객체의 시간, 분, 초, 밀리초를 나타내는 정수 반환

- `Date.prototype.setHours` `Date.prototype.setMinutes` `Date.prototype.setSeconds` `Date.prototype.setMilliseconds`

`Date` 객체의 시간, 분, 초, 밀리초를 나타내는 정수 설정

- `Date.prototype.getTime`

1970년 1월 1일 기점으로 `Date` 객체의 시간까지 경과된 밀리초 반환

- `Date.prototype.setTime`

`Date` 객체에 1970년 1월1 일 기멎으로 경과된 밀리초 설정

- `Date.prototype.getTimezoneOffset`

UTC와 `Date` 객체에 지정된 `locale` 시간과의 차이를 분 단위로 반환 KST(한국) = -9

- `Date.prototype.toDateString`

사람이 읽을 수 있는 형식의 문자열로 `Date` 객체의 날짜를 반환

- `Date.prototype.toTimeString`

사람이 읽을 수 있는 형식의 문자열로 `Date` 객체의 시간을 표현한 문자열 반환

- `Date.prototype.toISOString`

ISO 9601 형식으로 `Date` 객체의 날짜와 시간을 표현한 문자열 반환

- `Date.prototype.toLocaleString`

인수로 전달한 로캘을 기준으로 `Date` 객체의 날짜와 시간을 표현한 문자열 반환 

생략시 브라우저가 동작중인 시스템의 로캘 적용 

- `Date.prototype.toLocaleTimeString`

인수로 전달한 로캘을 기준으로 `Date` 객체의 시간을 표현한 문자열 반환 

생략시 브라우저가 동작중인 시스템의 로캘 적용