---
layout: post
title: Useful Matplotlib Functions
tags: [python, matplotlib]
---

계산물리 시간에 파이썬으로 그래프를 그려야 할 때가 있어서 관련 함수들을 정리했다.

<strike>사실 뭐 물어볼때 말/코드로 대답하기 귀찮고 일요일 면학 3타임에 잉여로워서라 카더라</strike>

사실 여기 나온것보다 훨씬 옵션이나 arg가 많지만 일단 필요한것 위주로 정리했다.

## `figure` ([API docs](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.figure.html#matplotlib.pyplot.figure))

matplotlib에게 그래프를 준비한다고 알려준다. 사실 그래프를 하나만 그릴 때와 같이 간단한 경우에는 알아서 library가 눈치 까서(?) 그려주지만 그래프를 여러개 그리거나, 그래프에 무언가 복잡한 작업을 할 때는 명시적으로 쓰는 것이 더 좋다.

## `show` ([API docs](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.show.html#matplotlib.pyplot.show))

솔직히 할말이 별로 없다. `figure`을 실행한 후에 만든 그래프를 화면에 띄운다.

## `plot` ([API docs](https://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.plot))

`plot`은 배열을 받아 그래프를 그리고, 선 모양을 설정할 수 있다.

선 모양은 `ro`와 같이 설정하는데, 0번째 글자가 색, 그 후의 글자가 선 모양을 정한다.

또한, kwarg로 그리는 곡선의 이름인 `label`을 받는데, `legend`에서 설명한다.

### 예제 코드

```python
import matplotlib.pyplot as plt
plt.plot([1, 2, 3, 4])
plt.plot([1, 2, 3, 4], [1, 2, 3, 4], 'ro') # red dots
```

## `xlabel`, `ylabel` ([API docs](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.xlabel.html#matplotlib.pyplot.xlabel))

축에 붙일 레이블이다.

## `axis` ([API Docs](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.axis.html#matplotlib.pyplot.axis))

y축, x축의 범위를 정하는 함수이다.

### 사용법

```python
plt.axis([x_min, x_max, y_min, y_max])
```

## `xlim`, `ylim` ([API docs](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.xlim.html#matplotlib.pyplot.xlim))

x축, y축의 범위를 설정한다. `axis`로 이 함수가 하는일을 커버할 수 있다.

## `legend` ([API docs](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.legend.html#matplotlib.pyplot.legend))

<strike>matplotlib의 전설</strike>

우선 그래프를 `plot`으로 그리는 시점에서 앞서 말한 `label`로 이름을 정한다.

### 예제 코드

```python
import matplotlib.pyplot as plt
plt.figure()
plt.plot([1, 2, 3, 4], label='Some Graph')
plt.legend()
plt.show()
```

### 위치 정하기

kwarg중 하나인 `loc`으로 어디에 붙어있을지를 정할 수 있다. "upper right", "lower left"와 같이 문자열로 써주면 알아서 해준다.

그리고 "best"가 있는데, 이건 그래프를 고려해서 그냥 자동으로 위치를 정해준다. 대규모 그래프에서는 느리다는 경고가 API docs에 있었다.

> The 'best' option can be quite slow for plots with large amounts of data. Your plotting speed may benefit from providing a specific location.

우리 방과후 수업에서는 그래프를 많아봐야 10개정도 그릴 것 같으니까 굳이 걱정 안해도 될 것같다.

가능한 위치들은 다음과 같다.

- best
- upper right
- upper left
- lower left
- lower right
- right
- center left
- center right
- lower center
- upper center
- center

원한다면 이렇게 위치를 정하는 대신 튜플로 좌표를 정해줄 수 있긴 하지만, 그렇게까지 힘들게 할 필요는 없을 듯하다.

## 참고 자료

모르는것 있으면 여기서 찾아보자. <strike>바쁜사람 괴롭히지 말고</strike>

[matplotlib API docs](https://matplotlib.org/genindex.html)
