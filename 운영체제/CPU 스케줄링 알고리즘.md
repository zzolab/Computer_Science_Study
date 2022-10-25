# CPU 스케줄링 알고리즘
- 어떤 프로세스에 CPU 소유권을 줄 것인지 결정하는 알고리즘

***

## 비선점형 방식
- 프로세스가 스스로 CPU 소유권을 포기하는 방식으로, 강제로 프로세스를 중지하지 않음
- 컨텍스트 스위칭으로 인한 부하가 적음

### FCFS (First Come, First Served, 선입 선처리 스케줄링)
- CPU를 먼저 요청하는 프로세스가 CPU를 먼저 할당
- Queue로 쉽게 관리
![image](https://user-images.githubusercontent.com/66233687/196361699-2f0b242a-759a-4ead-80c2-a98702062f88.png)
- Convoy Effect 발생 : 길게 수행되는 프로세스 때문에 다른 프로세스들이 준비 Queue에서 오래 기다리는 현상

### SJF (Shortest Job First, 최단 작업 우선 스케줄링)
- CPU가 이용 가능해지면, 가장 작은 next CPU burst를 가진 프로세스에 CPU를 할당
- 두 프로세스가 동일한 길이의 next CPU burst를 가지면, 선입 선처리 스케줄링을 적용
> CPU burst : 사용자 프로그램이 CPU를 직접 가지고 빠른 명령을 수행하는 단계
- 실행하기 전 next CPU burst의 길이를 완벽하게 예측하기 어려움
- starvation 발생 : CPU burst가 긴 프로세스가 실행되지 않음.

### 우선순위 (Priority Scheduling)
- 가장 높은 우선순위의 프로세스에 CPU를 할당
- starvation 발생 : 낮은 우선순위의 프로세스가 실행되지 않음.

***

## 선점형 방식
- 현대 운영체제가 쓰는 방식
- 지금 사용하고 있는 프로세스를 알고리즘에 의해 중단시켜 버리고 강제로 다른 프로세스에 CPU 소유권을 할당하는 방식

### 라운드 로빈
> round robin : 순환 순서 방식. 리스트의 맨 위에서 아래로 가며 하나 씩 뽑고, 끝나면 다시 맨 위로 돌아가는 식으로 진행된다. 쉽게 말해 "기회를 차례대로 받기"
- 각각의 프로세스에 동일한 CPU 할당 시간을 부여해서 해당 시간 동안만 CPU를 할당
- 할당 시간 내에 처리를 완료하지 못하면 다음 프로세스로 넘어감
- n개의 프로세스가 있을 때 할당 시간을 q로 설정하면, 어떤 프로세스도 (n-1)q 시간 이상을 기다리지 않음
- q가 커진다면 FCFS처럼 작동
- q가 매우 작아지면 process sharing : n개의 프로세스가 프로세서 속도의 1/n 씩으로 작동함
- 응답 시간을 빠르게 할 수 있다는 장점

### SRF (Shortest Remaining Time First)
- SJF와 같이 작은 next CPU burst를 가진 프로세스에 CPU를 할당
- 남은 프로세스의 burst time보다 더 짧은 process가 도착하면 CPU를 빼앗음
- 프로세스가 새로 들어올때마다 갱신됨
- Starvation 발생
- 새로운 프로세스가 들어올때마다 스케줄링이 변경되므로 CPU 사용 시간(burst time)을 정확히 예측하기 어려움

### 다단계 큐 스케줄링 (MLQ, MultiLevel Queue Scheduling)
- 우선순위마다 준비 큐 형성
- 항상 가장 높은 우선순위 큐의 프로세스에 CPU를 할당 
- 우선순위가 낮은 큐에서 작업 실행 중이더라도 상위 단계의 큐에 프로세스가 도착하면 CPU를 빼앗는 선점형 스케줄링
- 각 큐는 라운드 로빈이나 FCFS등 독자적 스케줄링 사용 가능
- 큐들 간의 프로세스 이동이 불가하기 때문에 스케줄링 부담이 적지만 유연성이 떨어짐
- 우선순위가 낮은 프로세스가 오랫동안 CPU 할당을 기다리는 starvation 현상이 발생할 수도 있음

![image](https://user-images.githubusercontent.com/66233687/196369330-f864493f-055f-459c-b4a7-a8c284fcf0c9.png)

## Reference
- https://code-lab1.tistory.com/m/45
- https://velog.io/@ss-won/OS-CPU-Scheduling-Algorithm
- https://blog.naver.com/PostView.nhn?isHttpsRedirect=true&blogId=wndrlf2003&logNo=70188882999&parentCategoryNo=&categoryNo=&viewDate=&isShowPopularPosts=false&from=postView
