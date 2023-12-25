# Contest Objetive
치과 구강이미지 합성 데이터 분양의 헬스케어 AI 경진대회이며, 구강이미지 내 충치 유무 판별 모델 개발을 목표로 함.

# Participants
Team Name : DATA TRIP
- Namjin Baek
- Dahyeon Lee
- Jinseon Park
  
# Competition Schedule
- 참 가 신 청 : 2023년 11월 30일(금) ~ 12월 05(화)
- 대 회 참 가 : 2023년 12월 11일(월) ~ 12월 15(금) 18:00 까지
- 레포트 제출 : 2023년 12월 17일(일) 낮 12:00 까지
- 심 사 기 간 : 2023년 12월 17일(일)
- 결 과 발 표 : 2023년 12월 18일(월)
- 시 상 식 : ’23.12.21.(목)

# Summary
- 본 경진대회는 동일한 환경(ssh & vim editor)과 동일한 GPU를 참가자에게 분배함.
- 주최측에서 Resnet기반 모델 사용을 권장하였으며, resnet50_binary 모델 사용
- 일부 참가자의 GPU 독점 이슈로, 배치 사이즈(16) 및 에폭 수(6)를 낮게 설정함.
- 손실함수는 CrossEntropyLoss, 옵티마이저는 Adam(lr=0.001).

# Resnet
- 충치가 하나라도 있으면 True로 출력하는 Resnet기반 모델을 개발함.
- GPU 이슈로 light한 Resnet50_binary 모델 사용
