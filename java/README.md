# Java

### 간단한 자바의 개요:
자바의 아버지 James Gosling, Mike Sheridan, 그리고 Patrick Naughton은 1991년 자바 프로젝트를 시작했다. 처음 이 언어는 제임스의 오피스 밖에 있는 Oak Tree를 보고 Oak로 정했으나 그 후로 Green을 거쳐 인도네시아산 커피 Java로 부르게 되었다.

1996년 Sun Microsystems를 통해 Java 1.0이 릴리즈 되었고 Java Virtual Machine (JVM)을 통해 동일한 자바 코드가 운영체제나 하드웨어의 제한 없이 실행될 수 있도록 Write Once, Run Anywhere (WORA)를 약속했다.

### 자바의 특징:  
1. 운영체제에 독립적이다.  
    - 자바 프로그램은 JVM 상에서 실행되기 때문에 운영체제에 대한 제약이 없다.
2. 객체지향 언어다.
    - 흔히 비교되는 절차적 프로그래밍 보다 실행하기 더 쉽고 빠르다.
    - 객체지향은 프로그램의 명확한 구조를 볼 수 있다.
    - 'Don't Repeat Yourself' DRY 원칙을 지키는데 용이하고, 유지보수 하기 쉽다.
    - 재사용 가능한 프로그램을 만드는데 비교적 적은 비용이 든다.
3. 오픈소스가 존재하고 많은 Java 개발자들이 많은 분야 관련 좋은 라이브러리를 공유하고 있다.
4. 자동으로 메모리 관리를 한다.
    - Garbage Collector, JVM내 Heap 메모리 영역 내 사용되지 않는 오브젝트에 대한 메모리 자원을 청소한다.
5. 멀티쓰레드를 더 쉽게 구현할 수 있다.
    - 쓰레드 생성 및 관리에 대한 라이브러리를 제공 하고 있다.

### Java Virtual Machine, aka 'JVM':
자바 가상 머신. 역할은 크게 3가지로 분류된다.
1. 자바와 운영체제 사이 중개자 역할을 한다.
2. 자바 어플리케이션을 Class Loader를 통해 읽고 자바 API들과 함께 실행시킨다.
3. Heap 영역의 메모리 관리를 한다 (Garbage Collector)  

#### 자바 프로그램의 실행 프로세스:
<img src="https://pediaa.com/wp-content/uploads/2018/11/Difference-Between-Interpreter-and-JIT-Compiler_Figure-2.jpg" />
    
1. 소스 파일들을 Java Compiler가 bytecode(.class)로 컴파일 한다. 
2. JVM에서 Class Loader를 사용해 필요한 클래스 파일을 runtime에 동적으로 load한다
3. 실행 엔진(Execution Engine)이 필요한 bytecode를 실행 가능하도록 추가 작업을 진행 한다.
    - Interpreter, 인터프리터는 bytecode를 명령어 단위로 읽어서 실행 한다. 단점은 한줄씩 실행하기에 느리다.
    - Just In Time Compiler (JIT), JVM은 어떠한 코드 블럭이 자주 실행 되는지 모니터링을 해서 대상이 되는 메소드나
    메소드의 부분, 그리고 루프등을 JIT Compiler를 통해 native machine code로 컴파일 한다.
    - 한 어플리케이션 안에서 어느 부분은 interpreter로, 어느 부분은 native machine code로 컴파일 되어서 실행 되는 경우가 발생한다는 말이다.
    - 운영체제에 따른 JVM 설치 및 실행으로 동일한 코드를 각 운영체제의 native machine code로 실행하게 된다. 이를 통해 운영체제에 대한 제약이 없고, Write Once Run Everywhere (WORE)가 보장된다.
     
#### JVM 아키텍쳐:
<img src="https://www.guru99.com/images/1/2.png" width="600"/>

1. Class Loader:
    - 클래스 파일을 읽는 기능을 한다.
2. Method Area:
    - 클래스 정보, 메소드 정보 등의 메타 데이터, Runtime Constant Pool(상수 자료형 등), static 변수 등이 생성되는 영역
    - 하나의 프로세스 내 모든 쓰레드들이 공유하는 영역 
3. Heap:
    - 프로그램 내 객체들이 저장되는 곳. 코드 상 new 키워드를 사용해 생성되는 객체들을 담는 곳.
    - Garbage Collector로 메모리가 관리 된다.
    - 모든 쓰레드들이 공유하는 영역
