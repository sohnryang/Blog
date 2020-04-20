---
layout: post
title: Dancing Links and Sudoku
tags: [algorithms, coding]
---

다시 오랜만에 글 쓴다. 백준에서 [다이아 문제](https://solved.ac/search/tier%3Ad5..d1%20) 아무거나 하나라도 풀고 싶어서 찾던 중, [이 문제](https://www.acmicpc.net/problem/3763)가 풀만 해 보여서 시작했다.

사실 스도쿠 푸는건 이번이 처음이 아니다. 백준 때문은 아니지만 ~~중학교 동아리 시간에 주는 스도쿠 풀어버리고 놀기 위해~~ [스도쿠 푸는 알고리즘을 만든 적은 있다](https://github.com/sohnryang/sudoku-solver). 그때 알고리즘은 제약 전파를 이용했던 걸로 기억하는데, 문제 분류에 ~~백준 특성상 훼이크일 확률도 좀 있지만~~ Knuth's Algorithm X가 있어서 공부해 보기로 했다.

## Knuth's Algorithm X
