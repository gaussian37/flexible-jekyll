---
layout: post
title: Mini-batch gradient descent
date: 2019-07-08 00:00:00
img: dl/dlai/dlai.png
categories: [dl-dlai] 
tags: [python, deep learning, optimization, mini-batch gradient descent] # add tag
---

<br>
<div style="text-align: center;">
    <iframe src="https://www.youtube.com/embed/4qJaSmvhxi8" frameborder="0" allowfullscreen="true" width="600px" height="400px"> </iframe>
</div>
<br>

- 이번 시간에는 신경망 네트워크를 훨씬 더 빨리 트레이닝 시킬 수 있도록 도와주는 최적화 알고리즘에 대하여 배워보도록 하겠습니다.
- ML을 적용하는 것은 매우 경험적이고 반복적인 작업을 동반하는 것으로 여러 모델들을 학습시키고 가장 잘 동작하는 것을 찾아야 합니다.
- 따라서 학습의 속도 또한 매우 중요 합니다. 
- 또한 DL의 경우 큰 데이터에 잘 작동하는 경향이 있습니다. 신경망을 큰 데이터 셋에서 학습을 시킬 수 있는데, 이런 경우 학습이 매우 느립니다.
- 이런 경우 빠른 최적화 알고리즘과 양질의 최적화 알고리즘을 갖는 것이 효율성을 높일 수 있습니다. 
- 이번 시간에는 이러한 방법 중 하나인 `미니 배치 그래디언트 디센트`에 대하여 알아보도록 하겠습니다.

<br>

<center><img src="../assets/img/dl/dlai/mini_batch_gradient_descent/1.PNG" alt="Drawing" style="width: 800px;"/></center>

<br>

- 먼저 위 슬라이드와 같이 $$ X $$ (학습 데이터) 와 $$ Y $$ (정답 데이터)가 있다고 가정해 보겠습니다.
- 이 때, $$ X $$ 의 차원은 $$ (n_{x}, m) $$이 되고 $$ Y $$의 차원은 $$(1, m)$$이 됩니다. 
- 예를 들어 데이터 셋의 크기인 $$ m $$이 5백만 이라고 가정해 보겠습니다. 꽤 큰 값이지요?
- 이런 경우 한번에 학습할 데이터의 양을 작게 나눈다고 생각해 보겠습니다. 그리고 작은 단위의 학습 데이터셋을 `미니 배치`라고 부르겠습니다.
- 예를 들어 1,000개의 단위로 학습 데이터를 쪼개서 생각한다면 $$ (x^{(1)}, x^{(2)}, \cdots , x^{(1000)}) $$ 까지가 첫번째 미니 배치에 해당합니다.
    - 표기의 편의상 $$ (x^{(1)}, \cdots,  x^{(1000)}) $$ 을 $$ X^{\{1\}} $$로 $$ (x^{(1001)}, \cdots,  x^{(2000)}) $$ 을 $$ X^{\{2\}} $$로 표시하겠습니다.
    - 그러면 마지막 배치는 $$ X^{\{5000\}} $$이 됩니다. 
- 이에 상응하게 $$ Y $$ 데이터도 동일한 크기로 나누어야 합니다. 따라서 Y 데이터도 미니 배치 단위로 $$ Y^{\{1\}}, Y^{\{2\}}, \cdots, Y^{\{5000\}} $$이 됩니다.
- 그러면 한번에 모든 데이터를 이용하여 학습을 하는 경우와 미니 배치 단위로 학습을 하는 경우가 나뉘게 됩니다.
- 앞에서 배워왔던 gradient descent 방법은 한 번에 모든 데이터를 이용하여 학습을 합니다. 즉, 한 번에 학습하는 학습 데이터의 범위가 $$ X, Y $$가 됩니다.
- 반면 이번에 배울 mini-batch gradient descent 방법은 한 번에 미니 배치 하나를 이용하여 학습을 합니다. 즉, 한 번에 학습하는 학습 데이터의 범위는 $$ X^{(t)}. Y^{(t)} $$ 가 됩니다.

<br>

