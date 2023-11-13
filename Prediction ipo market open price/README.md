# Summary

## 공모주 크롤링
* selenium, BeautifulSoup을 사용하여 크롤링 작업 수행
  * 사이트 HTML 구조가 특이하여 크롤링 하는데에 시간을 많이 투자함.
  
## 공모주 데이터 정제 및 EDA
* 도메인 지식을 활용하여 데이터 정제 수행

## 공모주 모형
* pycaret 사용한 앙상블 모델 생성 수행
  * Ensemble Model 사용 (RF, ET, XGB, GBDT)
  * 이상치가 존재하여 robust한 metrics, RMSLE 사용
  
