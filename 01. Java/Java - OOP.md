# Java - OOP (24. 01 .16 ~ 17)

## 객체 지향 언어의 특징

### Abstraction (추상화)

- 현실의 객체를 추상화 → 하나의 클래스를 구성
- 클래스는 구체화 되어서 객체가 된다.

### Polymorphism (다형성)

- 하나의 객체는 여러가지 type으로 참조 할 수 있다.

### Inheritance (상속)

- 부모 클래스를 자식이 정의함으로써 코드의 재사용을 가능하게 한다.
    - 부모의 모든 멤버가 자동으로 상속되지만 `private` 변수는 상속되지 않는다.
    - 부모의 생성자는 자식의 생성자에서 명시적으로 지정 가능
    - 부모 클래스에서 기본 생성자가 명시적으로 지정 해야한다.
    - 자식 클래스에서 `super()` 로 부모 생성자를 지칭하는 변수

### Encapsulation (데이터 은닉과 보호)

- 객체의 데이터를 외부에 직접 노출시키지 않고 메서드를 이용해 보호 한다.
    - `private` 를 사용
    - `public setter()` 메서드
    - `public getter()` 메서드
    - `private isValidate()` 메서드

## Class vs Object

### 클래스

- 객체를 정의해놓은 것

### 객체

- 클래스를 데이터 타입으로 변환해 실제 동작하는것
- JVM의 **heap** 영역에 저장된다. → 사라질댄 G.C에 의해 정리됨
- 객체의 변수들은 **stack** 영역에 저장된다.

## 변수

### 인스턴스 변수

- 클래스 영역에 선언
- 객체가 만들어질 때 heap에 객체 별로 생성됨
- Garbage Collector에 의해 객체가 없어질 때 소멸됨 (프로그래머가 명시적 소멸x)

### 클래스 변수

- 클래스 영역 안에 `static` 키워드를 붙이며 생성
- 클래스가 로딩 될 때 heap에 클래스 별로 생성 → 클래스 이름으로 접근
    - 객체 이름으로도 접근은 가능하나 waring 알림이 뜸

### 지역 변수 & 파라미터 변수

- 클래스의 `{}` 이 아닌 중괄호 안에 생성된 변수 (메소드 안)
- 선언된 라인이 실행 될 때, Stack 영역 안에 생성됨
- 명시적 초기화가 필요
- 외부에서는 접근이 불가능 하기에 소속이 불필요
    - 내부에서는 이름으로 바로 접근 가능
- `{ }` 을 벗어날 때 메모리에서 없어진다.

## 메서드

- 현실의 객체가 하는 동작을 프로그래밍 화

### 선언부

- 어떤 타입을 return 할지 형을 명시적 표현
- return 을 받을땐 묵시적 형변환 적용
- 호출시 넘겨줘야할 변수 → 파라미터
    - 파라미터도 전달시 묵시적 형변환 적용

**가변인자 Variable argument**

- 메서드 선언이 동일 타입의 인자가 몇개 들어올지 예상할 수 없을 경우
- 배열 타입도 가능하지만 호출 전 배열 선언에 번거러움
- `...` 을 이용해 파라미터를 선언하면 값을 개수에 따른 자동 배열 생성 및 초기화
    
    ```jsx
    public class VariableArgsTest {
        public static void main(String[] args) {
            VariableArgsTest vt = new VariableArgsTest();
            vt.variableArgs(1, 2, 3);
            vt.variableArgs(1, 2, 3, 4, 5);
            vt.variableArgs(1, 2);
        }
    
        public void variableArgs(int... params) {
            int sum = 0;
            for (int i : params) {
                sum += i;
            }
            System.out.println(sum);
        }
    
    }
    ```
    

### 구현부

- 중괄호안에 처리한는 내용 → 비즈니스 로직
- 값 반환시에는 묵시적 형변환
- 변수와 마찬가지로 *static* 과 *non-static* 상태를 구분해서 호출

## 메서드 호출 스택

### 메서드 호출 스택

- stack 구조
- 각각의 메서드 호출시 메서드 동작을 위한 메모리 상자를 하나씩 할당
    - 상자 내부에는 메서드를 위한 변수 등 로컬 변수 구성
- A 메서드 → B 메서드 호출시 새로운 상자 쌓기
    - 위에 있는 B 만 활성화
    - A 메서드 스택은 정지 상태
    - B 메서드가 리턴 되고 메모리 반납 되면 A가 최상위가 됨 → 재 활성화

 

## 기본형 변수 vs 참조형 변수

- 메서드 호출시 파라미터는 **복사** 되서 전달된다.
    - *Call by Value*
- 객체를 파라미터로 전달 할 때는 객체가 가리키는 **주소**를 전달한다.
    - 즉 파라미터의 멤버 변수를 수정한다면 원본도 수정된다!!!

## 메서드 오버로딩

- 동일한 기능을 수행하는 메서드의 추가 작성
- 동일한 기능을 여러 형태로 작성할 경우에 사용
- 기억해야할 메서드가 감소하고 중복 코드에 대한 효율적 관리 가능

## 메소드 오버라이딩

- 메서드 이름은 같아야한다.
- 매개변수의 개수, 타입, 순서가 같아야한다.
- 리턴 타입이 같아야한다.
- 접근 제한자는 부모보다 범위가 넓거나 같아야한다.
- 조상보다 더 큰 예외를 던질 수 없다.

## 상속

- 상위 클래스의 자산을 하위 클래스에서 재사용 하기 위한것
- 코드의 재사용성 증가 → 유지 보수성 향상
- 자바의 상속은 단일 상속이다.

## 바인딩

### 정적 바인딩

- 컴파일 시간에 참조 변수의 타입에 따라 연결이 달라진다.
- 상속관계에 있어 객체의 멤버 변수가 중복 될 때 또는 static method

### 동적 바인딩

- 다형성을 이용해서 런타임 시간에 메모리의 실체 객체 타입으로 결정
- 상속관계에 있어 객체의 instance method가 재정의 되었을 때 마지막에 재정의된 자식클래스의 메서드가 호출됨

---

---

# JAVADOC 작성법

```jsx
/**
 * javadoc 입니다.
 * <pre> 
 * 		html 태그가 사용이 가능하고요 
 * 		줄넘기기도 편하죠 
 * </pre>
 * 
 * <h2> 어노테이션 목록입니다. </h2>
 * @author 작성자 이름입니다.
 * @version 버전 정보 입니다.
 * @see 관련 api 정보 입니다.
 * @since JDK 버전 정보입니다.
 * @param 매개변수 설명입니다.
 * @return 리턴 값을 설명합니다.
 */
```