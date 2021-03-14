# :mag: Index

- [Ensemble 이란?](#idx1) 

- [Ensemble 의 3가지 유형](#idx2) 

- [1. Voting](#idx3)

- [2. Bagging](#idx4) 

- [3.Boosting](#idx5)
- [참고자료](#idx6)

  

---

### :radio_button: Ensemble 이란? <a id="idx1"></a>

​	

__머신러닝/딥러닝에서 앙상블이란 여러 단일 예측(or 분류)모델을 하나로 엮어 더 좋은 성능의 복합 모델을 만드는 기법을 뜻한다.__

​	

사람으로 치면 조금 똑똑한 사람 여러명을 통한 집단 지성으로 아주 똑똑한 전문가 한 명보다 더 좋은 결과를 가져오는 상황 쯤으로 이해할 수 있다.

​	

뛰어난 성능의 단일 모델도 물론 좋지만, 적당한 성능의 여러 단일 모델 조합하여 앙상블 모델을 활용하면 더 뛰어난 일반화 성능을 자랑하는 경우가 많기 때문에 지금까지도 이를 활용한 연구가 활발히 진행되고 있다.

<p align="center">
    <img src="https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=http%3A%2F%2Fcfile1.uf.tistory.com%2Fimage%2F277EC53454C39CD9353783" alt="집단지성" width=300
</p>



​		

---

### :radio_button: Ensemble 의 3가지 유형 <a id="idx2"></a>

​	

이러한 앙상블 기법에는 여러 종류가 있지만 가장 대표적이고 많이 쓰이는 유형은 3가지가 있다.

1. __Voting__ 

2. __Bagging__ 

3. __Boosting__ 

   

각 기법을 활용하는 대표 모델은 다음과 같다.

> __Bagging__ : Random Forest

> __Boosting__ : AdaBoost, Gradient Boost, XGBoost, LGBM

​	

---

### :radio_button: 1. Voting <a id="idx3"></a>

​	

Voting 기법은 앙상블 기법 중 가장 간단한 기법으로 분류(Classification) 문제에서 활용된다.

__"각각의 단일 모델들이 예측한 분류 중 가장 많은 비율을 차지한 레이블을 최종 결과로 예측한다"__ 가 바로 보팅 방식의 개념이다.

​	

예를 들어 1,2,3 중 하나로 분류해야 하는 문제를 위해 10개의 단일 모델을 보팅 방식으로 앙상블 하였다고 가정하자.

각 모델들의 예측이 다음과 같다면,

```
1로 예측 : 2개 모델
2로 예측 : 5개 모델
3로 예측 : 3개 모델

1로 예측한 비율 => 0.2
2로 예측한 비율 => 0.5 (win!)
3로 예측한 비율 => 0.3
```

최종 결과를 2로 예측 하는것이 바로 Voting 이다.

​	

이러한 Voting 기법은 크게 2가지 방식의 적용 방식이 존재하는데,

​	

:pencil2: __Hard Voting__ 

- 위에서 예시로 든 상황처럼 각 모델들의 softmax(or logistic) 적용 값에서 가장 큰 값만 참고하여 비율을 계산

> ex) A, B, C 모델의 softmax 적용 값이 다음과 같다면
>
> A 모델 = {1일 확률: 0.7 , 2일 확률: 0.2 , 3일 확률: 0.1} 
>
> B 모델 = {1일 확률: 0.4 , 2일 확률: 0.3 , 3일 확률: 0.3} 
>
> C 모델 = {1일 확률: 0.0 , 2일 확률: 0.9 , 3일 확률: 0.1}
>
> ​	
>
> 각 모델의 max 분류만 참고하여 
>
> __"A번 모델 = 1이라 예측"__
>
> __"B번 모델 = 1이라 예측"__
>
> __"C번 모델 = 2이라 예측"__  
>
> 와 같이 생각하여 가장 비율이 큰 `1` 을 최종 분류로 결정하는 방식으로 voting을 진행

​	

:pencil2: __Soft Voting__ 

- hard voting 보다 조금 더 정교한 계산 방식으로,  softmax(or logistic) 적용 값을 모두 참고하여 비율을 계산

> ex) A, B, C 모델의 softmax 적용 값이 다음과 같다면
>
> A 모델 = {1일 확률: 0.7 , 2일 확률: 0.2 , 3일 확률: 0.1} 
>
> B 모델 = {1일 확률: 0.4 , 2일 확률: 0.3 , 3일 확률: 0.3} 
>
> C 모델 = {1일 확률: 0.0 , 2일 확률: 0.9 , 3일 확률: 0.1}
>
> ​	
>
> 각 모델의 softmax 값을 모두 참고하여 
>
> __"1이라 예측한 softmax 값 총합 = 0.7(A) + 0.4(B) + 0.0(C) = 1.1"__
>
> __"2이라 예측한 softmax 값 총합 = 0.2(A) + 0.3(B) + 0.9(C) = 1.4"__
>
> __"3이라 예측한 softmax 값 총합 = 0.1(A) + 0.3(B) + 0.1(C) = 0.5"__  
>
> 와 같이 생각하여 가장 총합이 큰 `2` 를 최종 분류로 결정하는 방식으로 voting을 진행

​	

---

### :radio_button: 2. Bagging <a id="idx4"></a>

​	

Bagging 기법은 [Random Forest 개념 정리](https://ineed-coffee.github.io/posts/RandomForest/) 에서도 자세히 다뤘지만,

`Bootstrapping` + `aggregating` 의 합성 용어이다.

​	

__Boostrapping__ 이란 통계학 용어로, 전체 집합에서 무작위 복원추출을 통해 여러 부분집합을 만드는 행위를 말한다.

예를들어 `[1,2,3,4,5]` 라는 전체 데이터셋이 있을때 무작위 복원추출을 통하여 크기가 3짜리인 부분 데이터셋 `[3,1,3]` , `[2,5,1]` , `[4,5,5]` 등등을 만드는 것이 부트스트래핑이다.

이러한 행위의 목적은 전체 집합의 각기 다른 부분 집합을 통해 여러 모델들을 학습하게 되면 정답에 대한 편항을 증가시키는 효과가 있어 일반화 성능에 도움이 되기 때문이다.

​	

![boostrap](../assets/bagging1.PNG)

​	

__Aggregating__ 이란 '집계하다' 라는 의미를 가진 광범위한 용어로 평균이나 최빈값 등을 도출하는 동작을 말한다.

Bagging 에서의 집계란 위의 Boostrapping 을 통해 생성된 각기 다른 데이터셋으로부터 학습한 여러 모델들의 아웃풋을 집계하여 최종 예측값/분류값을 도출하는 과정을 말한다.

학습의 목적이 Prediction / Classification 인지에 따라 집계하는 방식이 다른데, 가장 많이 활용되는 방식은 다음과 같다.

​	

:pencil2: __Prediction__ 

>  __Averaging : Bagging을 통해 엮인 각 모델들의 출력값의 평균을 최종 출력으로 사용한다.__ 
>
> if 
>
> Model_1 ==> 5.5
>
> Model_2 ==> 7
>
> Model_1 ==> 4.5
>
> Final_output = (5.5 + 5 + 4.5)/3 = 5.0

​	

:pencil2: __Classification__ 

>  __데이터 성격에 맞는 Voting 방식을 택한다.__ 
>
> FYI, Random Forest 모델은 각 의사결정나무의 출력을 Hard-Voting을 통해 집계한다.

​	

***

### :radio_button: 3.Boosting <a id="idx5"></a>

​	

Boosting 기법은 Bagging 과 다르게 여러

`Bootstrapping` + `aggregating` 의 합성 용어이다.



---


### :radio_button: 참고자료 <a id="idx6"></a>

- [나의 첫 머신러닝/딥러닝](https://wikibook.co.kr/mymlrev/) Chapter 4.6 


