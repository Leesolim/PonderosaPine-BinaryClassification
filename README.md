# PonderosaPine-Binary Classification
----
### 문제인식 및 가설 설정
- 우리나라의 고유수종 구상나무(Korea Fir)는 기후변화로 인해서 2013년 부터 집단고사가 진행되고 있고, 현재 구상나무숲 복원을 위한 노력을 하고 있습니다. 집단 고사 원인은 적설량 부족으로 인한 고산지역의 건조현상으로 추정 중입니다. 구상나무처럼 기후 변화 등으로 인하여 자연스럽게 자라던 나무들에게 인위적인 도움이 점점 필요해지고 있고, 적절한 도움을 주기 위해서는 각 나무의 생육 환경에 대한 선행연구가 필요합니다. 나무수종별로 데이터가 체계적으로 정리되어 있을수록, 효과적인 산림 계획 수립 및 의사결정을 할 수 있을 것입니다.

- 우리나라 자료면 더 좋았겠지만, 이번 연구에서는 콜로라도 루즈벨트 국유림 4개 지역에서 생장하고 있는 나무에 대한 데이터를 이용하여 연구를 진행하고자 합니다. (kaggle_Forest Cover Type Prediction) 루즈벨트 국유림은 로지폴 소나무와 가문비나무/전나무가 약 85% 차지하고 있습니다. 나무들의 생육환경 연구를 통해서 숲의 다양성을 유지하기 위하여 이번 연구에서는 세번째로 많은 폰데로사 소나무의 생육환경에 대한 연구를 진행하고자 합니다.

- 이진 분류로 타겟은 폰데로사 소나무(Yes, 1), 폰데로사 소나무 이외의 나무(No, 0)로 설정하고, 나무들의 생육환경에 대한 가설을 검토하려고 합니다.
    - 가설1. 폰데로사 소나무가 잘 자라는 위치(고도)가 있을 것이다.
    - 가설2. 폰데로사 소나무가 잘 자라는 토양이 있을 것이다. 

----
### 프로젝트 진행 과정
- 데이터 전처리 : pandas, numpy
- 머신러닝 분류 모델 학습학습 및 성능 확인 
    - 최빈값 기준 모델(accuracy_score) : scikit-learn
    - 결정트리 모델, 랜덤포레스트 모델 : scikit-learn
    - 그레디언트 부스팅 모델 : xgboost
- 모델해석
    - 특성 중요도 : matplotlib
    - PDP : pdpbox

