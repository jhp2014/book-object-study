
###### 1) 메시지와 인터페이스
![[메세지 전송 표기법.png]]

*ref.*
메시지 → [[오브젝트04-08.pdf#page=82]]
용어정리 → [[오브젝트04-08.pdf#page=85]]


###### 2) 오퍼레이션 이름 짖는 방법

+ 협력 이라는 문맥을 반영해야 한다
+ 클라이언트가 객체에게 무엇을 원하는지 표현

*ref.*
[[오브젝트04-08.pdf#page=101]]

###### 3) 원칙의 함정

**캡슐화 이전**
+ screening에게 할인 조건의 날짜가 맞는지 **시키지** 않고, Screening에게 정보를 **묻고** 있다.
```
public class PeriodCondition implements DiscountCondition {
    private DayOfWeek dayOfWeek;
    private LocalTime startTime;
    private LocalTime endTime;

    public boolean isSatisfiedBy(Screening screening) {
        return dayOfWeek.equals(screening.getWhenScreened().getDayOfWeek()) &&
                startTime.compareTo(screening.getWhenScreened().toLocalTime()) <= 0 &&
                endTime.compareTo(screening.getWhenScreened().toLocalTime()) >= 0;
    }
}
```

**캡슐화 이후**
+ screening에게 할인 기간이 맞는지 계산을 시킨다.
```
public class Screening {
    private Movie movie;
    private int sequence;
    private LocalDateTime whenScreened;

    public boolean isDiscountable(DayOfWeek dayOfWeek, LocalTime startTime, LocalTime endTime) 
    {
	return 검증 로직 결과
    }
}
```

```
public class PeriodCondition implements DiscountCondition {
    private DayOfWeek dayOfWeek;
    private LocalTime startTime;
    private LocalTime endTime;

    public boolean isSatisfiedBy(Screening screening) {
    return screening.isDiscountable(dayOfWeek, startTime, endTime)
    }
}
```


**문제점**
+ `Screening` 이 기간에 따른 할인 조건을 판단하는 책임을 떠안게 된다.
+ 이것은 `Screening` 의 본질적인 책임이 아니다.
+ `Screening` 이 `PeriodCondition`의 인스턴스 변수의 변경에 영향을 받게 된다.

**해결**
+ 캡슐화 하향 하지만,
  → 응집도 향상
  → `Screening` ↔ `PeriodCondition` 결합도 하향


>##*내 생각*
>캡슐화의 Trade - Off
>→ 객체의 자율성이 부여 된다. 이는 객체가 책임을 지는 것이다.
>따라서, 이 객체가 이 책임을 지는 것이 맞는지 판단해야 한다.
>
>또한, 묻는 객체가 정말 "*객체*" 인지 "*데이터*" 인지 판단해야한다.

*ref.*
[[오브젝트04-08.pdf#page=104]]




###### 4) 명령 - 쿼리 분리 원칙

**용어 정리**
+ 프로시저 ( 명령 ) → 부수 효과 O 
+ 함수 ( 쿼리 ) → 부수 효과 X 

**장점**
+ 코드는 예측 가능하고 이해하기 쉽다.
+ 디버깅이 용이하고, 유지보수가 쉽다.

>##*내 생각*
>함수는 하나의 동작만 수행하는 것이 맞다.
>하지만, 명령과 쿼리를 합쳐 놓으면 함수가 자연스럽게 2가지 동작을 수행하게 되는데, 이로 인해 디버깅이 어려워 지는 것 같다.
>
>따라서, Command - Query 분리 외에도 함수는 하나의 동작만 수행 하도록 작성하자.

*ref.*
[[오브젝트04-08.pdf#page=104]]