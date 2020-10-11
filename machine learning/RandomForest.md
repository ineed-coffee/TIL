# :mag: Index

- [랜덤 포레스트(Random Forest)는 무엇일까?](#idx1) 
- [랜덤 포레스트의 핵심 : bagging (bootstrap + aggregate)](#idx2) 
- [랜덤 포레스트의 중요 매개변수](#idx3)
- [sklearn 라이브러리를 활용한 랜덤 포레스트](#idx4) 
- [Reference](#idx5)



---



### :radio_button: 랜덤 포레스트(Random Forest)는 무엇일까? <a id="idx1"></a>



이전에 [의사결정 나무 (Decision Tree)](https://github.com/ineed-coffee/TIL/blob/master/machine%20learning/DecisionTree%20%EA%B0%9C%EB%85%90%20%EC%A0%95%EB%A6%AC.md) 에 대한 개념을 정리하였는데 이름에서도 알 수 있듯이 __무작위 숲 (Random Forest)__ 는 의사결정 나무를 활용한 모델의 한계점 및 취약점을 극복하기 위한 __개선&확장 알고리즘__ 이다. 



의사결정나무는 그 학습 과정에서도 알 수 있듯이 트리의 높이에 따라 과적합 학습으로 빠질 수 있는 정도가 차이가 크고, 그에 따라 특이값에 상당히 민감한 모델이 되기 쉽다. 트리의 높이를 제한하거나 만들어진 트리에서 오류를 최소로 하는 가지를 몇개 잘라내는 방식으로 일반화 성능을 높일 수 있지만 데이터 자체가 잘 문서화되어 있어야 그나마 효과를 볼 수 있어 다양한 데이터에 활용하기 어렵다.



> 그럼 무작위 숲은 이러한 의사결정나무의 한계점을 어떻게 극복하는것일까?



우리가 쇼핑몰에서 어떤 옷을 사려하는데 상품평이 3개만 달려있고 3개 모두 긍정적인 아이템과 , 상품평이 7천개 이상 달려있고 긍정/부정의 리뷰가 고루 있는데 긍정적인 리뷰가 조금 더 많은 아이템이 있다고 하면 우린 어떤 아이템을 좋은 상품이라 생각할까?



__당연히 후자!__ 각기 다른 취향과 체형을 가진 사람들로부터 평가 받은 상품에 대한 리뷰를 훨씬 신뢰할 수 있다고 생각할것이다. 바로 이러한 점이 랜덤 포레스트에서 취하고자 하는 방식이다. 표면적인 이해를 돕자면, 랜덤 포레스트를 통해 모델을 구성하는 방식은 학습을 위해 만들어 놓은 데이터셋에서 조금씩 조금씩 데이터 일부를 뽑아 의사결정 나무들을 만들고, 각 의사결정 나무들에게 같은 예측 데이터셋을 입력으로 넣어주어 어떤 결과를 예측하는지 종합하여 판단한다. 분류 문제의 경우 더 많은 의사결정 나무들이 선택한 카테고리를 , 회귀 문제의 경우 각 의사결정 나무들이 예측한 값의 평균을 최종적으로 모델의 출력으로 결정한다.  



__※ 무작위 숲의 이해를 돕기 위한 그림__ 

![무작위 숲](data:image/png;base64,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)

출처 [https://kuduz.tistory.com/1202](https://kuduz.tistory.com/1202)



---

### :radio_button: 랜덤 포레스트의 핵심 : bagging (bootstrap + aggregate) <a id="idx2"></a>



> 어떻게 생각해보면 당연한 말 같다. 모델 하나만의 결과는 신뢰도가 낮으니 모델을 여러개 만들어서 출력을 종합해보자! 
>
> 근데 그럼 트리만 여러개 만들면 끝인걸까?



각각의 트리가 비슷한 모양을 가진다면, 조금더 정확히는 숲을 이루는 나무들이 서로 상관화(correlated)되어 있다면 트리가 아무리 많아도 성능 개선을 기대할 수 없다. 따라서 단순히 `숲` 이 아니라 `무작위 숲` 이 되기 위해서는 트리마다 생김새가 다르도록 __랜덤성__ 을 가진 나무들로 구성되어야 한다.



표면적으로만 이해하기에는 __'그냥 트리 여러개 만들어서 평균이나 빈번값 활용하는 그거'__  정도로 이해할 수 있겠지만 사실 랜덤 포레스트의 핵심 키워드는 바로 __`bagging`__ :star: ​이다.



bagging 을 설명하기 앞서 랜덤 포레스트 알고리즘과 같이 기존 알고리즘들을 엮어 활용하는 것을 __앙상블(ensemble) 기법__ 이라고 하는데 bagging 은 이러한 앙상블 기법 중 하나이다. 카테고리 제목에서도 알 수 있듯이 bagging 이라는 단어는 bootstrapping + aggregating 을 합쳐놓은 용어이다. 두 단어는 간략히는 각각 다음과 같은 의미를 갖는 용어인데,

```
Bootstrapping : 전체 집합에서 무작위 복원추출을 통해 여러 부분집합을 만드는 행위
Aggregating : '집계한다' 는 광범위한 용어로 평균이나 최빈값 등을 도출하는 행위
```



두 용어 중에서 더 큰 의미를 가지는 단어는 bootstrapping 이다. 숲을 이룰 각 나무를 학습하는데 쓰일 데이터셋으로 학습데이터 전체를 사용하지 않고 그중 일부만 활용하는 것인데 그 일부를 무작위로 복원추출하여 생성하겠다는 것이다. 만약 100개의 학습 데이터가 있다고할때 그 중 20개의 데이터만 뽑아 하나의 나무를 구성하고 다시 20개의 데이터를 100개에 포함시킨 뒤 또 랜덤하게 20개를 뽑아 다음 나무를 생성하며 각 나무는 서로 다른 모양의 가지와 높이를 구성하게 된다. 



이 두 용어를 합친 bagging 기법은 다음과 같이 정리할 수 있다.

__`"머신 러닝에서 앙상블 기법 중 하나인 bagging 은 boostrapping을 통해 train_set 에서 무작위 복원 추출을 통해 기저 모델을 생성하고 , 이러한 기저 모델을 어려개 생성하여 이들의 출력 결과를 aggregating 하여 학습하는 알고리즘이다."`__ 



__※ 사실 bagging 이외에도 랜덤포레스트의 각 나무는 임의 노드 최적화라는 방법을 통해 더욱 일반화 성능을 얻고 있는데 이 정리에서는 bagging 에 대해서만 다루었다.__ 



---


### :radio_button: 랜덤 포레스트의 중요 매개변수 <a id="idx3"></a>

- __숲의 크기__ :star:
  - 숲을 구성할 나무의 수를 뜻하는 매개변수로 나무의 수가 증가할수록 일반화 성능이 우수하지만 , 훈련과 검증의 시간은 오래걸린다.

- __각 트리의 높이__ :star: ​
  - 숲을 구성하는 각 나무들의 최대 깊이를 설정하는 매개변수로 과소적합&과대적합과 밀접한 관계를 가지므로 적절한 높이를 통해 학습하는 것이 중요하다.
- __임의성의 정도와 종류__ 
  - 전체 데이터에서 부분 데이터를 추출하는 과정에서 어떤 분포 함수를 적용하는지에 따라 랜덤성에 차이가 있다. 깊은 설명은 생략
- __각 트리의 특징 벡터 선정__ 
  - 참고내용에서 언급한 부분, 실제 각 트리는 부분 데이터 중에서도 모든 특성을 다 학습에 활용하지 않고 각 노드에서 일부 특성만을 고려하여 분기하는데 이때 활용되는 훈련 목적 함수의 종류에 따라 일반화 성능의 차이가 있다. 깊은 설명 생략



---


### :radio_button: sklearn 라이브러리를 활용한 랜덤 포레스트 <a id="idx4"></a>





---


### :radio_button: Reference <a id="idx5"></a>

- [https://ko.wikipedia.org/wiki/%EB%9E%9C%EB%8D%A4_%ED%8F%AC%EB%A0%88%EC%8A%A4%ED%8A%B8#%ED%9B%88%EB%A0%A8_%EB%AA%A9%EC%A0%81_%ED%95%A8%EC%88%98](https://ko.wikipedia.org/wiki/%EB%9E%9C%EB%8D%A4_%ED%8F%AC%EB%A0%88%EC%8A%A4%ED%8A%B8#%ED%9B%88%EB%A0%A8_%EB%AA%A9%EC%A0%81_%ED%95%A8%EC%88%98)
- http://hleecaster.com/ml-random-forest-concept/
- https://lsjsj92.tistory.com/542




### 