----
### 데이터셋 설명
- 캐글 원본 데이터 : Forest Cover Type Prediction (https://www.kaggle.com/datasets/uciml/forest-cover-type-dataset)
    - Elevation - Elevation in meters
    - Aspect - Aspect in degrees azimuth
    - Slope - Slope in degrees
    - Horizontal_Distance_To_Hydrology - Horz Dist to nearest surface water features
    - Vertical_Distance_To_Hydrology - Vert Dist to nearest surface water features
    - Horizontal_Distance_To_Roadways - Horz Dist to nearest roadway
    - Hillshade_9am (0 to 255 index) - Hillshade index at 9am, summer solstice
    - Hillshade_Noon (0 to 255 index) - Hillshade index at noon, summer solstice
    - Hillshade_3pm (0 to 255 index) - Hillshade index at 3pm, summer solstice
    - Horizontal_Distance_To_Fire_Points - Horz Dist to nearest wildfire ignition points
    - Wilderness_Area (4 binary columns, 0 = absence or 1 = presence) - Wilderness area designation
        - Area1 - Rawah
        - Area2 - Neota
        - Area3 - Comanche Peak
        - Area4 - Cache la Poudre 
    - Soil_Type (40 binary columns, 0 = absence or 1 = presence) - Soil Type designation
    - Cover_Type (7 types, integers 1 to 7) - Forest Cover Type designation
        - 1 - Spruce/Fir(가문비나무/전나무)
        - 2 - Lodgepole Pine(로지폴 소나무)
        - 3 - Ponderosa Pine(폰데로사 소나무)
        - 4 - Cottonwood/Willow(마루나무/버드나무)
        - 5 - Aspen(사시나무)
        - 6 - Douglas-fir(미송)
        - 7 - Krummholz(작은 나무숲)


- 데이터 선정
    - 원본 데이터 관측치(581,012개)
        - 루즈벨트 국유림 4개 지역(Rawah/ Neota / Comanche Peak/ Cache la Poudre Wilderness Area)으로 구성
        - 30m x 30m 면적을 기준으로 나무 종류 식별
    - 프로젝트 데이터 관측치(290,332개)
        - 본 연구에서 필요한 폰데로사 소나무의 경우 2개 지역(Comanche Peak/ Cache la Poudre Wilderness Area)에서만 자라고 있으므로 2개 지역에 대해서만 머신러닝을 진행
        - 중복치와 결측치는 확인 결과 없음
        - 이상치는 수치데이터는 boxplot을 통한 검토를 통하여 제거하지 않기로 결정
-----

### 분류모델 학습 및 성능 확인
- 분석 기법
    - 폰데로사 소나무 여부를 확인하는 이진 분류 문제로 트리기반 모델을 학습
    - 타겟 데이터(Yes : 0.123, No : 0.877)는 불균형 데이터이므로 하이퍼 파라미터를 조정하여 모델을 학습함(class_weight, scale_pos_weight)
    - 최빈값 기준 모델(accuracy_score) : scikit-learn
    - 결정트리 모델, 랜덤포레스트 모델 : scikit-learn
    - 그레디언트 부스팅 모델 : xgboost


- 모델 학습 성능 확인
    - 평가지표(Accuracy, Precision, Recall, F1-score)에서 우수성을 나타낸 Gradient Boosting 모델 선택
        
         | 분류평가지표 | 기준모델 | Decision Tree | Random Forest | Gradient Boosting |    
         |:---:|:---:|:---:|:---:|:---:|     
         |Accuracy|0.88|0.97|0.98|0.99|    
         |Precision|0|0.87|0.90|0.94|    
         |Recall|0|0.93|0.96|0.97|    
         |F1-score|0|0.90|0.93|0.95|    

- 모델 성능 개선 및 일반화 성능확인
    - 숲 조성에는 많은 시간과 비용이 발생하므로, Yes(1)라고 예측했는데 실제로는 No(0)인 경우가 치명적인 오류라고 판단
         ![image01](https://user-images.githubusercontent.com/109954540/222321865-aa46b198-0c8b-4f6c-b896-9286dc782433.png)

    - 베이지안 튜닝을 통하여 Gradient Boosting 모델의 성능을 개선하고 일반화 성능을 테스트함
         | 분류평가지표 | 개선 전(검증 데이터) | 개선 후(검증 데이터) | 일반화(테스트 데이터) |  
         |:---:|:---:|:---:|:---:|     
         |Accuracy|0.99|0.99|0.99|    
         |Precision|0.94|0.95|0.96|    
         |Recall|0.97|0.97|0.98|    
         |F1-score|0.95|0.96|0.97|
----
### 결과 정리(가설검정 및 모델 해석)
   ![image](https://user-images.githubusercontent.com/109954540/222322451-cd95c4cd-5639-4884-b88a-2613305ae41b.png)
   ![image](https://user-images.githubusercontent.com/109954540/222322988-163838bf-2e02-4c62-92a8-673e4db47684.png)
   ![image](https://user-images.githubusercontent.com/109954540/222323002-1850d8d1-fb3d-4cbb-af99-90fbcf4ddded.png)
    
- 폰데로사 소나무의 생육환경
    - 루즈벨트 국유림 : Comanche Peak/ Cache la Poudre Wilderness Area
    - 고도
        - 2000m~2800m이하까지 생가능
        - 2100m ~ 2500m까지의 높이를 가장 선호
    - 토양
        - Soil_Type(1, 2, 3, 4, 5, 6, 10, 11, 12, 14, 16, 17)에서 생육 가능
        - Type2(Vanet - Ratake families), Type 4(Ratake family)의 토양 선호

----
### 프로젝트 한계점
- 머신러닝의 예측 성능이 너무 높으므로 정보 누수 여부를 확인할 필요가 있음
- 해외 데이터이므로 우리나라 구상나무에 적용하는 것에는 한계가 있음 
- 미래의 생육환경까지 고려하여 산림조성 계획 수립 및 의사결정에 활용하기 위해서는 기후 변화 예측 데이터까지 고려가 필요



