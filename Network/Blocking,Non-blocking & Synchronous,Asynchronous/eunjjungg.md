# 1. 정의

- Blocking : A 함수가 B 함수를 호출할 때 B 함수가 자신의 작업이 종료되기 전까지 A 함수에게 제어권을 돌려주지 않는 것
- Non-Blocking : A 함수가 B 함수를 호출 할 때, B 함수가 제어권을 바로 A 함수에게 넘겨주면서, A 함수가 다른 일을 할 수 있도록 하는 것
- Synchronous : A 함수가 B 함수를 호출 할 때, B 함수의 결과를 A 함수가 처리하는 것.
- Asynchronous : A 함수가 B 함수를 호출 할 때, B 함수의 결과를 B 함수가 처리하는 것. (callback)


<br/><br/>

# 2. 매트릭스 이해

![image](https://user-images.githubusercontent.com/100047095/196027647-8ece6522-dbf8-4829-a664-aafb73e09e13.png)

<br/>

**Sync-NonBlocking 모델**

- Synchronous : A 함수가 B 함수를 호출 할 때, B 함수의 결과를 A 함수가 처리하는 것.
- Non-Blocking : A 함수가 B 함수를 호출 할 때, B 함수가 제어권을 바로 A 함수에게 넘겨주면서, A 함수가 다른 일을 할 수 있도록 하는 것
- 따라서 조합해보면 B 함수가 호출되고 non-blocking에 의해 제어권을 바로 돌려주기에 A 함수는 다른 일을 수행할 수 있지만 언제 종료되는지 알 수 없는 B 함수의 종료를 synchronous에 의해 A 함수가 처리해야 함. 따라서 언제 종료되는지 알 수 없기에 A 함수가 반복적으로 종료를 B 함수에게 물어야 함.

<br/>

**Sync-Blocking 모델**

- Synchronous : A 함수가 B 함수를 호출 할 때, B 함수의 결과를 A 함수가 처리하는 것.
- Blocking : A 함수가 B 함수를 호출할 때 B 함수가 자신의 작업이 종료되기 전까지 A 함수에게 제어권을 돌려주지 않는 것
- 조합해보면 그냥 간단함. Blocking에 의해 A 함수가 B 함수를 호출하고 제어권을 돌려받지 못하고 대기하고, B 함수가 종료를 하면 그때서야 A 함수가 제 할 일을 수행할 수 있는 상황.

<br/>

**ASync-NonBlocking 모델**

- Asynchronous : A 함수가 B 함수를 호출 할 때, B 함수의 결과를 B 함수가 처리하는 것. (callback)
- Non-Blocking : A 함수가 B 함수를 호출 할 때, B 함수가 제어권을 바로 A 함수에게 넘겨주면서, A 함수가 다른 일을 할 수 있도록 하는 것
- 조합해보면 A 함수가 B 함수를 호출하고 제어권은 바로 A 함수가 가지고 B 함수의 종료 여부에 대해 신경쓰지 않아도 됨. 콜백으로 종료를 B 함수가 처리하고 A 함수에게 알리기 때문.

<br/>

**ASync-Blocking 모델**

- Asynchronous : A 함수가 B 함수를 호출 할 때, B 함수의 결과를 B 함수가 처리하는 것. (callback)
- Blocking : A 함수가 B 함수를 호출할 때 B 함수가 자신의 작업이 종료되기 전까지 A 함수에게 제어권을 돌려주지 않는 것
- 조합해보면 A 함수가 B 함수를 호출하고 아무일도 하지 못함. 왜냐하면 Blocking에 의해 제어권을 A 함수에게로 넘겨주지 않기 때문. 또한 B 함수의 결과를 B 함수가 처리해야 하므로 모두 처리하고 콜백으로 A 함수가 불리기 전까지는 아무것도 하지 못함.
