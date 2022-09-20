# 팩토리 패턴(Factory Pattern)

## 1. 팩토리 패턴이란?

객체를 생성하는 인터페이스는 미리 정의하되, 인스턴스를 만들 클래스의 결정은 서브 클래스 쪽에서 내리는 패턴이다.

즉, 여러개의 서브 클래스를 가진 슈퍼 클래스가 있을 때 인풋에 따라 하나의 자식 클래스의 인스턴스를 리턴해주는
방식이다.

이런 팩토리 패턴은

- 어떤 클래스가 자신이 생성해야 하는 객체의 클래스를 예측할 수 없을 때
- 생성할 객체를 기술하는 책임을 자신의 서브클래스가 지정했으면 할 때

사용된다.

---

## 2. 자바스크립트에서의 팩토리 패턴

### 2-1. 팩토리 패턴 적용 전

```javascript
class Car {
  constructor(props) {
    this.name = props.name;
    this.year = props.year;
    this.price = props.price;
  }
  getDiscount() {
    this.price -= this.sale;
  }
  getInfo() {
    return this.name + "의 가격은 " + this.price + "원 입니다.";
  }
}

class Avante extends Car {
  constructor(props) {
    super(props);
    this.sale = Math.floor(props.price / 50);
  }
}

class Sonata extends Car {
  constructor(props) {
    super(props);
    this.sale = Math.floor(props.price / 60);
  }
}

class Grandeur extends Car {
  constructor(props) {
    super(props);
    this.sale = Math.floor(props.price / 70);
  }
}

const getFinalPrice = (info) => {
  let car;
  if (info.name.toLowerCase() === "avante") {
    car = new Avante(info);
  } else if (info.name.toLowerCase() === "sonata") {
    car = new Sonata(info);
  } else if (info.name.toLowerCase() === "grandeur") {
    car = new Grandeur(info);
  }
  car.getDiscount();
  return car.getInfo();
};
```

이와 같은 코드가 있다고 가정하자. 자동차 주문이 들어오면 자동차의 이름에 따라 `car` 인스턴스를 생성하고,
할인하고, 최종 정보를 리턴하는 간단한 코드이다.

하지만 자동차의 종류가 더 많아진다면 코드변화에 대응하기엔 좋지 않는 코드이다. 즉 변화에 닫힌코드이다.

**코드를 구현할 때에는 변하는 부분과 변하지 않는 부분을 분리**해야 하는데 위의 코드에선 `if`문이 바로 변하는 부분이다.
이를 따로 분리하여 공장으로 만들어보자.

---

### 2-2. 팩토리 패턴 적용 후

```javascript
class Car {
  constructor(props) {
    this.name = props.name;
    this.year = props.year;
    this.price = props.price;
  }
  getDiscount() {
    this.price -= this.sale;
  }
  getInfo() {
    return this.name + "의 가격은 " + this.price + "원 입니다.";
  }
}

class Avante extends Car {
  constructor(props) {
    super(props);
    this.sale = Math.floor(props.price / 50);
  }
}

class Sonata extends Car {
  constructor(props) {
    super(props);
    this.sale = Math.floor(props.price / 60);
  }
}

class Grandeur extends Car {
  constructor(props) {
    super(props);
    this.sale = Math.floor(props.price / 70);
  }
}

class CarFactory {
  nameMap = {
    avante: Avante,
    sonata: Sonata,
    grandeur: Grandeur,
  };
  create(props) {
    try {
      const Type = this.nameMap[props?.name?.toLowerCase()];
      return new Type(props);
    } catch (error) {
      console.error("error create new car", error);
    }
  }
}
```

`CarFactory`에 대해 자세히 살펴보자.

위의 코드를 살펴보면 `CarFactory` 클래스가 객체를 찍어내는 역할을 한다. 즉, 객체를 만드는 공장이다.
`CarFactory`의 메서드엔 `create`가 있고 이를 호출하여 원하는 자동차를 만들 수 있다. 예를 들어 보자.

```javascript
const factory = new CarFactory();
const car1 = factory.create({ name: "Avante", year: 2016, price: 10000000 });
```

먼저 `factory`인스턴스를 하나 생성하고 `create` 메서드를 호출하는데 매개변수로 객체로 전달한다.
이 객체엔 자동차의 정보가 담겨져 있다.

`create` 메서드가 실행되는 과정을 자세히 살펴보자.

