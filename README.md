# 채무 불이행 여부 예측 (Dacon 해커톤, 2025.02.03 ~ 2025.03.31)

## 📌 프로젝트 개요
이 프로젝트는 Dacon "채무 불이행 여부 예측" 해커톤에서 진행되었습니다.  
금융 데이터를 활용하여 고객의 **채무 불이행 여부(0 또는 1)를 예측하는 분류 문제**를 해결하는 것이 목표였습니다.  

---

## 🏆 최종 성과
- **데이콘 해커톤 12위 / 930명 중**(현재 진행 중)
- **AUC 기준 최적 모델(DL) 성능: 0.638**
- **머신러닝과 딥러닝 기법을 비교하여 최적 솔루션 도출**

---

## 🛠 사용 기술
### 머신러닝 모델
- **Logistic Regression**
- **SVC (Support Vector Classifier)**
- **RandomForest**
- **LightGBM**
- **XGBoost**
- **CatBoost** (최종 선정 모델)

### 하이퍼파라미터 최적화 방법
- **Random Search**
- **Grid Search**
- **Bayesian Search**(최종 최적화 기법)

### 딥러닝 모델
- 다양한 **다층 신경망 (MLP)** 구조 실험
- 최적 성능을 낸 **단층 신경망 (Input - 256 - Output)**
- **Adam Optimizer**
- **Binary Cross-Entropy Loss**
- **EarlyStopping 적용**
- **L2 정규화, Dropout 실험** (성능 하락으로 미적용)

---

## 📊 데이터 전처리 및 변수 선택
1. **스케일링 비교**:  
   - `StandardScaler`, `MinMaxScaler`, `RobustScaler` 적용  
   - **큰 차이가 없어 StandardScaler 최종 선택**  

2. **불균형 데이터 처리**:  
   - `SMOTE` 기법을 사용했으나 오히려 AUC 점수 하락  
   - **SMOTE 미적용**  

3. **변수 중요도 분석을 통한 특성 선택**
   - **각 머신러닝 모델 별 변수 중요도 분석**
   - **'대출 목적' 컬럼(Object) 제거** → AUC 최고 점수  
   - **'현재 직장 근속 연수' 컬럼(Object) 추가 제거** → AUC 2번째 최고 점수  

---

## 📈 모델 실험 및 결과

### 1️⃣ 머신러닝 모델 실험  
- **Baseline 모델**로 로지스틱 회귀, SVC, 랜덤포레스트, LightGBM, XGBoost, CatBoost를 기본 파라미터로 테스트  
- **RandomizedSearchCV, GridSearchCV, BayesSearchCV**을 활용하여 `RandomForest`, `LGBM`, `XGB`의 하이퍼파라미터 최적화  
- **'대출 목적' 변수를 제거했을 때, CatBoost 모델이 가장 높은 점수 기록**  

---

### 2️⃣ 딥러닝 모델 실험  
- **다층 신경망(MLP) 구조**: 다양한 깊이(0-10층), 노드 수(1-1024), 정규화 기법(L2, Dropout) 실험  
- **에포크(epochs), 학습률(learning rate), 배치 크기(batch size) 등 다양한 실험 진행**  
- **최적 성능을 기록한 구조: 단층 신경망 (Input - 256 - Output)**
- **L2 정규화 및 Dropout을 적용하면 오히려 성능이 저하됨**  
- **'대출 목적' 컬럼 제거 후 성능 상승,
- 다음으로 결과에 적은 영향을 끼친 **'현재 직장 근속 연수'컬럼 제거 시 점수 하락**  