<center><img src="../assets/img/dl/dlai/mini_batch_gradient_descent/2.PNG" alt="Drawing" style="width: 800px;"/></center>

<br>

- 그러면 미니 배치 그레디언트 디센트가 어떻게 작동하는 지 한번 알아보도록 하겠습니다.
- 미니 배치 그레디언트 디센트를 학습 데이터에서 사용하기 위해서 배치를 t = 1 ~ 5000까지 실행해 보면 됩니다. 각각 1000개씩 데이터를 가지고 있는 미니 배치가 5000개 있기 때문입니다.
- for loop 내부에서는 첫번째로 입력 값에 대한 forward propagation을 수행합니다.
    - 즉, 학습 데이터 $$ X^{t} $$에 대하여 먼저 forward propagation을 수행합니다.
- forward propagation은 위 슬라이드의 식과 같이 구성될 수 있습니다. 예를 들어 
    - 　$$ Z^{[1]}  = W^{[1]}X^{t} + b^{[1]} $$ 일 때, $$ A^{[1]} = g^{[1]}(Z^{[1]}) $$ 가 됩니다.
    - 같은 원리로 $$ A^{[l]} = g^{[l]}(Z^{[l]}) $$ 이 됩니다.
    - 그러면 $$ (W^{[1]}, b^{[1]}) $$ 부터 $$ (W^{[l]}, b^{[l]}) $$ 까지 모두 $$ X^{t} $$ 배치 데이터와 연산이 되어 forward prop이 되어야 합니다.
- 이 때, forward prop은 벡터라이제이션을 이용하여 한번에 모든 가중치와 배치 데이터가 연산되도록 해야 효율적입니다.
    - 즉 $$ W $$와 $$ X^{t} $$가 한번에 벡터라이제이션을 통하여 곱해져야 합니다.
- 각 배치의 크기가 1,000이므로 Cost function $$ J $$는 위 슬라이드와 같이 표현될 수 있습니다. 
    - 평균값을 위하여 1,000으로 나누게 되고 추가적으로 regularization 항도 추가하였습니다.
    - 따라서 $$ J^{t} = \frac{1}{1000} \sum_{i=1}^{l} \mathcal L (\hat{y}^{(i)}, y^{(i)}) + \frac{\lambda}{2 \cdot 1000} \sum_{l} \Vert W^{[l]} \Vert^{2} $$ 가 됩니다.
- Cost function 까지 구하고 나면 이 함수를 기반으로 back propagation을 수행합니다.
- 미니 배치 그레디언트 디센트를 사용하므로 back prop은 $$ J $$가 아닌 $$ J^{t} $$를 대상으로 수행되고 이 때 대상 데이터는 $$ (X^{t}, Y^{t}) $$ 입니다.
- back prop을 하고나면 $$ W^{[l]} = W^{[l]} - \alpha dW^{[l]} $$, $$ b^{[l]} = b^{[l]} - \alpha db^{[l]} $$ 로 Weight와 bias가 업데이트 됩니다.
- 1 epoch 이라고 하면 모든 데이터셋이 한번 학습된 것을 뜻하게 됩니다. 따라서 기존의 그레디언트 디센트 방법에서는 1 epoch을 학습하면 1번의 업데이트가 발생하게 됩니다.
- 반면 미니 배치 그레디언트 디센트에서는 1 epoch에서는 여러번의 업데이트가 발생하게 되는데요. 위 예제에서는 5,000개의 배치가 있으므로 1 epoch에 5,000번의 업데이트가 발생하게 됩니다.
- 따라서 큰 데이터 셋이 있는 경우 미니 배치 그레디언트 디센트를 사용하면 기본적인 그레디언트 디센트를 사용할 때 보다 훨씬 더 빨리 학습이 수렴되게 됩니다.
- 미니 배치 그레디언트 디센트에 대한 조금 더 자세한 내용은 다음 글에서 다루어 보겠습니다.       

<br>

- 다음 글 : [Understanding mini-batch gradient descent](https://gaussian37.github.io/dl-dlai-understanding_mini-batch_gradient_descent/) 