1.  `create` 메서드가 호출되면 매개변수의 `name`의 값에 따라 `Type`이 정해진다.

    ```javascript
    const Type = this.nameMap[props?.name?.toLowerCase()];
    ```

    `Type`에 따라 어떤 종류의 자동차가 만들어지는지 정해진다. 위의 예시에선 `name`의 값이 `Avante`이기 때문에
    아반때 자동차가 만들어진다.

2.  `Type`에 맞는 자동차 인스턴스가 만들어지고 이를 반환한다.

    ```javascript
    return new Type(props);
    ```

3.  예제에서는 아반때 자동차가 만들어 지므로 `Avante` 클레스가 생성이되고 이 클래스는 `Car` 클래스를 상속 받고있다.

    ```javascript
    class Avante extends Car {
      constructor(props) {
        super(props);
        this.sale = Math.floor(props.price / 50);
      }
    }

    class Car {
      constructor(props) {
        this.name = props.name;
        this.year = props.year;
        this.price = props.price;
      }
      getInfo() {
        return this.name + "의 가격은 " + this.price + " 입니다.";
      }
    }
    ```

4.  생성된 `Avante` 자동차의 인스턴스이다.    
    <img width="591" alt="Factory1" src="https://user-images.githubusercontent.com/57981252/191270533-b1b98635-106f-4613-af94-bebc81900cd0.png">

---

### 2-3. 자동차의 최종 가격을 반환하는 함수

```javascript
const getFinalPrice = (info) => {
  const factory = new CarFactory();
  const car = factory.create(info);
  car.getDiscount();
  return car.getInfo();
};
```

팩토리 패턴을 적용함으로써 자동차 인스턴스를 만드는 부분을 따로 분리하여 관리를 할 수 있게 되었다.

---

### 2-4. Array.map() 메서드를 사용한 인스턴스 생성

만약 여러 대의 자동차 정보가 담긴 `data`가 받았다고 생각해보자. 우리는 이 `data`를
가지고 모든 자동차 인스턴스를 만들어야 한다. `data`의 예는 아래와 같다.

```javascript
const data = [
  { name: "Avante", year: 2012, price: 10000000 },
  { name: "Sonata", year: 2022, price: 30000000 },
  { name: "Avante", year: 2016, price: 18000000 },
  { name: "Grandeur", year: 2008, price: 15000000 },
  { name: "Genesis", year: 2020, price: 40000000 },
];
```

`data`를 바탕으로 자동차 인스턴스를 만드는 코드는 아래와 같다.

```javascript
const factory = new CarFactory();
const cars = data.map((item) => factory.create(item));
```

인덱스4번 데이터에 해당하는 인스턴스는 생성되지 않고 나머지 자동차 인스턴스는 생성된다. `error`는 `create` 메서드 내에서 발생한 것이다.

![Factory2](https://user-images.githubusercontent.com/57981252/191270575-76ec94ab-c59f-4d58-ab58-e4dd7c4f9cfd.png)

> 만약 `create` 메서드를 `static` 으로 정의하면 정적 메서드가 되며 이는 클래스의 인스턴트 없이 호출이 가능하게 되
> 메모리를 절약할 수 있고 개별 인스턴스에 묶이지 않으며 클래스 내의 함수를 정의할 수 있다.

---

## 출처

[[생성 패턴] 팩토리 패턴(Factory Pattern) 이해 및 예제](https://readystory.tistory.com/117)  
[Javascript Factory Pattern 팩토리 패턴 반복 객체 생성 패턴](https://aljjabaegi.tistory.com/617)  
[팩토리메소드 패턴(Factory Method Pattern)](https://kyungyeon.dev/posts/42)

도움이 많이 되었던 유튜브 🎬

- 개발자가 알아야할 디자인패턴 | ep2. Factory Pattern | 자바스크립트 팩토리 패턴   
  [![개발자가 알아야할 디자인패턴 | ep2. Factory Pattern | 자바스크립트 팩토리 패턴](https://img.youtube.com/vi/L78FbkyOcyk/0.jpg)](https://youtu.be/L78FbkyOcyk)
- Design pattern, Factory Pattern, 디자인패턴, 팩토리 패턴   
  [![Design pattern, Factory Pattern, 디자인패턴, 팩토리 패턴](https://img.youtube.com/vi/AmwEIt0vhxA/0.jpg)](https://youtu.be/AmwEIt0vhxA)
- 디자인패턴, Factory Method Pattern, 팩토리 패턴    
  [![디자인패턴, Factory Method Pattern, 팩토리 패턴](https://img.youtube.com/vi/ejXUhFKcbIU/0.jpg)](https://youtu.be/ejXUhFKcbIU)

---
