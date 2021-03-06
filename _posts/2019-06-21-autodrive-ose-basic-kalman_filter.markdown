---
layout: post
title: 칼만 필터의 전체적인 구조
date: 2019-06-23 00:00:00
img: autodrive/ose/kalman_filter.jpg
categories: [autodrive-ose] 
tags: [컴퓨터 비전, 칼만 필터, kalman filter] # add tag
---

<br>

[Optimal State Estimation 글 목록](https://gaussian37.github.io/autodrive-ose-table/)

<br>

- 출처 : 칼만필터는 어렵지 않아
- 이번 글에서는 칼만필터의 전체적인 구조 및 이론에 대하여 알아보도록 하겠습니다.
- 이 글에서는 칼만 필터의 이론적인 배경이나 증명 보다는 사용적인 측면에서의 이론을 다룹니다.
    - 만약 칼만 필터 이론의 상세 내용에 관심이 있으시면 이 글을 참조하시면 쉽게 이해가 되실 겁니다.
    - 링크 : https://gaussian37.github.io/ad-ose-lkf_basic/
- 아래 스테이트 다이어그램은 칼만 필터의 전체 플로우를 나타냅니다.
- 이번 글의 목적은 아래 플로우 전체를 이해하기 위한 것이니 천천히 따라가시면 이해가 될 거라고 생각됩니다.

<br>
<center><img src="../assets/img/autodrive/ose/basic/kalman.png" alt="Drawing" style="width: 800px;"/></center>
<br>

- 위 다이어그램을 보면 수식은 조금 어려워 보일 수 있으나 간단히 설명하면 1단계에서 4단계까지 순서대로 수행한다고 생각하시면 됩니다.
- 사용만 하려고 한다면 수식의 의미를 정확히 이해하지 못한다 하더라고 기계적으로 따라하기만 해도 됩니다.
- 자 그러면 위의 다이어그램을 한번 보겠습니다. 점선으로 이루어진 다이어그램이 `칼만 필터 알고리즘`입니다.
- 입력과 출력이 하나씩인 구조로 측정값($$ z_{k} $$)가 주어지면 알고리즘 내부에서 처리한 다음 추정값($$\hat{x}_{k}$$)를 출력합니다.
- 내부 계산은 총 4단계를 거치게 됩니다. 알고리즘을 분석할 때 아래첨자 `k`는 `k`번째 측정값에 대한 계산이라는 뜻이고 알고리즘이 반복해서 수행된다는 것을 뜻합니다.
- 칼만 필터의 전체 구조가 이전 스텝 (`k-1`)의 값을 이용하여 현재 스텝 (`k`)의 값을 업데이트 한다는 것이기 때문에 `k` 라는 인덱스를 추가한 것이므로 헷갈린다면 잠시 무시하셔도 됩니다. 다만 **이전 스텝과 현재 스텝** 이것은 기억하셔야 합니다.
- 반면 위 첨자(`-`)는 매우 중요한 기호이오니 구분하시고 보셔야 합니다.

<br>

[Optimal State Estimation 글 목록](https://gaussian37.github.io/autodrive-ose-table/)

<br>