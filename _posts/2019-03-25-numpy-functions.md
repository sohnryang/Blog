---
title: Numpy functions
layout: post
tags: [python, numpy]
---

저번에 올린 [matplotlib 함수 모음](https://sohnryang.github.io/blog/2019/03/17/matplotlib-functions.html)에 이어 이번에는 numpy에 관해 올리려고 한다. <strike>고만좀 물어보라고 미친것들아</strike>

## `array` 함수
numpy 배열을 만든다. arg로 파이썬 리스트를 받는다.

```python
import numpy as np
arr = np.array([1, 2, 3])
```

## `linspace`와 `arange` 함수
어떤 범위 안의 값들을 가진 배열을 만든다.

`linspace(start, end, num)`는 `start`부터 `end`까지 `num`개의 값들을 가진 배열을 만든다.

반면 `arange(start, stop, step)`은 `start`이상 `stop`미만의 값들을 가진 배열을 만든다. 여기서 `start`나 `step`을 안주고 `stop`만 주면 `start = 0`, `step = 1`인 것처럼 실행된다.

```python
import numpy as np
arr1 = np.linspace(0, 9, 10) # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]와 같음
arr2 = np.arange(0, 10, 1) # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]와 같음
```

## `zeros`함수
이름 그대로 0으로 채워진 배열을 만든다.

```python
import numpy as np
arr1d = np.zeros(5) # [0, 0, 0, 0, 0]과 같음
arr2d = np.zeros((2, 2)) # [[0, 0], [0, 0]]과 같음
```

## `sum`함수
배열에 담긴 수들의 합을 구한다.

```python
import numpy as np
arr = arange(10)
result = np.sum(arr) # 결과값은 45
```

## 배열 연산 (일명 broadcasting)
numpy 배열에 직접 연산을 하는 방법이다. 예를 들어 어떤 숫자 배열이 있는데, 배열에 있는 숫자들에 각각 1씩 더하고 싶다고 해보자. 파이썬 리스트에 익숙한 사람은 반복문을 쓰거나, 리스트 컴프리헨션을 쓸것이다. (몰라도 상관없으니 그냥 넘어가도 된다.)

numpy에서는 그냥 덧셈연산자를 쓰면 된다. 우리가 1씩 더하고 싶은 배열이 `arr`이라고 하면 그냥 이렇게 쓰면 된다.

```python
arr = arr + 1
```

numpy 배열에 덧셈, 뺄셈, 나눗셈, 곱셈과 같은 연산을 하면 그냥 배열의 모든 숫자들에 대해서 한다고 받아들인다. 심지어 `<`, `>`, `>=`, `<=`, `==`과 같은 조건 연산자에서도 이것이 가능한데, 이런 경우에는 결과 배열에 숫자가 아니라 `True`와 `False`가 들어가게 된다.

```python
import numpy as np
arr = np.arange(10)
bigget_than_5 = arr > 5 # [False, False, False, False, False, False, True, True, True, True]
```

## 인덱싱과 슬라이싱
배열에서 원하는 값들을 뽑아오는 방법들이다.

### 인덱싱
numpy 배열에서 특정 부분에 있는 값들을 가져온다. 파이썬 표준 리스트와 같이 -1을 인덱스로 넣어주면 맨 마지막 것을 준다.

```python
import numpy as np
arr = np.arange(10)
first_element = arr[0] # 가장 처음
last_element = arr[-1] # 가장 마지막
```

2차원 이상의 배열인 경우 쉼표로 차원을 구분한다.

```python
import numpy as np
arr = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
top_left = arr[0,0] # 왼쪽 위
```

또한, `True`와 `False`로 이루어진 배열로 인덱싱할 수 있다. 예를 들어 5보다 큰 숫자들만 뽑고 싶다고 하자.

```python
import numpy as np
arr = np.arange(10)
bigger_than_5 = arr[arr > 5]
```

### 슬라이싱
슬라이싱은 배열에서 원하는 범위의 숫자들을 가져올 수 있게 해준다. 배열이 `arr`일때 다음과 같은 방법을 이용하여 슬라이싱한다.

```python
arr[시작위치:끝위치]
```

시작위치가 0이거나 끝위치가 맨 마지막 원소일 경우 생락할 수 있고, 여기서 끝위치에 있는 원소는 결과에 포함하지 않으니 조심하자. <strike>이런걸로 나 부르지 말고</strike>

```python
import numpy as np
arr = np.arange(10)
sliced = arr[1:5] # [1, 2, 3, 4]
```

또한, `arr[:]`과 같이 하면 그냥 `arr`라고 하는것과 같은 효과가 있다. 이런 기능은 특히 2차원 이상의 배열에서 유용하다.

예를 들어 내가 계산한 시간에 대해 위치와 속도가 다음과 같은 2차원 배열로 담겨 있고, 내가 위치만 뽑아내고 싶다고 하자.

```python
[[1, 2],
 [3, 4],
 [5, 6],
 [7, 8]
 ...
 [41, 42]]
```

이때 위치만 뽑아내면 `[1, 3, 5, 7, ... 41]`이고, `data`라는 이름의 배열에 있다고 할 때 다음과 같이 뽑아낼 수 있다.

```python
data[:,0]
```

이를 설명하자면, 우선 첫먼째 차원에서 모든 원소를 다 선택하고, 두번째 차원에서 0번째 원소만 선택한다는 뜻이다.

## <strike>난 그래도 모르겠는데?</strike>
공식문서에서 찾아서 보자 <strike>물어보기 전 생각좀</strike>

[numpy API docs](https://docs.scipy.org/doc/numpy-1.14.1/reference)
