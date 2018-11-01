---
layout: post
title: "타입스크립트 코리아 강좌 정리"
subscript: "타입스크립트를 이해해보자"
tags: ["Typescript", "beginer"]
categories: ""
comments: true
permalink: /study/:title
date: 2018/10/30
---


# 1. Typescirpt 에 관하여

> tpyscript 는 자바스크립트를 포함한 프로그래밍 언어

- 타입스크립트는 'Compiled Language'이다
- 자바스크립트는 'Interpreted Language'이다

> 그러나 엄밀히 따지자면 컴파일 언어라고 보기는 힘들고 메타 프로그래밍이라고도 하며, 트랜스파일(바밸 등) 언어라고도 보기도한다.

| Compiled               | Interpreted            |
| ---------------------- | ---------------------- |
| 컴파일이 필요          | 컴파일이 필요없음      |
| 컴파일러가 필요        | 컴파일러가 필요없음    |
| 컴파일하는 시점이 있음 | 컴파일하는 시점이 없음 |
| 컴파일된 결과물 실행   | 코드 자체를 실행       |

> 컴파일 언어는 최적화 과정을 거침 \* 특히 타입스크립트는 타입을 체크하는 과정을 거침

## 정적타입 언어 VS 동적 타입 언어

### 정적타입 언어

미리 타입을 정의 해놓고 사용함

### 동적 타입언어

타입이 정의되어 있지 않고 자유럽게 변화가 가능

타입스크립트는 정적타입 언어의 장점을 자바스크립트에 결합한 언어이다.

## Traditional Compiled Language

- 컴파일 언어라고 한다
- C, C++, go 등
- 일반적으로 실행시 기계어로 바꾸는 방식(인터프리터 언어)보다 빠르다.

TS => JS

이 강좌에서 배우는 것은 컴파일은 어떤 역할을 하는지 어떤 도구들이 있고 올바르게 사용하는 방법과, 타입스크립트 자체를 이해

# 2. 개발 환경 구축

## Node.js 설치

강좌 외적으로 저는 Node.js 의 버전을 자유롭게 바꾸다보니 NVM 사용을 권장합니다. 예) Lambda 에서 지원하는 버전과 React 에서 지원하는 버전이 전혀 다르면서 생기는 문제 등등

curl 을 이용해 설치

```
curl -o https://raw.githubusercontent.com/creationix/nvm/v0.26.1/install.sh | bash
```

## Browser 설치

Chrome, firefox 와 같이 검사가 있는 브라우저를 추천 함

## Tpyscript compiler 설치

```
npm i typescript -g // 전역으로 설치됩니다
```

## IDE 설치

