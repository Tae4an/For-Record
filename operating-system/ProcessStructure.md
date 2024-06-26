# 프로세스의 구조와 fork() 시스템 호출

## 프로세스의 구조

### 코드 영역
- 프로그램의 본문이 기술된 곳으로, 프로그래머가 작성한 코드가 탑재된다.
- 탑재된 코드는 읽기 전용으로 처리되어 변경할 수 없다.

### 데이터 영역
- 코드가 실행되면서 사용하는 변수나 파일 등의 각종 데이터를 모아놓은 곳이다.
- 데이터는 변하는 값이기 때문에 이곳의 내용은 기본적으로 읽기와 쓰기가 가능하다.

### 스택 영역
- 운영체제가 프로세스를 실행하기 위해 부수적으로 필요한 데이터를 모아놓은 곳이다.
- 프로세스 내에서 함수를 호출하면 해당 함수를 수행하고 원래 프로그램으로 되돌아올 위치를 이 영역에 저장한다.
- 이 영역은 사용자에게는 보이지 않으며 운영체제에 의해 관리된다.

## fork() 시스템 호출

### 개념
- 실행 중인 프로세스로부터 새로운 프로세스를 복사하는 함수다.
- 실행 중인 프로세스와 똑같은 프로세스가 하나 더 만들어진다.

### 동작 과정
- `fork()` 시스템 호출을 하면, 부모 프로세스의 프로세스 제어 블록(PCB)을 포함한 대부분의 영역이 자식 프로세스에 복사된다.
- 복사된 내용 중 프로세스 구분자, 메모리 관련 정보, 부모 및 자식 프로세스 구분자는 변경된다.

### 장점
- 프로세스의 생성 속도가 매우 빠르다.
- 추가 작업 없이 자원을 상속할 수 있다.
- 시스템 관리를 효율적으로 할 수 있다.

### 예
- 부모 프로세스의 코드가 실행되어 `fork()` 문을 만나면, 똑같은 내용의 자식 프로세스를 하나 생성한다.
- 이때 `fork()` 문은 부모 프로세스에 0보다 큰 값을 반환하고, 자식 프로세스에는 0을 반환한다.
- 만약 0보다 작은 값을 반환하면 자식 프로세스가 생성되지 않은 것으로 간주하고 ‘Error’를 출력한다.
