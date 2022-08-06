## 25.7 프로퍼티

### 인스턴스 프로퍼티

인스턴스 프로퍼티는 `constructor` 내부에서 정의해야 한다.

`constructor` 내부 코드가 실행되기 이전에 이미 내부 `this`에는 클래스가 암묵적으로 생성한 빈 객체가 바인딩 되어있다.

`constructor` 내부 `this`에 인스턴스 프로퍼티를 추가하면 클래스가 암묵적으로 생성한 빈 객체, 즉 인스턴스에 프로퍼티가 추가되어 인스턴스가 초기화된다.

인스턴스 프로퍼티는 언제나 public 하지만 private한 프로퍼티를 정의할 수 있는 사양이 현재 제안 중에 있다.

### 접근자 프로퍼티

접근자 프로퍼티는 자체적으로 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 함수로 구성된 프로퍼티이다.

```js
class Person {
  constructor(firstName, lastName) {
    this.firstName = firstName
    this.lastName = lastName
  }
  // getter 함수
  get fullName () {
    return `${this.firstName} ${this.lastName}`
  }
  // setter 함수
  set fullName () {
    [this.firstName, this.lastName] = name.split(' ')
  }
}
const me = new Person()
```

접근자 프로퍼티 `fullName`에 값을 저장하면 `setter` 함수가 호출되고 접근하면 `getter` 함수가 호출된다.

클래스의 메서드는 기본적으로 프로토타입 메서드가 된다.  
-> 따라서 클래스의 접근자 프로퍼티 또한 인스턴스 프로퍼티가 아닌 프로토 타입 프로퍼티

### 클래스 필드 정의 제안

클래스 필드는 클래스 기반 객체지향 언어에서 클래스가 생성할 인스턴스의 프로퍼티를 가리키는 용어다.

최신 브라우저와 최신 Node.js 에서는 다음 예제와 같이 클래스 필드를 클래스 몸체에 정의할 수 있다.

```js
class Person {
  name = 'Lee'
}
const me = new Person()
console.log(me) // Person {name: 'Lee'}
```

이 때 `this`에 클래스 필드를 바인딩 하면 안된다.  
`this`는 클래스의 `constructor`와 메서드 내에서만 유효하다.

인스턴스를 생성할 때 외부의 초기값으로 클래스 필드를 초기화 하려면 `constructor`에서 클래스 필드를 초기화 해야 한다.  
이 때는 `constructor` 밖에서 클래스 필드를 정의할 필요가 없다.  
클래스가 생성한 인스턴스에 클래스 필드에 해당하는 프로퍼티가 없다면 자동 추가 되기 때문이다.

클래스 필드에는 함수도 할당할 수 있으며 할당 된 함수는 프로토타입 메서드가 아닌 인스턴스 메서드가 된다. (권장X)

### private 필드 정의 제안

`private`의 선두에는 #을 붙여주고 참조할 때도 #을 붙여준다.

`public` 필드는 어디서든 참조할 수 있지만 `private` 필드는 클래스 내부에서만 참조 가능하다.

외부에서는 접근자 프로퍼티를 통해 간접적으로 접근할 수 있다.

`private` 필드는 반드시 클래스 몸체에 정의해야 한다.

### static 필드 정의 제안

`static` 키워드를 이용하여 정적 필드 정의

## 상속에 의한 클래스 확장

기존 클래스를 상속받아 새로운 클래스를 확장하여 정의하는 것

```js
class Animal {
  constructor(age, weight) {
    this.age = age
    this.weight = weight
  }
  eat() {
    return 'eat'
  }
}

class Bird extends Animal {
  fly() {
    return 'fly'
  }
}
```

### extends 키워드

클래스는 상속을 통해 다른 클래스를 확장할 수 있는 문법인 `extends` 키워드가 제공된다.

상속을 통해 확장된 클래스를 서브 클래스, 서브클래스에게 상속된 클래스를 수퍼클래스라 부른다.

`extends`는 수퍼클래스와 서브클래스 간의 상속 관계를 설정한다.  
클래스도 프로토타입을 통해 상속 관계를 구현한다.

수퍼클래스와 서브클래스는 인스턴스의 프로토타입 체인뿐 아니라 클래스 간의 프로토타입 체인도 생성한다. 이를 통해 프로토타입 메서드, 정적 메서드 모두 상속 가능하다.

### 동적 상속

`extends` 키워드 다음에는 클래스뿐만이 아니라 `[[constructor]]` 내부 메서드를 갖는 함수 객체로 평가될 수 있는 모든 표현식을 사용할 수 있다.

```js
function Base1() {}
class Base2 {}
let condition = true

class Derived extends (condition ? Base1 : Base2) {}
```
### 서브 클래스의 constructor

클래스에서 `constructor`을 생략하면 빈 `constructor`가 암묵적으로 정의된다.

프로퍼티를 소유하는 인스턴스를 생성하려면 `constructor` 내부에서 인스턴스에 프로퍼티를 추가해야 한다.

### super 키워드

함수처럼 호출할 수도 있고 `this`와 같이 식별자처럼 참조할 수 있는 특수한 키워드

- `super`을 호출하면 수퍼클래스의 `constructor`을 호출한다.

`super` 키워드 호출 시 주의 사항

1. 서브클래스에서 `constructor`을 생략하지 않는 경우 반드시 `super`을 호출해야 한다.
1. 서브클래스의 `constructor`에서 `super`를 호출하기 전에는 `this`를 참조할 수 없다.
1. `super`는 반드시 서브클래스의 `constructor`에서만 호출한다.

- `super`를 참조하면 수퍼클래스의 메서드를 호출할 수 있다.

1. 서브클래스의 프로토타입 메서드 내의 super.함수는 수퍼클래스의 프로토타입 메서드의 함수를 가리킨다.
    1. ES6의 메서드 축약 표현으로 정의된 함수만이 [[HomeObject]]를 가지며 super를 참조할 수 있다. 단 super 참조는 부모 클래스의 메서드를 참조하기 위해 사용하므로 서브클래스의 메서드에서 사용해야 한다.
2. 서브클래스의 정적 메서드 내에서 super.함수는 수퍼클래스의 정적 메서드 함수를 가리킨다.

### 상속 클래스의 인스턴스 생성 과정
1. 서브클래스의 `super` 호출  
  서브클래스는 자신이 직접 인스턴스를 생성하지 않고 수퍼클래스에게 인스턴스 생성을 위임 => 서브클래스의 `constructor`에서 반드시 `super`를 호출해야 하는 이유이다.
1. 수퍼클래스의 인스턴스 생성과 `this` 바인딩
1. 수퍼클래스의 인스턴스 초기화
1. 서브클래스 `constructor`로의 복귀와 `this` 바인딩  
  super가 반환한 인스턴스가 `this`에 바인딩.
1. 서브클래스의 인스턴스 초기화
1. 인스턴스 반환