4. JVM Language Stacks:
    - 지역 변수나 임시 값들이 생성되는 영역이다.
    - 각각의 쓰레드가 생성 될 때 해당 쓰레드 만의 JVM stack이 생성된다.
    - 하나의 메소드가 실행될 때 그 메소드 실행을 위한 새로운 frame이 생성된다. frame은 메소드 실행이 완료될 때 삭제된다.
5. PC Registers:
    - 쓰레드가 생성될 때 마다 생성되는 영약이다.
    - 해당 쓰레드가 실행되는 JVM 명령 부분의 주소를 가지고 있다.
6. Native Method Stacks:
    - 자바가 아닌 다른 언어로 쓰여진 native code 명령을 가지고 있다.


#### Garbage Collection:
Garbage Collector를 통해 Heap Memory 영역 내 객체들 중 사용되는 객체, 사용되지 않는 객체를 분류하고 사용되지 않는 객체들을 지워 메모리 공간을 확보하는 작업이다.

<img src="https://miro.medium.com/max/700/0*zQNh1EUPEuDBQ7NZ.png" width="500" height="300" />

- Marking Process:
    - 이 과정에서 Garbage Collector는 모든 객체들을 스캔해 사용되고 있는지 더이상 사용되지 않는지 구분한다.

<img src="https://miro.medium.com/max/700/0*n8c2TYVvPIWoflDi.png" width="500" height="300" />

- Deletion without Compacting:
    - 사용되지 않는 객체들을 삭제해 메모리 공간을 확보한다.
    - Memory Allocator가 사용 가능해진 메모리 공간을 참조해 새로운 객체에 할당한다.

<img src="https://miro.medium.com/max/700/0*dv5yt9m6hJcJIt8Z.png" width="500" height="300" />

- Deletion with Compacting:
    - 사용되지 않는 객체들을 삭제하고 남은 객체들을 이동시켜 객체간 메모리 사이 빈 공간들을 채운다.
    - Memory Allocator가 확보한 공간의 시작점을 참조하기 때문에 새로운 객체에 할당하는 작업이 빠르다.

### Object Oriented Programming (OOP)
객체 지향 프로그래밍 이란:
1. 실세상의 물체를 클래스와 객체를 사용해 표현하고 객체간의 관계와 상호 작용을 프로그램으로 디자인 하는 방법론.
2. 객체를 정의하고, 객체간 상호작용에 필요한 변수나 함수들을 구현한다.
3. 사람의 사고와 가장 비슷하게 프로그램을 만드려는 방법론.

#### 클래스, 객체, 인스턴스

1. 클래스 (class):
    - 객체를 생성하기 위한 도면(blueprint).
    - 객체의 구조, 속성, 행동들을 정의한다.
2. 객체 (Object):
    - 클래스로 생성된 실체.
    - 객체는 클래스의 인스턴스다.
    - 하나의 클래스로 여러개의 객체를 생성할 수 있다.
3. 인스턴스 (Instance):
    - 어떤 실체를 뜻하지 않고, 관계를 말할때 사용된다.

#### 객체 지향의 특징:

1. 추상화:
    - 오직 필요한 속성만 보여주고 불필요한 정보들은 숨기는것.
    - 객체와 관련된 디테일만 보여줌으로써 프로그램 복잡도를 줄일수 있다.
2. 캡슐화:
    - 클래스의 데이터와 메소드를 하나의 단위로 묶는 메커니즘.
    - 다른 클래스로 부터의 데이터 접근을 막는다. 
    - 구현 디테일을 외부로 노출시키지 않는다.
3. 상속:
    - 클래스가 다른 클래스의 구성 요소(fields and methods)들을 상속 받을수 있다는 메커니즘.
    - Superclass(parent, 부모)클래스는 상속하는 클래스
    - Subclass(child, 자식)클래스는 상속받는 클래스
4. 다형성:
    - 다양한 형태를 가진다는 의미.
    - 하나의 액션을 다른 방법들로 구현 하는것.
    - Overriding과 Overloading이 대표적임.
        - Overriding, 클래스 상속과 부모 클래스 메소드 재정의 및 인터페이스에 정의된 메소드 구현.
        - Overloading, 동일한 이름의 메소드가 파라미터(타입이나 개수)에 따라 다르게 동작하도록 구현.

#### References:
1. https://www.viralpatel.net/java-virtual-machine-an-inside-story
2. https://www.guru99.com/java-virtual-machine-jvm.html
3. https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html
4. https://www.javatpoint.com