# 주최
DACON + HD(HYUNDAI)

# 배경
- 코로나 19이후 물류 정체로 인해 다수의 항만에서 선박 대기 시간이 길어지고, 물류 지연이 되고 있음.
- 접안(배를 육지에 대는 것) 전에 선박이 해상에 정박(해상에 닻을 바닥 밑에 내려놓고 운항을 멈추는 것) 하는 시간을 대기시간(Target Variable)으로 정의

# 목적
항만 내 선박의 대기시간을 예측하는 AI 알고리즘 개발

# 기대 효과
선박의 접안 시간 예측 가능으로, 선박 대기시간을 줄여 연료 절감 및 온실가스 감축 효과 기대

# Process

1. 변수 생성 (Feature Engineering)
2. Target Encoding
3. MinMaxScaler + HistGradientBoosting Model
4. Clipping
