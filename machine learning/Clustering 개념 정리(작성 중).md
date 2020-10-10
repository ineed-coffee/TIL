# :mag: Index

- [제목1](#idx1) 
- [제목2](#idx2) 
- [제목3](#idx3)
- [제목4](#idx4) 
- [제목5](#idx5)
- [제목6](#idx6)
- [제목7](#idx7)
- [제목8](#idx8)
- [제목9](#idx9)

---



### :radio_button: 제목1 <a id="idx1"></a>





---


### :radio_button: 제목2 <a id="idx2"></a>





---


### :radio_button: 제목3 <a id="idx3"></a>





---


### :radio_button: 제목4 <a id="idx4"></a>





---


### :radio_button: 제목5 <a id="idx5"></a>





---


### :radio_button: 제목6 <a id="idx6"></a>





---


### :radio_button: 제목7 <a id="idx7"></a>

__클러스터와 데이터 사이의 거리를 측정하는 방법들__ 

군집 A 와 데이터 B의 거리를 측정한다 생각할때

- min distance - 군집A 내에서 B에 가장 가까운 데이터 사이의 유클리디안 거리를 사용
- max distance - 군집A 내에서 B에 가장 먼 데이터 사이의 유클리디안 거리를 사용 
- centroid distance - 데이터 B가 특정 군집에 속한 데이터라면 군집의 중심끼리의 거리를 사용 __(가장 일반적)__ :star: 
- group average distance (fully-connected) - 군집 A 와 B가 속한 군집 사이 모든 데이터들 간의 거리 합을 사용



---


### :radio_button: 제목8 <a id="idx8"></a>





---

### :radio_button: 군집화 알고리즘 종류 <a id="idx9"></a>

- __K-means__ 
  	- K : 클러스터 개수
   - K 개의 클러스터 내 거리제곱의 합을 최소로 하는 방향으로 군집화 진행
   - 1. 초기 K 개의 랜덤 Centroid 설정 
     2. 각 Centroid 와 모든 데이터 사이의 거리를 계산
     3. 모든 데이터에 대해 가장 가까운 Centroid 가 속하는 군집에 할당
     4. 각 군집에 대해 새로운 Centroid 계산 (mean_value) -> Centroid 업데이트
     5. ②~④ 의 과정을 반복하며 `|old_Centroid - new_Centroid| < ε` 인 순간 업데이트 종료
  - how many k ? : `1` elbow 기법 , K 증가에 따른 완만 지점 서칭 `2` k= sqrt(n/2) , n= 데이터 사이즈 , 데이터 수가 크지 않을때 유용 
   - 초기 Centroid 에 따라 성능이 차이가 있으므로 위 과정을 여러번 실행하여 각 데이터를 가장 빈번하게 등장하는 군집에 할당하는 식으로 성능 개선 중 (Majority Voting)

- __H-clustering (Hierachical , 계층적 트리 모형)__ 
  - K-clustering 에서 포괄할 수 없는 유형의 데이터나 한계점들을 개선한 군집 방식
  - 클러스터 수를 지정할 필요 없다는것이 대표적 장점
  - 덴드로그램 (Dendrogram) : 데이터들이 묶이는 순서를 나타내는 트리구조로 이를 보며 클러스터 수를 결정할 수 있다.
  - 1. HC는 데이터들 간에 거리 or 유사도가 미리 계산되어 있어야 군집 진행이 가능함
    2. 거리 행렬에서 가장 작은 값을 찾아 두 집단을 한 그룹으로 연결
    3. `N X N` 거리 행렬에서 그룹화 후 `N-1 X N-1` 사이즈 거리 행렬을 다시 계산
    4. __②~③__ 과정을  반복하며 최종적으로 2 집단이 남으면 연결하며 종료
- __DBSCAN__ 
  - eps(epsilon) ? : 특정한 1개의 데이터로부터 떨어진 거리 (사용자가 정하는 기준치)
  - 점 p가 있을때, p로부터 eps 이내에 다른 점들이 MinPts 이상일때 하나의 클러스터로 인식
  - Border point : 본인을 중심으로 조사한 eps로는 클러스터를 이룰 수 없지만 그 속에 코어 포인트가 있는 경우 이러한 데이터를 경계점이라 부름. 
  - 본인이 코어 포인트가 되면서 eps 내에 다른 코어 포인트가 존재하면, 두 클러스터를 병합
  - 어느 클러스터에도 포함되지 않은 데이터들을 Outlier , Noise data 로 취급
  - 