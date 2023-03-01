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
    - 기준 모델(accuracy_score) : scikit-learn
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


- 표본 선정
    - 원본 데이터는 루즈벨트 국유림 4개 지역(Rawah/ Neota / Comanche Peak/ Cache la Poudre Wilderness Area)으로 구성되어 있으나, 본 연구에서 필요한 폰데로사 소나무의 경우 2개 지역(Comanche Peak/ Cache la Poudre Wilderness Area)에서만 자라고 있으므로 2개 지역에 대해서만 머신러닝을 진행
    - 원본 데이터 관측치 : 581,012개 / 프로젝트 데이터 표본 : 290,332개
    - 중복치와 결측치는 확인 결과 없음
    - 이상치는 수치데이터는 boxplot을 통한 검토를 통하여 제거하지 않기로 결정
-----

### 분류모델 학습 및 성능 확인




----
### 모델 해석



----
### 한계점 및 해결방법





