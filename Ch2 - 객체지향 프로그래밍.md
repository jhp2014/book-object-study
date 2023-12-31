
##### 1) 요구사항

+ 영화
+ 상영
+ 할인 정책
	+ 할인 조건
		+ 순번 조건
		+ 기간 조건
	+ 할인 정책
		+ 금액 할인
		+ 비율 할인

*ref.*
[[오브젝트01-03.pdf#page=64]]

##### 2) 협력→객체→클래스

협력의 관점 → 객체 결정 → 객체 행위 & 상태 (Class 작성)
+ 클래스 고민 전, 어떤 객체가 필요한지 결정
+ 협력 속에서 객체를 찾아야 한다.

###### 2.1)객체
캡슐화 ↔ 자율성 
+ 접근 제어 :: 외부에서 간섭 불가

###### 2.2) 협력
**메세지**
다른 객체와 유일한 상호작용 방법
**메소드**
메세지 처리에 대한 행동

*ref.*
[[오브젝트01-03.pdf#page=75]]

###### 2.2.1) 상속
**구현 상속(implementation inheritance)**
+ 올바르지 못한 상속 방법이다.
+ 코드 재 사용을 위한 상속
	+ 이 경우 **합성** 사용 권장

**인터페이스 상속(interface inheritance)**
+ 부모의 메세지를 모두 처리할 수 있게 된다. 
+ 즉, 같은 타입이다.

*ref.*
[[오브젝트01-03.pdf#page=90]]


**추상클래스 & 인터페이스 트레이드 오프**
+ 추상 클래스는 구현까지 재 사용 가능하지만,
+ 구현이 필요 없는 경우에도 재 사용 된다.

*ref.*
[[오브젝트01-03.pdf#page=94]]


**단점**
1) 부모 클래스의 내부 구조를 잘 알아야 한다.
```
# 추상 클래스
public abstract class super {
	public void template() {
		inner()
	}

	public abstract inner() {
		
	}
} 
## inner를 구현하는 자식 클래스들은 inner가 상위 클래스에서 어떻게 사용되는지 알고있어야 한다.
```

2) 유연하지 못하다. 즉, 컴파일 타임에 강하게 결합된다.

**해결**
+ 코드 재 사용을 위해서는 상속 보다는 합성을 사용하자
+ 인터페이스 사용을 위해서는 상속 OK

*ref.*
[[오브젝트01-03.pdf#page=96]]




