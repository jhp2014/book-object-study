###### 1) OCP(Open-Closed Principle)

**핵심**
+ 컴파일타임 의존성 고정 하고, 런타임 의존성을 변경 하라
+ 즉, 추상화에 의존해야 한다.


###### 1.1) 생성과 사용의 분리

**이유**
추상화에 의존하기 위해서는
→ 객체를 생성하면 안된다.

  > ##*객체 생성을 하면 안되는 이유*
  > + 추상화가 아닌 구체 타입에 의존하도록 한다.
  > + 객체 생성하기 위해서는 객체의 인자까지 알아야 하므로, 강하게 결합된다.
  >
  >**따라서, 추상화에 의존하기 위해 객체를 생성하면 안된다.**


*ref.*
[[오브젝트08-11_OCR.pdf#page=35]]


###### 1.2) 객체 생성 위치

클라이언트에서 객체 생성 및 의존성 주입

**FACTORY 객체 사용**
+ 객체 생성에 특화된 객체
![[Factory사용 후 의존성.png]]

```
import org.eternity.money.Money;
import org.eternity.movie.step01.Movie;

public class Client {
    private Factory factory;

    public Client(Factory factory) {
        this.factory = factory;
    }

    public Money getAvatarFee() {
        Movie avatar = factory.createAvatarMovie();
        return avatar.getFee();
    }
}
```
>##*문제점 - 내 생각*
>Client가 Movie에 의존한다는 것이 내부에 숨겨져 있다.
>
>하지만, 의존성 주입을 지원하는 프레임워크를 사용하지 못하는 경우 어쩔 수 없다.

*ref.*
Factory 객체 :: [[오브젝트08-11_OCR.pdf#page=38]]


###### 1.3) DIP (Dependency Inversion Principle)

**의존성 역전 원칙**
+ 상위 수준의 모듈은 하위 수준의 모듈에 의존해서는 안 된다. 
  → 둘 모두 추상화에 의존해야 한다.
+ 추상화는 구체적인 사항에 의존해서는 안 된다. 
  → 구체적인 사항은 추상화에 의존해야 한다.

**의존성 역전 원칙과 패키지**

![[전통적인 모듈 구조.png]]
![[객체지향적인 모듈 구조.png]]

*ref.*
[[오브젝트08-11_OCR.pdf#page=50]]
