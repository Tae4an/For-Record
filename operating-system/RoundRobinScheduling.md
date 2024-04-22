# Round-Robin 스케줄링


## 기본 개념
- **FCFS와 시간 간격 결합:** First-Come, First-Served(FCFS) 기반으로, 정해진 시간 간격(타임퀀텀) 동안만 프로세스가 CPU를 사용한다.
- **타임퀀텀:** 일반적으로 10~100 밀리초(ms) 사이에서 설정되며, 이는 프로세스가 CPU를 점유할 수 있는 최대 시간을 의미한다.
- **원형 큐 구현:** 준비 큐는 원형큐(circular queue)로 구현되어 각 프로세스가 공평하게 CPU 시간을 할당받는다.

## 특징
- **선점 방식:** 
  - 프로세스가 타임퀀텀을 초과하여 실행되는 경우, 다음 프로세스로 강제 이동시키는 선점 방식을 사용한다.
- **최대 대기 시간:** 
  - 준비 큐에 n개의 프로세스가 있는 경우, 한 프로세스의 최대 대기 시간은 `(n-1) * q`가 된다.
- **문맥 교환의 효과:** 
  - 타임퀀텀이 짧을수록 문맥 교환의 횟수가 증가하여 시스템의 부담이 커질 수 있다. 
    - 이는 문맥 교환에 따른 오버헤드 증가로 이어진다.

## 적용 환경
- **시분할 시스템:** Round-Robin 스케줄링은 시분할 시스템에 적합한 알고리즘으로, 공정한 CPU 시간 배분을 목표로 한다.

## 고려 사항
- **타임퀀텀 설정:** 타임퀀텀의 길이는 시스템의 성능과 직접적으로 관련이 있으며, 너무 짧거나 긴 설정은 효율성을 떨어뜨릴 수 있다.
- **문맥 교환 최소화:** 적절한 타임퀀텀 설정을 통해 문맥 교환을 최소화하고, 시스템의 전체적인 처리량과 반응 시간을 개선할 수 있다.