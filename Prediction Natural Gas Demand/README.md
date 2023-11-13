# 정리

## 천연가스 수요 예측 AI 모형 개발
* SARIMAX 모형
  * 외생변수 '평균기온' 투입
  * 평균기온과 천연가스 수요의 상관관계와 인과관계가 있음을 통계적 검정을 통해 알 수 있었고,
    관련 논문을 통해 확인할 수 있었다.

## 파일 세부내용
* 01.data_prepare.ipynb : 제공 데이터와 외부 데이터 병합
* 02-1.EDA_ARIMA.ipynb : SARIMAX 모형을 통한 EDA
* 02-2.EDA_external_data.ipynb : 외부 데이터 EDA
* 03.temperature_data_pred.ipynb : 외생변수 투입을 위해 rophet을 활용한 평균기온 예측
* 04.Modeling.ipynb : 모형 구축