[vscode(무료)](https://visualstudio.microsoft.com/ko/?rr=https%3A%2F%2Fwww.google.co.kr%2F), intelliJ(유료)

- visual studio code 는 Typscript 로 만들어졌다.
- 타입스크립트 지원이 강력하다

## tsc init

tsc 설정 파일을 init 함
target, module, strict 정도가 기본 설정으로 되어있음.

## ts lint

```
npm i tslint -D
```

tslint --init

# 3. Compiler Options
## tsconfig
[ts config 가이드](http://json.schemastore.org/tsconfig)

## 최상위 프로퍼티
1. CompileOnSave: 파일 저장시 자동 컴파일, Visual studio에서 사용 가능
2. extends: v2.1 new spec
3. compileOptions 
    - 다양한 옵션이 제공됨
    - typeRoots: 배열 안에 들어있는 경로들 아래에 모듈만 가져옴
    - types: 배열 안에 모듈, ./node_modules/@types/ 안의 모듈 이름에서 찾아옴
    - typeRoots, types와 함께 사용하지 않음
    - target: 컴파일 해서 어떤 자바스크립트 버전으로 downgrade 시킬거냐 기본은 es3이다
    - lib: 기본 type definition 라이브러리를 어떤 것을 사용할 것이냐
        - lib를 지정하지 않을때 
        - target이 'es3'이고 디폴트로 lib.d.ts를 사용함
        - target이 'es5'이면, 디폴트로 dom, es5, scripthost를 사용함
    - outDir: 소스 구조의 전부를 컴파일 하려면 사용
    - outFile: 구조 상관없이 컴파일 하려면 사용
    - module: 결과물이 어떤 js파일을 쓸건지 target이 es6면 es6가 기본값, es6가 아니면 'commonjs'가 기본값
4. files: 
    - 상대 혹은 절대 경로의 리스트 배열
    - exclude 보다 우선순위 높음
5. include
    - exclude 보다 우선순위 낮음
    - *같은걸 사용하면 .ts / .tsx 등 설정한 것만 include 함
6. exclude
    - 설정 안하면 기본 4가지를 설정 (node_modules, browser_components, jspm_packages, outDIr)를 기본적으로 제외
    - outDir은 항상 제외



# 4. typescript basic type
- Typescript에서 프로그램 작성을 위해 기본 제공하는 데이터 타입
- Javscript 기보 자료형을 포함
    - ECMAScript 표준에 따른 기본 자료형은 6가지
    - Boolean
    - String
    - Null
    - Undefined
    - Symbol
    - Array: Object형
- 프로그래밍을 도울 몇가리 타입이 더 제공됨
    - Any
    - Void
    - Never
    - Enum
    - Tuple: Object

## literal?
값자체가 변하지 않는 값을 의미함
상수와 다른 것은 상수는 가리키는 포인터가 고정이라는 것이고, 리터럴은 그 자체가 값이자 리터럴

## 권장 소문자를 사용해라
new Number(5) -> number(5);

new Boolean(false) -> boolrean(false);

## Any
- 어떤 타입이든 상관없음 
- 그러나 권장하지 않음 (이걸 쓸꺼면 그냥 es6바밸 문법을 사용해라)

## Tuple
- 배열인데 한가지 타입이 아닐 경우
- 객체
- 사용할때 주의가 필요함

# 5. var, let, const
- var
    - es5
    - 함수 스코프
    - 호이스팅이 가능
    - 재선언 가능
- let, const
    - es6
    - 블록 스코프
    - 호이스팅 불가능
    - 재선언 불가
- var 말고 let, const를 사용하자

## let, const 차이점
```javascript
let a: string = "에이";
let a = "에이"; //자동으로 String으로 타입을 맞춰줌

const b: string = "비";
const b = "비"; //별도의 타입을 만들어 주지 않음
```

# 6. Type assersions
- 형변환과는 다름
    - 형변형은 실제 데이터 구조를 바꿔줌
- '타입이 이것이다'라고 컴파일러에게 알려주는 것을 의미함
    - 그래서 작성자가 100% 신뢰하는 것이 중요하다.
- 문법적으로는 두가지 방법이 있다
    - 변수 as 강제할 타입
    - <강제할 타입>변수
```javascript
let a: any = "this is a string";
let b: number = (someValue as a).length;
```

## 타입 별칭
- 인터페이스와 유사해 보임
- Primitive, Union Type, Tuple
- 기타 직접 작성해야하는 타입을 다른 이름에 저장할 수 있다.
- 만들어진 타입의 refer로 사용하는 것이지 타입을 만드는것은 아니다.

### Union
```javascript
let a: any;
let b: string | number;

b = "스트링";
b = 0;

//만약 사례가 복잡하다면?

function test(arg: string | number): string | number {
    return arg;
}
//위와 같이 작성할때마다 해주는게 힘들다보니 사용함
type StringOrNumber = string | number; //이게 union타입

function test(arg: StringOrNumber): StringOrNumber {
    return arg
}
```

### interface
```javascript

//interface가 없다면
const person: {name: string; age: number} = {
    name: 'MrMoon',
    age: 12
};

//interface를 사용한다면
interface Person{
    name: string;
    age: number
}
const person: Person = {
    name: 'mrMoon',
    age: 12
}

// 주요 사용처
function hello(p: Person): void {
    console.log(`안녕하세요 ${p.name} 입니다`)
}

```

### interface optional
```javascript
interface Person {
    name: string;
    age?: number; //age를 강제하지 않음
}
```

### indexable type
```javascript
interface Person {
    name: string;
    [index: string]: string;
}
const person : Person = {
    name: "mark";
}
person.anybody = "Anna";

//여기서 접근하는 index를 어레이로 선언했기 때문에 가능 함
interface Person2 {
    [index: number]: string;
}

const p2: Person2 = {};
p2[0] = "hi";
p2[100] = "hello";
```

위와 같이 array에 string이나 number로 interface를 만들어줄 순 있지만 array는 아님

## interface in funciton
```javascript
interface Person {
    name: string;
    hello(): string;
}

const person: Person = {
    name: 'mark',
    hello(): string{
        return 'hello world';
    }
}
```

## class implements interface
```javascript
interface IPerson {
    name: string;
    hello(): void;
}

class Person implements IPerson {
    name: string = null;

    constructor(name: string) {
        this.name = name;
    }
    hi(): void {
        console.log('This is hi');
    }
    hello(): void {
        console.log(`hello i am ${name}`);
    }
    
}

const person: IPerson = new Person("moon");
const person: Person = new Person("moon");
//두가지 모두 사용 가능하다
```
>IPerson의 타입을 가지고 있는 person은 interface에서 정의하지 않은 hi 함수에 접근할 수 없다.

## string OR number
```javascript
interface StringArray {
    [index: number]: string;
}

const sa: StringArray = {};
sa[100] = '백';
```

# 7. 클래스

## class
```javascript
class Person {
    name: string;
    age: number;
    // 모든 프로퍼티는 public
    constructor(name: string) {
        this.name = name
    }

    // 할당하지 않는 변수는 undefined가 되어서 나오지 않음
    // 그래서 = null이라고 해주는게 일단 좋음 (기본적인 프로그래밍 방식)
}

const person = new Person('Mark');
```
1. 생성사 함수가 없으면 디폴트 생성자가 불린다.
1. 클래스의 프로퍼티 혹은 멤버 변수가 정의되어 있지만, 값을 대입하지 않으면 undefined이다.
1. 접근 제어자는 public이 디폴트 이다.

## 접근 제어자 - private

```javascript
class Person {
    private _name: string = 'Mark';
    private _age: number;
}

const person = new Person('Mark');
```

1. 디폴트 값은 public 이고 private 로 선언한 프로퍼티 접근 불가능 (c#과 흡사)


## protected
private는 부모 클래스건 어디서건 절대로 접근이 안되는 반면에 protected는 부모에서는 접근이 가능함

```javascript
class Person {
    protected _name: string = 'amark';
    private _age: number = null;
}

class Child extends Person {

    constructor() {
        super(); // constructor에서 무언가 작업을 하기 위해서는 super를 해줘야함 (상속 받았을 때)

        this._name += '아들';

    }
    getName() {
        return this._name
    }
    getAge() {
        return this._age //접근이 안됨
    }
}

const person: Child = new Child();

```

## 클래스와 메서드
```javascript
class Person {
    // protected _name: string = 'amark';
    // private _age: number = null;

    // 굳이 변수 선언없이 이렇게 해도 가능
    constructor(protected name: string, protected age: number){

    }

    hello(): void {
        console.log(this.name);
    }

    //arrow function도 가능
    printHello = (): void => {
        console.log('hello world');
    }
}

const person: Person = new Person('Moon', 35);

class Child extends Person {

    constructor() {
        super('Mark Jr', 5);
    }
}

const child: Child = new Child('Mark', 35);
child.hello();
// console : Mark Jr
```

- 클래스를 상속받아서 사용하려면 꼭 constructor 에서 super()를 해줘야함

## 클래스의 getter, setter
```javascript

interface IPerson {
    getName();
}

//인터페이스에서 이렇게 사용할 수도 있음

class Person implements IPerson{
    private _name: string;
    private _age: number;

    constructor(name: string, age: number) {
        this._name = name;
        this._age = age;
    }

    get name() {
        return this._name;
    }
    
    set name(name: string) {
        this._name = name;
    }

    // get set을 안쓰고 이방법도 사용 가능

    getName(): string {
        return this._name;
    }
}

const person: IPseron = new Person('moon', 26);
console.log(person.name); // moon
person.name = 'moon jong min';
console.log(person.name); // moon jong min

const person: IPerson = new Person('Mark', 35);
person.getName();

// interface를 활용 하면 이런식으로도 사용 가능함
```

## class의 static 프로퍼티, 메서드
```javascript
class Person {
    public static HEIGHT: number;

    public static Talk(): void {
        console.log('안녕하세요');
    }
}

const person: Person = new Person();
person.HEIGHT // 접근안됨

Person.HEIGHT // 접근됨 (클래스 자체에 프로퍼티가 동적으로 생성됨)
Person.Talk(); // 동일함
```

- 동적으로 생성된다는 얘기에 좀 집중을 해봐야 할것 같은데 변화도 가능하다는 점이다.
- 리엑트할 때도 사용되는 default props 같은 경우에 사용됨
- 역시 static을 너무 사용하면 좋지 않음
- public static은 의미가 있음
- private static의 의미는 고민이 필요함


## Anstract Class - 미완된 클래스
```javascript 
abstract class APerson {
    protected _name: string = 'Mark';
    abstract setName(name: string): void;
    // 이렇게 미완성으로 만들어 놓고 상속받거나 할때 사용 가능함
}
```

## class와 private constructor
```javascript
// 싱글톤 예제
class Perference {
    private static Instance: Perference = null;
    public static getInstance(): Perference {
        if(Perference.Instance === null){
            Preference.Instance = new Preference();
        }

        return Preference.Instance;
    }
    private constructor() {
        
    }

    hello() {

    }
}

const p = Perference.getInstance();
p.hello();
```

## class와 readonly
```javascript
class Person {
    private readonly _name: string = null;
}
```

- readonly는 get, set중에 get만 있는것과 흡사하다.


# 8. generic
- any -> generic
- 제네릭을 쓰는 가장 큰 이유는 템플릿 라이브러리 (cpp)처럼 타입을 변수로 주고 싶을때 사용함

```javascript
function hello<T>(message: T): T {
    return message;
}

hello<string>('hello moon');
hello<string>('hello moon').length;//문자열의 내장 함수도 사용가능
hello<number>(35);

const a: string[] = [];
const b: Array<string> = [];
```
- 메시지가 number, string에 상관없이 가능함
- 장점은 any로 사용하면 헬퍼같은게 제대로 작동이 되지 않는데 제네릭은 정상 작동함

## generic 인자
```javascript
function hello<T>(message: T[]): T{
    return message[0]
}
```
- T의 array 형태로도 사용할 수 있다.

## generic class
```javascript
class Person<T> {
    private _name: T;
    
    constructor(name: T) {
        this._name = name;
    }
}

const mark = new Person('Mark');
new Person<number>('Mark'); //error!
```
- name의 타입이 설정하는 대로 되어줌

## generic with extends
```javascript
class Person<T extends string | number> {
    private _name: T;

    constructor(name: T) {
        this._name = name;
    }
}

const mark = new Person('mark');
```

## generic with multiple type
```javascript
class Person<T, K> {
    private _name: T;
    private _age: K;

    constructor(name: T, age: K) {
        this._name = name;
        this._age = age;
    }
}

const mark = new Person('mark', 35);
```

## type lookup system
- 2.1 버전에 나옴
```javascript
interface Person {
    name: string;
    age: number;
}

// type Test = keyof Person;

// function getProperty(obj, key) {
//     return obj[key]; //가끔이 key가 없을땐 undefined 에러를 뿜는데 (나도 겪음) 이걸 해결하는데 lookup system
// }

function getProperty<T, K extends keyof T>(obj: T, key: K): T[K]{
    return obj[key];
}

function setProperty<T, K extends keyof T>(obj: T, key: K, value: T[K]): T[K]{
    obj[key] = value
}

const person: Person = {
    name: 'Mark',
    age: 35
}

getProperty(person, 'name');
setProperty(person, 'name', 'anda');
```

- 상당히 자주 쓰일것 같음 
- // type Test = keyof Person; 이 부분이 좀 중요한것 같은데 keyof Person을 해줬기 때문에 Test는 리터럴로 name, age 프로퍼티를 갖게 되는것


# 9. iterator

## for...of
- es3
  - for (var i=...)
- es5
  - array.forEach
    - break 를 할 수 없었따.
- es6
  - for of
    - 원칙적으로는 배열에서만 사용 가능

## for...in
- 배열을 순회할 때는 사용하지 말것
  - index가 number가 아니라 string으로 나온다.
  - 배열의 프로퍼티를 순회할 수도 있따.
  - prototype 체인의 프로퍼티를 순회할 수도 있다.
  - 루프가 무작위로 수회할 수도 있다.
  - for of를 쓸 것
- 객체를 순회할 때
  - for(const prop of Object.keys(obj))도 사용할 수 있음

## target es3 forEach
- 트렌스파일시에 es3인데도 lib에서 잘못 판단되어서 적용이 안되고 es5 기준으로 생성됨

## Sysmbol.iterator
- 프로퍼티이며, 함수가 구현되어있으면, iterable 이라고 한다.
- Array, Map, Set, String, Int32Array, Unit32Array, etc, 에는 내장된 구현체가 있으므로 이터러블 하다.
- 그냥 객체는 이터러블하지 않다.
- 이터레이터를 통해 이터러블한 객체의 Symbol.iterator함수를 호출한다.
- traget: es3 or es5
  - Array 에만 for..of사용 가능
  - 일반 객체에 사용하면 오류
- target: es6
  - Symbol.iterator를 구현하면 사용 가능

## custom iterable
```javascript
class CustomIterable implements Iterable<string> {
    private _array: Array<string> = ['first', 'second'];

    [Symbol.iterator]() {
        var nextIndex = 0;

        return {
            next: () => {
                return {
                    value: this._array[nextIndex++],
                    done: nextIndex > this._array.length
                }
            }
        }
    }
}

const cIterable = new CustomIterable();

for (const item of cIterable) {
    console.log(item);
}
```
- 배열의 이터레이터를 돌면 예 for of 객체의 for을 돌리면 커스텀한 for of 로 돌리면 class 내부에 있는 배열도 사용 가능하기에 사용함.
- 사실 무슨 말 인지..


# 10. Decorator
- Class
- Method
- Property
- Parameter

- 모든 decorator 는 function이다


## class decorator
```javascript
function hello(constructorFn: Function) {
    console.log(constructorFn);
}

function helloFactory(show: boolean) {
    if (show)
      return hello;
    else
      return null;
}

@helloFactory(false)
class Person {

}
```
## class decorator expert
```javascript
function hello(constructorFn: Function) {
    constructorFn.prototype.hello = function() :void {
        console.log('hello');
    }
}

@hello
class Person {

}

const p = new Person();
(<any>p).hello(); // 이런식으로 밖에 사용해야함

```

## method decorator

```javascript
function editable(canBeEditable: boolean) {
    return function(target: any, propName: string, description: PropertyDescriptor) {
        console.log(target);
        console.log(propName);
        console.log(description);

        description.writable = canBeEditable;
    }
}

class Person {

    constructor() {
        console.log('new Person ()');
    }

    @editable(false)
    hello(): void {
        console.log('hello');
    }

}

const p = new Person();
p.hello();

p.hello = function() {
    console.log('world');
}
p.hello();

```


## property decorator

```javascript
function writetable(canBeWriteable: boolean) {
    return function(target: any, propName: string): any {
        console.log(target);
        console.log(propName);

        return {
            writetable: canBeWriteable
        }
    }
}


class Person {

    @writetable(true)
    name: string = 'Mark';

    constructor() {
        console.log('new Person ()');
    }

    hello(): void {
        console.log('hello');
    }

}

const p = new Person();
console.log(p.name);
```

## parameter decorator
```javascript
function printInfo(target: any, methodName: string, paramIndex: number) {
    console.log(target);
    console.log(methodName);
    console.log(paramIndex);

}

class Person {
    private _name: string;
    private _age: number;

    constructor(name: string, @printInfo age: number) {
        this._name = name;
        this._age = age;
    }

    hello(@printInfo message: string): void {
        console.log(message)
    }

}


// const p = new Person('Mark', 35);
```

- 개인적으로 decorator는 예를들면 프레임워크를 만들때나 어떠한 모듈을 만들때 변수 검증 등을 하는데 사용하면 요긴하게 쓰일것 같다는 생각이 들었다.


# 11. Type Inference
## 타입 추론
- 기본적으로 타입을 명시적으로 스지 않을 때 추론하는 방법에 대한 규칙
  - 명시적으로 쓰는 것은 타입 추론이 아니라 코드를 읽기 좋게 하는 지름길
- let은 기본적으로 우리가아는 기본 자료형으로 추론
- const는 리터럴 타입으로 추론
  - 오브젝트 타입을 쓰지 않으면, 프로퍼티는 let 처럼 추론
    - const person = {name: 'Mark', age: 35}
    - person => {name:string; age: number}
- 대부분 추론은 쉽다.
  - 단순 변수
  - structing, destruction
- array, 함수의 리턴에서는 워하는데로 얻기가 힘들다.

## 배열 타입 추론

```javascript
const aaray1 = []; // any type으로 추론함
const array2 = ['a', 'b'] // array string
const array3 = ['a', 1, 'cone'] // union type으로 추론함

class Animal {
    name: string;
}

class Dog extends Aniaml {
    dog: string;
}

class Cat extends Animal {
    cat: string;
}

const array4 = [new Dog(), new Cat()]; // union dog | cat
```

## 리턴 타입 추론
```javascript
function hello(message: string | number) { 
    // 리터럴 타입의 world이거나 0을 추론
    if(message === 'world')
      return 'world'
    else
      return 0
}
```
## 유니온 타입과 가드
```javascript
interface Person {
    name: string;
    age: number;
}

interface Car {
    brand: string;
    wheel: number;
}

function isPerson(arg: any): arg is Person {
    return arg.name !== undefined;
} // 이 부분이 타입가드

function hello(obj: Person | Car) {
    if (isPerson(obj)) {
        obj.age;
  }
}
```


## 마치며
약 11개의 챕터이자 강좌는 14개인 타입스크립트 코리아에서 만든 이 강좌는 [유튜브](https://www.youtube.com/watch?v=PFBRhxjIBUM&list=PLV6pYUAZ-ZoHx0OjUduzaFSZ4_cUqXLm0)에서 확인하실 수 있습니다.

타입스크립트를 막연하게 어렵다고만 생각했었는데 오히려 프로그램을 작성하는데 있어서 더욱더 안정성이 있다는것은 이 강좌를 통해서 확실히 알게되었다.

실제로 직접 가서 참여한 세미나보다도 상당히 훌륭했고 예제들 역시 상당히 훌륭했다.



