## 최적의 수소충전소 입지 선정

> 201904008 곽재원

## 문서 설명

- 본 프로젝트에 대한 개요은 [수소충전소 최적 입지 선정](https://github.com/jaewonE/Selecting-the-optimal-hydrogen-charging-station-location/blob/main/%EC%88%98%EC%86%8C%EC%B6%A9%EC%A0%84%EC%86%8C%20%EC%B5%9C%EC%A0%81%20%EC%9E%85%EC%A7%80%20%EC%84%A0%EC%A0%95.md)에 기술되어 있다.

- 본 프로젝트에서 사용된 원본 데이터에 대한 자세한 설명은 [수소충전소 최적 입지 선정 사용 데이터](https://github.com/jaewonE/Selecting-the-optimal-hydrogen-charging-station-location/blob/main/%EC%88%98%EC%86%8C%EC%B6%A9%EC%A0%84%EC%86%8C%20%EC%B5%9C%EC%A0%81%20%EC%9E%85%EC%A7%80%20%EC%84%A0%EC%A0%95%20%EC%82%AC%EC%9A%A9%20%EB%8D%B0%EC%9D%B4%ED%84%B0.md)에 기술되어 있다.

- 분석 진행과정은 다음과 같다.
  1. data_trans.ipynb: 원본 데이터를 전처리하여 분석에 사용할 수 있는 형태로 변환한다.
  2. create_regression_dataset.ipynb: 전처리된 데이터를 이용하여 회귀분석을 위한 데이터셋을 생성한다.
  3. model.ipynb: 랜덤 포레스트 회귀 모델을 생성하고 평가한다.
  4. get_best_location.ipynb: 생성된 모델을 이용해 수소충전소 부지로 적합한 LPG 충전소와 주유소를 선정한다.
  5. data_visualization.ipynb: 데이터 시각화를 통해 데이터의 특성을 파악한다.

<br>

## 메인 데이터셋 설명

`trans_data/combined_grid_centers.csv`는 lat(위도), long(경도) 지점에서 각각의 요소값을 측정한 값이다. 각각의 요소(열)에 대한 설명은 다음과 같다.

- lat: 위도
- long: 경도
- hydrogen_distance: 가장 가까운 수소충전소까지의 거리
- school_distance: 가장 가까운 학교까지의 거리
- baby_school_distance: 가장 가까운 어린이집 까지의 거리
- elderly_center_distance: 가장 가까운 경로당가지의 거리
- fire_station_distance: 가장 가까운 소방서까지의 거리
- rescue_station_distance: 가장 가까운 구조대 및 안전센터까지의 거리
- traffic_volume: 해당 지점에서의 평균 교통량
- hydrogen_car_count: 해당 구역에서 사용되는 수소차의 개수
- population_density: 해당 구역의 인구밀도

최적의 수소충전소 위치를 선정하기 위해 hydrogen_distance를 종속변수로 하며 school_distance, baby_school_distance, elderly_center_distance, fire_station_distance, rescue_station_distance, traffic_volume, hydrogen_car_count, population_density 변수를 독립변수로 하는 랜덤 포레스트 회귀 모델을 생성하였다.

이때 현재 설치된 수소충전소가 사회적 합의를 통해 결정된 최적의 위치라고 가졍하였기에 hydrogen_distance 값이 작을수록 적합한 수소충전소 위치로 판단하는 지도학습을 진행하였다.
