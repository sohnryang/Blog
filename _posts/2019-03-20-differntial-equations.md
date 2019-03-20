---
layout: post
title: Differential Equations
tags: [math, physics]
---

분명 나는 수II까지밖에 못배웠는데 방과후에서는 나보고 미분방정식을 풀라고 한다. <strike>망했다</strike>

여기서는 방과후수업에서 받은 자료들과 위키/내 <strike>수학 겁나 못하는</strike> 머리에서 온 것들을 모았다.

## 미분방정식과 그 예
미분방정식은 모르는 함수와 그 함수의 도함수를 포함하는 방정식이다. <strike>여기서 쉽겠네 하고 낚임</strike>

### 선형 미분방정식
모르는 함수와 그 도함수에 대해 1차항까지만 있는 방정식이다.
$$
\frac{dy}{dx} = y
$$

$$
\frac{d^2y}{dx^2} + a_1(x) \frac{dy}{dx} + a_2(x)y = f(x)
$$
등등...

### 비선형 미분방정식
선형 미분방정식과 달리, 2차 이상의 항들이 있다. 이런건 손으로 풀기보다는 컴퓨터가 노가다하는 수치해석 알고리즘을 이용한다.
$$
\frac{d^2y}{dx^2} = k \sin{y}
$$

### 편미분방정식
편미분을 이용한 미분방정식이다. 이런것도 비선형 미분방정식처럼 컴퓨터한테 시킨다.
$$
\frac{\partial^2{V}}{\partial{x^2}} + \frac{\partial^2{V}}{\partial{y^2}} = 0
$$

### 변수분리법
다음과 같은 형태의 미분방정식에 사용하는 방법이다.
$$
\frac{dy}{dx} = f(x)g(y)
$$

#### 예제
다음과 같은 방정식이 있다고 하자.
$$
\frac{dy}{dx} = \frac{y + 1}{x + 1}
$$

양번에 $dy$를 곱한다.
$$
\frac{1}{y + 1}dy = \frac{1}{x + 1}dx
$$

양변을 적분한다.
$$
\int \frac{1}{y + 1}dy = \int \frac{1}{x + 1}dy
$$

이는 다음과 같다. ($C$는 적분상수)
$$
\ln{(y + 1)} = \ln{(x + 1)} + C
$$

정리하면 ($C_1$은 임의의 상수)
$$
y + 1 = C_1(x + 1)
$$

미분방정식 중에서는 그나마 간단하다.

### 수치해석 알고리즘
앞서 말했듯 복잡한 미분방정식은 손으로 풀기보다 노가다를 잘하는 컴퓨터에게 시켜서 푼다. 이러한 알고리즘에는 오일러의 방법같은 것이 있다.

## 참고 문헌
- [Wikipedia 미분방정식 문서](https://en.wikipedia.org/wiki/Differential_Equation)
- [Wikipedia Ordinary Differential Equation 문서](https://en.wikipedia.org/wiki/Ordinary_differential_equation)
