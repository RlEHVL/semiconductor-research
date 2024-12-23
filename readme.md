# 반도체 연구 (공모전)
**RIEHVL 해설**.  
> 본 목적은 대학 개인 프로젝트로 제출하기 위함으로.  
> 모든 코드는 본인이 작성함

# 공모전 링크
https://dacon.io/competitions/official/236323/overview/description

![image](https://github.com/user-attachments/assets/9596f2d7-d648-46e2-804f-478eda6f7549)

이 그림은 각 변수의 **분포 히스토그램**을 보여줍니다. 

---

## **1. 전반적인 설명**
"이 히스토그램은 데이터에 포함된 입력 변수(`x_0`~`x_10`)와 타겟 변수(`y`)의 분포를 보여줍니다. 각 변수의 분포를 분석함으로써, 데이터가 가지는 특성을 이해하고, 모델이 안정적으로 학습할 수 있도록 전처리 방향을 결정할 수 있었습니다."

---

## **2. 개별 변수 분석**
변수의 특성과 모델 학습에서의 의미를 분석하여 설명합니다.

### **(1) x_0, x_2, x_3**
- **특징**:
  - 대체로 **정규분포**에 가까운 형태를 가집니다.
  - 중심값(평균값)에 데이터가 집중되어 있고, 극단적인 값은 거의 없습니다.
- **해석**:
  - 이 변수들은 변동성이 적고 안정적이므로, 모델 학습에 긍정적으로 기여할 수 있습니다.
  - 추가적인 변환이나 처리 없이도 모델에 바로 사용할 수 있습니다.

---

### **(2) x_1, x_4, x_5, x_10**
- **특징**:
  - 분포가 **비대칭적(Skewed)**입니다.
    - `x_1`: 오른쪽 꼬리가 긴 분포(양의 비대칭).
    - `x_4`, `x_5`, `x_10`: 왼쪽 꼬리가 긴 분포(음의 비대칭).
  - 이상치 또는 극단값이 눈에 띄게 나타나는 변수들입니다.
- **해석**:
  - 분포가 비대칭인 변수들은 **로그 변환** 또는 **정규화**를 통해 분포를 개선할 수 있습니다.
  - 특히 `x_4`, `x_5`, `x_10`은 극단값이 많으므로, 이상치 처리를 통해 모델의 안정성을 높이는 것이 중요합니다.

---

### **(3) x_6**
- **특징**:
  - **이중봉(바이모달 분포)**를 가지며, 두 개의 뚜렷한 데이터 군집이 관찰됩니다.
- **해석**:
  - 이 변수는 특정 공정 조건에 따라 데이터가 두 그룹으로 나뉘는 특성을 가질 가능성이 있습니다.
  - 이 변수에 대해서는 **클러스터링**을 통한 추가 분석이나, 모델이 이 특성을 학습할 수 있도록 그대로 유지하는 방향을 고려할 수 있습니다.

---

### **(4) x_7, x_8, x_9**
- **특징**:
  - 데이터가 특정 구간에 치우쳐 있으며, 완만한 분포를 보여줍니다.
  - 예를 들어, `x_7`은 약간 오른쪽으로, `x_8`은 약간 왼쪽으로 치우쳤습니다.
- **해석**:
  - 이 변수들은 비교적 안정적인 분포를 가지며, 추가적인 변환 없이도 모델 학습에 적합합니다.

---

### **(5) 타겟 변수 y**
- **특징**:
  - `y` 값은 80~90 구간에 대부분 집중되어 있으며, 극단적인 낮은 값(20~70 구간)이 일부 존재합니다.
- **해석**:
  - 타겟 값의 분포가 비대칭적이므로, 극단값이 모델 학습에 미칠 영향을 고려해야 합니다.
  - 극단값 처리를 통해 모델이 정상 범위(80~90)에 집중할 수 있도록 유도할 수 있습니다.

---

1. **"이 히스토그램은 데이터의 각 변수(`x_0`~`x_10`)와 타겟 변수(`y`)의 분포를 시각화한 것입니다."**

2. **정상적인 분포**:
   - "`x_0`, `x_2`, `x_3`는 정규분포에 가까운 형태로, 모델 학습에 안정적으로 기여할 수 있습니다."

3. **비대칭적 분포와 극단값**:
   - "`x_1`, `x_4`, `x_5`, `x_10`는 분포가 비대칭적이며 극단값이 존재합니다. 이 변수들에 대해 로그 변환 또는 이상치 처리를 고려했습니다."
   - "특히, `x_4`와 `x_5`는 타겟 변수와 높은 상관관계를 가지면서도 극단값이 많아 모델 성능에 중요한 영향을 미칠 가능성이 있습니다."

4. **특이 분포**:
   - "`x_6`는 이중봉(바이모달) 분포를 보여, 특정 조건에 따라 데이터가 나뉠 가능성이 있습니다. 이를 그대로 모델에 반영해 학습하도록 설계했습니다."

5. **타겟 변수 y**:
   - "타겟 변수 `y`는 대부분 80~90 구간에 몰려 있으며, 일부 낮은 극단값이 존재합니다. 이를 모델이 올바르게 예측할 수 있도록 이상치 처리를 검토했습니다."

---

![image](https://github.com/user-attachments/assets/185cc738-1a9c-4c67-9b23-dcb5479aadb3)


---

## **1. 박스플롯 구조**
박스플롯에서 주목해야 할 부분:
- **중앙값(Median)**:
  - 박스 내부의 선으로 표시되며, 데이터의 중앙값을 나타냅니다.
- **사분위수(IQR, Interquartile Range)**:
  - 박스의 상단과 하단은 각각 **3사분위수(Q3)**와 **1사분위수(Q1)**를 나타냅니다.
  - IQR = Q3 - Q1
- **Whisker(수염)**:
  - 박스 위아래로 뻗은 선으로, 데이터를 1.5 × IQR 내에서 표시합니다.
  - Whisker 밖의 점들은 **이상치(Outliers)**로 간주됩니다.

---

## **2. 각 변수의 해석**
### **(1) x_0, x_1, x_2, x_3, x_7, x_9, x_8**
- 분포:
  - 이 변수들은 비교적 **정상적인 분포**를 가지고 있으며, 중앙값이 박스의 중간에 위치.
  - 이상치가 거의 없거나 발견되지 않음.
- 해석:
  - 해당 변수들은 데이터의 변동성이 적으며, 대부분의 값이 IQR 범위 안에 포함됨.
  - 학습 모델에 안정적으로 기여할 가능성이 높음.

### **(2) x_4**
- 분포:
  - **중앙값이 박스 하단에 가까움**, 데이터가 약간 왼쪽으로 치우친(Skewed) 분포를 가질 가능성이 있음.
  - Whisker 하단에 다수의 **이상치**가 존재.
- 해석:
  - 이상치가 많이 발견되며, 해당 변수는 특정 극단적인 상황에서 중요한 정보를 나타낼 수 있음.
  - 모델 학습 전에 이상치를 처리(예: 클리핑, 제거)하거나, 로그 변환을 고려할 수 있음.

### **(3) x_5**
- 분포:
  - 중앙값이 비교적 중앙에 위치하나, Whisker 하단에 다수의 **이상치** 존재.
- 해석:
  - x_4와 비슷한 특성을 가지며, 이상치가 결과에 영향을 미칠 가능성이 있음.
  - 이상치 처리 또는 상관관계를 고려한 추가 분석 필요.

### **(4) x_6**
- 분포:
  - Whisker 상단에 다수의 **이상치** 존재.
- 해석:
  - 데이터가 오른쪽으로 약간 치우친(Skewed) 분포를 가질 가능성이 있음.
  - 이상치가 변수의 중요성을 왜곡할 수 있으므로, 처리 필요.

### **(5) x_10**
- 분포:
  - Whisker 하단에 소수의 **이상치**가 존재.
- 해석:
  - 이상치가 비교적 적으며, 대부분의 데이터는 IQR 범위에 포함됨.
  - 해당 변수는 안정적으로 학습 모델에 기여할 가능성이 있음.

---

1. **이상치 제거**:
   - IQR을 기준으로 Whisker 밖의 이상치를 제거.
   - 단, 이상치가 데이터의 중요한 특성을 나타낼 수 있으므로 신중히 처리.
2. **클리핑(값 제한)**:
   - 이상치를 상/하한값(Q1 - 1.5 × IQR, Q3 + 1.5 × IQR)으로 조정.
3. **변환(예: 로그 변환)**:
   - x_4, x_5처럼 이상치가 많은 변수에 로그 변환을 적용하여 분포를 정규화.
4. **모델 기반 처리**:
   - 모델이 이상치를 자연스럽게 학습하도록, 별도의 처리 없이 그대로 유지.

---
1. **"이 박스플롯은 데이터 변수들의 분포와 이상치를 시각적으로 보여줍니다."**
2. **"대부분의 변수는 정상적인 분포를 가지며, 이상치가 적습니다. 그러나 x_4, x_5, x_6 변수에서는 다수의 이상치가 발견되었습니다."**

---

![image](https://github.com/user-attachments/assets/923aa327-38f0-4639-9cb2-7b745b35a6db)

주어진 상관관계 히트맵은 테스트 데이터(`test.csv`)의 각 변수 간 상관관계를 나타냅니다. 상관계수의 값은 -1에서 1 사이의 범위를 가지며, 다음과 같이 해석할 수 있습니다:

---

## **상관관계 해석**
1. **상관계수의 의미**:
   - **양의 상관관계 (+)**: 한 변수가 증가하면 다른 변수도 증가하는 경향이 있음.
   - **음의 상관관계 (-)**: 한 변수가 증가하면 다른 변수는 감소하는 경향이 있음.
   - **상관관계 없음 (0에 가까움)**: 두 변수 간에 선형적인 관계가 거의 없음.

2. **상관계수의 강도**:
   - **0.7 이상 또는 -0.7 이하**: 강한 상관관계.
   - **0.3 ~ 0.7 또는 -0.3 ~ -0.7**: 중간 정도의 상관관계.
   - **0.3 미만 또는 -0.3 초과**: 약한 상관관계.

---

## **히트맵의 주요 해석**
1. **강한 상관관계**:
   - `x_1`과 `x_7`의 상관관계: **0.97** (양의 강한 상관관계).
   - `x_4`와 `x_5`의 상관관계: **-0.98** (음의 강한 상관관계).
   - `x_10`과 `x_5`의 상관관계: **-0.99** (음의 강한 상관관계).

   - **의미**: 
     - `x_1`과 `x_7`은 서로 매우 유사한 패턴을 가지며, 둘 중 하나만 사용하거나 파생 변수(곱)를 생성할 수 있음.
     - `x_4`와 `x_5` 또는 `x_10`과 `x_5`는 음의 강한 상관관계가 있으므로, 모델이 둘의 영향을 상쇄하거나 의존하지 않도록 주의해야 함.

2. **중간 정도의 상관관계**:
   - `x_0`과 `x_3`: **-0.65** (음의 중간 상관관계).
   - `x_2`와 `x_10`: **0.68** (양의 중간 상관관계).

   - **의미**:
     - 중간 정도의 상관관계를 가지는 변수는 개별적으로 의미 있는 정보일 가능성이 있으므로 주의 깊게 다룰 필요가 있음.

3. **약한 상관관계 또는 상관 없음**:
   - `x_2`와 `x_6`: **-0.26** (약한 음의 상관관계).
   - `x_6`과 `x_7`: **0.48** (약한 양의 상관관계).

   - **의미**:
     - 약한 상관관계를 가진 변수는 독립적으로 작용할 가능성이 있으므로, 분석과 모델링에서 중요한 역할을 할 수 있음.

---

![image](https://github.com/user-attachments/assets/3d1edc3b-ee30-41cb-82a3-9faad1e77b31)

히트맵과 타겟 변수의 분포를 분석하는 목적 중 하나는 **과적합(overfitting)을 방지**하고, 데이터의 특성을 정확히 이해하여 모델의 일반화 성능을 높이는 데 있습니다.
---

## **1. 과적합 방지와 데이터 분석**
히트맵과 타겟 분포를 통해 데이터의 특성을 분석하는 목적은 과적합 방지를 포함하여 다음과 같은 이유가 있습니다:

### **(1) 변수 선택**
- 히트맵에서 상관관계를 확인한 이유는, 중복된 정보를 가진 변수들을 제거하거나 새로운 파생 변수를 추가해 모델의 성능을 개선하기 위함입니다.
- 과적합 방지와 관련된 부분:
  - 강한 상관관계를 가진 변수들이 많으면, 모델이 불필요하게 중복 정보를 학습하여 과적합 가능성이 커질 수 있습니다.
  - 반대로, 약한 상관관계를 가진 변수들은 서로 독립적인 정보를 제공하므로 모델 학습에 도움이 됩니다.

### **(2) 타겟 분포 확인**
- 타겟 변수 \(y\)의 분포를 분석한 이유는, 모델이 예측해야 할 값의 범위를 이해하고 데이터의 왜곡(skewness) 여부를 파악하기 위함입니다.
- 과적합 방지와 관련된 부분:
  - \(y\) 값이 대부분 특정 범위(80~90)에 집중되어 있고, 일부 극단값(예: 70 이하)이 존재합니다.
  - 모델이 극단값을 과도하게 학습하지 않도록 **이상치 처리**나 **가중치 적용** 등을 고려할 수 있습니다.

---

## **2. 놓칠 수 있는 추가적인 포인트**
### **(1) 데이터 스케일과 분포**
- 입력 변수(예: \(x_0\) ~ \(x_{10}\))와 타겟 변수(\(y\))의 분포가 서로 다를 경우, 모델이 특정 변수에 지나치게 의존할 가능성이 있습니다.
- 해결 방법:
  - 이미 적용한 **StandardScaler**를 통해 데이터 스케일을 조정하여, 모든 변수가 모델에 균등하게 반영되도록 합니다.
  - 그러나 타겟 변수 \(y\)는 정규화되지 않은 상태로 두는 것이 일반적입니다(왜냐하면 모델이 실제 값에 대해 학습하기 때문).

### **(2) 이상치(outlier)의 영향**
- 타겟 분포에서 확인된 **극단값(예: 20~60 구간의 \(y\))**이 모델 학습에 미치는 영향을 고려해야 합니다.
- 해결 방법:
  - 극단값의 비율이 낮으므로, 모델 학습 시 이러한 값을 제거하거나 **로지스틱 변환**이나 **로그 변환**을 적용할 수 있습니다.

### **(3) 상관관계와 변수의 중요도**
- 상관관계가 높은 변수는 타겟 변수에 대한 높은 설명력을 가질 수 있지만, 실제로는 다른 변수에 의해 설명되거나 중복될 수 있습니다.
- 놓칠 수 있는 부분:
  - 히트맵 상에서는 상관관계가 약한 변수(\(x_6\))가 중요하지 않아 보이지만, 다른 변수들과의 **비선형 관계**에서 중요한 역할을 할 가능성이 있습니다.
  - 상관관계가 낮은 변수라도 모델 훈련 시 중요 변수로 나타날 수 있으므로, **모델의 변수 중요도(feature importance)**를 반드시 확인해야 합니다.

### **(4) 타겟의 비대칭성(Skewness)**
- 타겟 \(y\)가 오른쪽으로 약간 치우친(skewed) 분포를 보이고 있습니다. 
- 놓칠 수 있는 부분:
  - 정규 분포에 가까운 데이터가 모델이 더 안정적으로 학습할 수 있도록 돕습니다. 만약 왜곡된 분포를 가진 데이터를 처리하지 않으면, 예측 결과에서 높은 \(y\) 값만 과도하게 예측될 가능성이 있습니다.
- 해결 방법:
  - 타겟 변수에 **로그 변환**을 적용하여 분포를 정규 분포에 가깝게 만들 수 있습니다.

---

1. **"히트맵과 타겟 분포를 분석한 이유는, 데이터의 특성과 변수 간 관계를 이해하여 모델이 올바르게 학습하도록 돕기 위함입니다."**

2. **히트맵 설명**:
   - "히트맵을 통해 강한 상관관계를 가진 변수들(예: \(x_1\), \(x_7\))을 확인했고, 중복 정보를 줄이기 위해 파생 변수를 생성했습니다."
   - "또한, 상관관계가 낮은 변수(\(x_6\))는 독립적인 정보를 제공할 수 있으므로 모델링에서 중요하게 활용될 가능성이 있습니다."

3. **타겟 분포 설명**:
   - "타겟 변수 \(y\)의 분포를 보면, 대부분 80~90 사이에 몰려 있는 정상 범위지만, 일부 극단값이 존재합니다."
   - "모델이 극단값에 과도하게 의존하지 않도록 이상치 처리를 고민하고, 필요 시 로그 변환을 적용하여 분포를 정규화할 수 있습니다."
---

![image](https://github.com/user-attachments/assets/563eeac8-0ceb-418b-b121-a27f4bd0fe10)
> [Val] DNN Recall: 0.8905
> Model Weights based on Recall: RF=0.25, XGB=0.25, LGBM=0.25, DNN=0.25
> [Val] Ensemble Recall: 0.8955


이 그래프는 **딥러닝 모델(DNN)의 학습과 검증 손실(loss) 변화**를 보여줍니다. 이 그래프를 해석하기 위해 상위 퍼센트 예측값과의 관계를 정리하면 다음과 같습니다.

---

## **그래프 해석**
### **1. Train Loss (왼쪽)**:
- **파란 선**은 학습 데이터에서의 손실(오차) 감소를 나타냅니다.
- 학습 초기에는 손실 값이 매우 크지만, Epoch가 진행됨에 따라 급격히 감소한 후 안정화.
- **해석**:
  - 모델이 학습 데이터를 점점 잘 예측하게 되었음을 의미합니다.

### **2. Validation Loss (오른쪽)**:
- **주황 선**은 검증 데이터에서의 손실(오차) 감소를 나타냅니다.
- 초기에는 손실이 크지만 빠르게 감소한 후, 안정적인 값을 유지.
- **해석**:
  - 모델이 검증 데이터에서도 과적합 없이 적절하게 학습했음을 의미합니다.

### **결론**:
- Train Loss와 Validation Loss 모두 안정적으로 수렴했으며, 두 값이 비슷한 수준으로 유지되고 있습니다.
- 이는 모델이 학습 데이터에 과적합하지 않고 일반화 성능을 유지하고 있음을 시사합니다.

---

1. **그래프의 의미**:
   - "이 그래프는 딥러닝 모델의 학습 및 검증 손실 변화를 보여줍니다. 손실 값이 안정적으로 감소하고 검증 데이터에서도 낮은 손실 값을 유지하고 있어 모델의 일반화 성능이 우수함을 확인할 수 있습니다."

2. **상위 퍼센트와의 연결**:
   - "이 그래프는 모델의 전체 성능을 나타내며, 상위 10% 예측값의 Recall 성능도 이러한 안정적인 학습 결과에서 비롯됩니다."
   - "구체적인 상위 퍼센트 Recall은 별도의 계산을 통해 검증되었으며, 이를 통해 최적의 결과를 도출했습니다."

---

# 코멘트
> 순수 혼자만의 힘.  
> 조력자 0명.  
> 이론 공부 10분 실무 독학 공부 12시간..   
> (나머지 시간 c언어)