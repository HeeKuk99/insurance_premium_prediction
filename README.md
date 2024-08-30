# insurance_premium_prediction
## 프로젝트 주제 : 신규 보험 가입 고객 유치를 위한 예상 보험료 측정 진단  
## 프로젝트 기한 2024.3 ~ 2024.6
## 분석 방법
### data 구성 확인
'Medical Cost Personal Datasets'  
-> Brett Lants가 쓴 'Machine Learning with R'에서 제공하는 insurance data  
-age, sex, bmi, children, smoker, region, charges 7가지 칼럼으로 구성  
![image](https://github.com/user-attachments/assets/8afb8d3e-2a2e-4259-ac9e-653dacea54dd)  
-dataset의 값 개수(count), mean, 표준편차(std), minimun, maximun, 백분위수 한눈에 보기  
![image](https://github.com/user-attachments/assets/1587a6f6-d0ff-4c0c-a2a6-a3ff2ca0a2d3)  
### data 전처리 및 시각화
#### data 전처리
-1개의 invalid value 제거  
-missing value 존재하지 않음  
-bmi, charges 칼럼에서 standard scalar 이용하여 outlier 찾아 제거
#### data 시각화
-categorical variables(sex, smoker, region)시각화  
-quantative variables(children, age, bmi, charges)시각화 
-charges(target variable) 중심의 데이터 연관성 분석  
-numerical columns 간 연관성  
  numerical columns 중에는 age(0.3), bmi(0.2)가 charges와 연관성이 높은 편이다.
  categorical columns는 레이블 인코딩(string>float 변환)을 하더라도 연관성을 계산하기는 어렵다.  
### label encoding
-sex : female(0), male(1)  
-smoker : n0(0), yes(1)
-region : northeast(0), northwest(1), southeast(2), southwest(3)  
-label : High(0), Low(1)
### data split
-data 칼럼 나누기(원인-결과)  
  원인 : 'sex', 'smoker', 'region', 'age', 'bmi', 'children'  
  결과 : 'charges'
-split data (train : test = 0.8 : 0.2)
-results :  
Training set : 1069  
Test set : 268  
Trainig target variable: : 1069  
Testing target variable : 268  
### 모델 학습-진료비 예측
![image](https://github.com/user-attachments/assets/e0d218e1-0773-46d1-938d-37e9c7b494c3)  
![image](https://github.com/user-attachments/assets/c75fb714-eadc-4313-be77-e98540e61643)  
![image](https://github.com/user-attachments/assets/1230535f-6c6d-4b93-9101-ce42cb723bb8)  
### 모델 평가
![image](https://github.com/user-attachments/assets/e56d5650-b630-41e9-9bce-20f8144366e3)
### 결과 확인
-가장 성능이 좋은 Gradient Boosting을 선택 후 feature importance 확인  
smoker: 0.6709143170466134  
bmi: 0.188440959726968  
age: 0.12287076244893755  
children: 0.012763821714206796  
region: 0.003859842101419106  
sex: 0.001150296961855103  
-전체 데이터셋에 대해 예측 수행  
![image](https://github.com/user-attachments/assets/41d7989b-732d-4be2-b966-93ae2d23fc1a)  
### classification 기준 설정
-charges 칼럼을 High/Low로 분할  
charges 칼럼을 변화율이 가장 큰 구간을 기준으로 'High'&'Low'label로 나눈다.  
Low charges 965, High charges 137로 약 9 : 1의 비율로 데이터가 나뉜다.  
![image](https://github.com/user-attachments/assets/49a9604a-9064-48cc-8976-33cac47dd9e1)  
### data split
-data 칼럼 나누기(원인-결과)  
  원인 : 'sex', 'smoker', 'region', 'age', 'bmi', 'children'  
  결과 : 'label'
-split data (train : test = 0.8 : 0.2)
-results :  
Training set : 953  
Test set : 239  
Trainig target variable: : 953  
Testing target variable : 239  
### 모델 학습 및 평가-High/Low classification
![image](https://github.com/user-attachments/assets/87927189-a542-411f-8819-d2d00e323dba)  
### 결과 확인
-가장 성능이 좋은 Random Forest를 선택 후 feature importance 확인  
smoker: 0.4829974565260843  
bmi: 0.21519401748621855  
age: 0.1836707425364386  
children: 0.06010553360356189  
region: 0.03812158569489455  
sex: 0.019910664152802182  
-전체 데이터셋에 대해 예측 수행  
![image](https://github.com/user-attachments/assets/60d77fcd-25dd-4875-8485-04342ea338ae)
### 최종 결론
![image](https://github.com/user-attachments/assets/4bb44948-f9da-4295-bafd-7d3b5febafd0)
