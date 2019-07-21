---
layout: post
title:  "Checked / Unchecked Exception"
date:   2019-07-21 11:24:10 +0900
categories: #java 
---
# Checked Exception
간단히 요약하면 try~catch~finally의 구문이 "반드시" 들어가야 하는 종류의 Exception. 

메소드 구현 히 메소드 옆에 throws {Exception 종류}를 붙임

메소드 샌드박스 개념이라고 볼 수 있으며, 구현된 메소드 전체를 한 트랜잭션단위로 볼 때 사용하면 좋을 것.

### 사용상 주의점  
Checked exception이 선언된 메소드의 전후에 실행되는 구문은 정상적으로 실행됨
~~~java
String s;
void parseAndSet(String filePath) {}
    try {
        s = Parser.parse(filePath);
    } catch(IOException e) {
        //~~
    }
    set(s);
}
~~~
위 패턴은 가능한 한 구성하지 말아야 할 패턴이다. try에서 파싱이 실패했을 때 catch문에서 탈출했다 할 지라도 set(s) 구문이 실행되어 결국은 NPE가 발생될 가능성이 잠재적으로 큰 코드이다.
보다 안전한 구성을 위해서 set(s)도 try/catch문에 반드시 넣어주어야 할 것이다.  
아주 다행인 것은 저러한 패턴이 나올 때 Java는 일반적으로 컴파일이 되지 않는데, 그것은 try 내부 블록의 String이 final or Effectively final 을 요구하기 때문이다.  
그러나 이 또한 코드와 같이 메소드 밖 Class 인스턴스 변수로 선언하게 되면 문제없이 컴파일이 될 수 있으니 주의해야 한다.   
또한 위의 패턴이 강제되기 때문에 SRP의 위반을 동반할 수 밖에 없다.

catch문에 return을 call한다거나 하는 방법을 사용할 수도 있겠지만, 그럴바에는 아래의 방법으로 탈출시키는게 나을 수 있다.

# Unchecked Exception

### ex

~~~java
void parseAndSet(String str) {
    set(parse(str));
}

String parse(String str) {
    if(isgoodForm(str)) {
        return str.dosth();
    } else {
        throw new BadFormException();
    }
}
~~~

코드의 깔끔함을 차치하더라도, 위의 구문에서 set과 parse가 나뉘어있다고 하더라도, 위와같은 메소드를 구성하는게 이러한 패턴에서는 훨씬 안전 할 수있다.

throw(Unchecked Exception)의 특징은 본인 객체에서만의 탈출이 아닌 해당 메소드를 사용하고있는 최상위 메소드까지의 탈출이 이루어진다.  

# Summery 

Clean Code 책에서는 위와같은 Checked Exception을 줄이고 Unchecked Exception을 적극 이용하라는 이야기가 나와있다.  
올바른 사용법을 준수해도 SRP의 위반이 있을 것이고 그렇지 않을 경우 Unchecked Exception을 부르는 대 참사가 생길 수 있을 것이다. 

다만 Checked Exception을 사용해야만 하는 경우가 있다. API 설계단계에서 Interface method 혹은 abstract method를 선언했고, (그리고 그것을 API설계자 본인이 작성하지 않는 경우) 해당 method가 잠재적으로 Checked Exception이 요구될 때에는 충분히 유용하게 사용될 수 있으리라 여겨진다.  
다만 이 때에는 SRP를 가능한 위반하지 않을 정도로 작은 범위내에서 선언해야 한다. 또한 특정 범위 이상의 메소드에 까지 throws의 책임을 넘겨서는 안 된다.