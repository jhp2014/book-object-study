
###### 1) 잘못된 설계
Theater 클래스가 거의 모든 클래스 **의존**
+ 의존클래스 변경 → Theater 클래스 변경가능성 ↑
+ 다른 클래스의 너무 많은 정보를 알아야 한다.

*ref)*
[[오브젝트01-03.pdf#page=39]]
[[오브젝트01-03.pdf#page=43]]


###### 2) 설계 개선
 객체의 자율성 향상

###### 2.1) ticketSeller 자율성 향상
**Theater의 enter Method 개선 전**
```
    public void enter(Audience audience) {
        if (audience.getBag().hasInvitation()) {
            Ticket ticket = ticketSeller.getTicketOffice().getTicket();
            audience.getBag().setTicket(ticket);
        } else {
            Ticket ticket = ticketSeller.getTicketOffice().getTicket();
            audience.getBag().minusAmount(ticket.getFee());
            ticketSeller.getTicketOffice().plusAmount(ticket.getFee());
            audience.getBag().setTicket(ticket);
        }
    }
```
**Theater의 enter Method 개선 후**
+ ticketSeller 자율성 부여
```
    public void enter(Audience audience) {
        ticketSeller.sellTo(audience);
    }
```
+ Audience 자율성 부여
```
public class TicketSeller {
    public void sellTo(Audience audience) {
        ticketOffice.plusAmount(audience.buy(ticketOffice.getTicket()));
    }
}
```

*ref)*
[[오브젝트01-03.pdf#page=50]]


###### 3) 절차지향 & 객체지향

###### 3.1) 절차 지향
**프로세스(Process)**
Theater의 enter Method  

**데이터(Data)**
Audience, Ticketseller, Bag, Ticketoffice

**단점**
프로세스가 모든 데이터에 의존하므로, 데이터가 변경되면 프로세스는 반드시 변경된다.

###### 3.2) 객체 지향
데이터와 프로세스가 동일한 모듈 내부에 위치

**객체 지향 설계 핵심**
적절한 객체에 적절한 책임을 할당 → 의존성 관리 → 결합도↓

**트레이드 오프**
객체에 자율성을 부여 → 결합도 증가
> 자율성이 없으면, 알아서 파라미터에 값이 들어온다.
> 하지만 자율성이 부여되면, 협력에 필요한 객체를 알아야 하므로 결합도가 증가한다.

*ref)*
+ 객체지향
	+ [[오브젝트01-03.pdf#page=54]]
+ 트레이드 오프
	+  [[오브젝트01-03.pdf#page=59]]
	+ [[오브젝트01-03.pdf#page=43|자율성 부여 전]] & [[오브젝트01-03.pdf#page=50|자율성 부여 후]]

> ##*내 생각*
> 객체의 자율성이 생긴다는 것은 책임이 생긴다는 것과 같은 말인 것 같다.
> 따라서, 자율성을 생각할 때 고려할 Trade-off는
> **객체가 이 책임을 가지는 것이 맞는지 판단해야 한다.** 

