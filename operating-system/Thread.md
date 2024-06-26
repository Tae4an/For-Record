# 스레드(Thread)

## **스레드 : 동기/아이디어**

대규모 프로그램은 여러 개의 서브프로그램으로 구성되어 있으며, 이를 하나의 실행 단위로 구성하는 경우를 프로세스라고 한다.  
예를 들어, `a.out`은 단일 프로세스 단위로 실행되며, 실행, 준비, 블록 상태 전이를 통해 운영된다.  
서브프로그램 중 하나가 I/O를 요구할 경우 전체 프로세스가 블록된다.

### 서브프로그램을 실행 단위로 만들 경우

하나의 서브프로그램에서 I/O를 요구할 경우 해당 서브프로그램만을 블록 시킨다.  
이를 통해 프로세스 내의 다른 서브프로그램은 독립적인 실행 단위로 계속 실행할 수 있다.

## **스레드의 정의**

-   스레드는 **경량화된 프로세스(Lightweight Process)** 로서, 프로세스 내에서 실행되는 독립적인 실행 경로이며, 자신의 실행 상태를 가지고 다른 스레드와 프로세스의 자원을 공유한다..
-   **스레드 제어 블록(TCB)**:
    -   각 스레드는 하나의 TCB를 가지고 있다.
-   **독립적 CPU 사용**:
    -   스레드는 CPU를 사용할 때 독립적으로 레지스터들을 사용한다.
    -   문맥 교환을 위해 레지스터 저장 공간이 필요하다.
-   **자원 공유**:
    -   같은 프로세스에 의해 생성된 스레드들은 텍스트와 데이터 부분을 공유한다.
        -   예를 들어, 전역 변수나 `open()`한 파일 디스크립터 등이 이에 해당한다.

## **스레드의 장점**

-   실행 단위가 스레드로 세분화되어 병행 수행이 증가한다.
-   **문맥 교환** 시간이 줄어든다.
-   스레드 생성 시간이 프로세스 생성 시간에 비해 짧고 효율적이다.

## **프로세스와 스레드의 비교**

-   **기존의 프로세스(Traditional or Heavyweight Process)**: 한 개의 스레드로 구성된 프로세스, 실행 단위가 한 개로 구성된 프로세스.
-   **프로세스 구성**: Text, Data 그리고 Stack으로 구성됨, PCB를 가짐.
-   **스레드(경량화된 프로세스)**: 하나의 프로세스 내에 여러 개의 스레드로 구성되어 있으며, Text와 Data는 프로세스 내의 스레드들 간에 공유됩니다. 각 스레드는 별도의 스택과 TCB를 가진다.

## **멀티스레드의 장점**

-   **응답성 향상**: 다중 스레드를 사용하면 하나의 스레드가 대기 상태일 때 다른 스레드가 작업을 계속 수행할 수 있어 전체 응답성이 향상된다.
-   **자원 공유**: 같은 프로세스 내의 스레드들은 메모리와 자원을 공유하므로 자원의 효율적 사용이 가능하다.
-   **효율성 향상**: 스레드 간의 문맥 교환은 프로세스 간의 문맥 교환보다 빠르고 자원을 덜 사용하므로 시스템의 효율성이 증가한다.
-   **다중 CPU 지원**: 멀티스레드 프로그램은 다중 CPU 환경에서 각 스레드가 별도의 프로세서에서 실행될 수 있어 성능이 향상된다.

## **단일 스레드 지원 운영체제**

-   **예시**: MS-DOS
-   **특징**: 하나의 프로세스에서 하나의 스레드만 실행 가능. 스레드 개념이 불확실.

## **다중 스레드 지원 운영체제**

-   **예시**: Windows NT, Solaris
-   **특징**: 하나의 프로세스에서 여러 스레드 실행 지원. 프로세스 내부의 스레드들이 자원을 공유하여 자원의 생성과 관리 중복성을 최소화하고, 각 스레드는 독립적으로 수행 가능.

## POSIX 스레드 라이브러리 및 관련 개념

### 1\. POSIX 스레드 라이브러리 (libpthread)

POSIX 스레드 라이브러리, `libpthread`,는 POSIX 표준에 근거하여 다양한 운영 체제에서 멀티스레딩을 지원하기 위해 사용된다. 이 라이브러리는 스레드의 생성, 종료 및 동기화 기능을 제공하여 개발자가 멀티스레드 응용 프로그램을 쉽게 구현할 수 있도록 돕는다.

### 2\. 주요 함수 설명

-   **`pthread_create()`**: 새로운 스레드를 생성하는 데 사용되는 함수다. 이 함수는 스레드 ID, 스레드 속성, 실행할 함수의 포인터, 그리고 그 함수의 인자를 매개변수로 받는다.
-   **`pthread_join()`**: 특정 스레드가 종료될 때까지 대기한다. 이 함수는 스레드가 종료되는 것을 확인하고 그 스레드의 리턴 값을 회수하는 데 사용된다.
-   **`pthread_exit()`**: 호출한 스레드를 종료시킵니다. 이 함수는 스레드의 종료 상태를 인자로 받아 다른 스레드에서 `pthread_join()`을 통해 이 값을 얻을 수 있도록 한다.

### 3\. `-lpthread` 옵션의 의미

`-lpthread` 옵션은 gcc 컴파일러에 POSIX 스레드 라이브러리를 링크하도록 지시한다. 이 옵션은 컴파일러에게 멀티스레딩 프로그램의 컴파일 시 필요한 스레드 관련 기능을 libpthread에서 찾도록 한다.

-   `gcc -lpthread -o thread thread.c` 명령에서 `-lpthread`는 링커가 스레드 관련 기능을 필요로 하는 코드를 컴파일할 때 필요한 스레드 라이브러리(libpthread)를 실행 파일에 연결하도록 한다.

### 4\. 라이브러리란?

라이브러리는 재사용 가능한 코드의 집합으로, 함수나 데이터를 모듈화하여 필요할 때 링크하여 사용할 수 있다.

라이브러리는 정적 라이브러리와 동적 라이브러리로 구분되며, `libpthread`와 같은 스레드 라이브러리는 시스템의 멀티스레딩 기능을 제공하는 동적 라이브러리의 예다.

### 5\. 링커의 역할

링커는 컴파일된 여러 코드 파일들을 하나의 실행 파일로 합치는 작업을 수행한다.

또한, 필요한 라이브러리를 프로그램에 연결하는 역할도 한다.

`-lpthread`와 같은 옵션을 사용할 때, 링커는 해당 라이브러리(libpthread)를 찾아 프로그램과 링크한다.

### 6\. 분리 컴파일

분리 컴파일은 큰 프로그램을 여러 소스 파일로 나누어 각각 독립적으로 컴파일한 후, 링킹 과정을 통해 최종 실행 파일을 생성하는 프로세스다. 이 방법은 코드 관리를 용이하게 하며, 수정이 필요한 부분만 재컴파일하여 시간을 절약할 수 있다.