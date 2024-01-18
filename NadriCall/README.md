# Host
대구광역시, 교육부, NIA, 경북대학교 등

# Objective

공공데이터를 활용한 나드리콜 운영 개선 아이디어 제고

# Participant

- 백남진 (대구대학교 4학년)
- 홍수현 (대구대학교 4학년)

# Role

- **기획 및 리더**
- **데이터 분석**
    - EDA(Exploratory Data Analysis)
    - 통계 분석 (ANOVA)
- **예측 모델 개발**
    - XGBoost
- **PPT 제작**

# Results

🏅혁신아이디어 수상 (장려상)

# **Issues and Improvements**

**대구광역시 위경도에 따른 배차시간 시각화**

대구광역시 행정동별로 배차시간을 시각화 하고 싶었다. 지도 시각화 경험이 없었고 geojson과 같은 파일도 처음 다루게 되었다. 지도 시각화 자료를 찾아보니 Python 내 라이브러리, plotly로 할 수 있었다. geojson은 아래 깃헙에 있다.

https://github.com/raqoon886/Local_HangJeongDong

```python
import plotly.express as px
import json
import os

# 대구광역시 geojson 파일을 찾아서 다운
geometry_daegu = json.load(open("hangjeongdong_대구광역시.geojson", encoding='utf-8))

# 대구광역시 ~구 ~동에서 ~동 만 추출
for feature in geometry_daegu['features']:
	adm_nm = feature['properties']['adm_nm']
	dong_name = adm_nm.split()[-1]
	feature['properties']['adm_nm'] = dong_name

# jeojson과 변수명이 같아야함
df.rename(columns={'출발지 행정동':'adm_nm'}, inplace=True)

# 행정동별 평균 배차시간 그룹핑
groupby_df = df.groupby(['adm_nm'])['배차시간'].mean().reset_index()

# 이상치를 고려해 로그 배차시간 사용
groupby_df['배차시간(분)_log'] = np.log1p(groupby_df['배차시간(분)'])

fig = px.choropleth(groupby_df, geojson=geometry_dg, locations='adm_nm', color='배차시간(분)_log',
                   color_continuous_scale='Blues', featureidkey='properties.adm_nm')

fig.update_geos(fitbounds='locations', visible=False)
fig.update_layout()
```

**시간의 흐름에 따른 행정동 배차시간 대시보드 개발**

00시부터 23시까지의 배차시간이 행정동별 다른지 확인하기 위해 Interactive한 시각화가 필요했다. Dashboard를 제작해야하는데, Tableau나 PowerBI를 활용한 경험이 없었다. 이를 위해 Python 라이브러리인 Dash와 Plotly를 조합해 사용했다.

```python
import dash
import dash_core_components as dcc
import dash_html_components as html
from dash.dependencies import Input, Output
import plotly.express as px

# Dash를 사용하기 위해 먼저 정의를 해준다.
app = dash.Dash(__name__)

hour_groupby_2022['배차시간(분)_log'] = np.log1p(hour_groupby_2022['배차시간(분)'])

# 초기 맵 설정 (예시: 0시에 대한 맵)
initial_map = px.choropleth(hour_groupby_2022[hour_groupby_2022['HOUR'] == 0], 
                            geojson=geometry_dg, 
                            locations='adm_nm', 
                            color='배차시간(분)_log',
                            color_continuous_scale='Reds', 
                            featureidkey='properties.adm_nm')

app.layout = html.Div([
    # 슬라이더를 통한 시간대 선택
    dcc.Slider(
        id='hour-slider',
        min=0,
        max=23,
        step=1,
        value=0,  # 초기값 설정
        marks={i: f'{i}시' for i in range(24)}
    ),
    # Choropleth 맵을 표시할 영역
    dcc.Graph(
        id='choropleth-map',
        figure=initial_map
    )
])

@app.callback(
    Output('choropleth-map', 'figure'),
    [Input('hour-slider', 'value')]
)

def update_map(selected_hour):
    # 선택된 시간대에 따라 맵 업데이트
    fig = px.choropleth(hour_groupby_2022[hour_groupby_2022['HOUR'] == selected_hour], 
                        geojson=geometry_dg, 
                        locations='adm_nm', 
                        color='배차시간(분)_log',
                        color_continuous_scale='Reds', 
                        featureidkey='properties.adm_nm')
    fig.update_geos(fitbounds='locations', visible=False)
    return fig

if __name__ == '__main__':
    app.run_server(debug=True)
```

상호작용 가능한 대시보드를 제작하였다.

# Lesson learned

**비즈니스 모델 캔버스 (BMC)**

데이터를 분석해서 나온 아이디어가 실제로 수요자에게 어떤 가치를 제공하는지가 중요하다. 우리의  아이템을 사용하는 고객은 누구인지(Customer Segmentation), 어떤 가치를 제공하는지(Value) 등 9가지 요소를 알아야 한다. 아이디어가 정말로 실현가능한지 가치가 있는지  **비즈니스 모델 캔버스** 로 정리할 수 있었다.

**고객분류는** 서비스를 이용하는 고객은 누구인가?에 초점을 둔다. 노약자 및 장애인, 그리고 운전기사가 있겠다. **가치 제안은** 고객에게 어떤 가치를 제공해 줄 수 있는지에 대한 것이다. 승객들에게 배차시간을 감소시켜주고, 행정동별 콜 예측으로 휴차시간을 감소시킨다. 여기서 휴차시간이란, 승객이 하차한 후 다음 콜까지의 시간으로 정의한다.

**채널은** 어떤 방식으로 제공해줄 것인지에 대한 것이고 나드리콜 어플을 통해 제공한다. **고객 관계는** 고객을 유치시킬 수 있는 가치에 대해 정의한다. 배차시간 단축으로 승객들은 만족할 것이며, 콜 예측으로 기사들은 효율적으로 운영해 수입을 증가시킬 수 있다.

**수익 흐름은** 어떻게 수익을 창출할 것인지에 대한 것이다. 택시비 일부와 나드리콜 어플 내 광고를 등록해 수익을 벌어들인다. **핵심 자원은** 이 서비스를 활용하기 위해 어떤 자원이 필요한지, 즉 접수 데이터와 스팟존 근처 차량에게 선택지 창을 제공하며 스팟존 위치를 제공하는 것이다.

**핵심 파트너는** 우리 사업의 파트너는 누구인지 알아보는 것이다. 나드리콜 운전기사와 일반 택시기사가 있다. 타 업체와 협업을 통해 나드리콜 차량 대수를 늘릴 수 있다. **핵심 활동은** 서비스를 고객에게 제공하기 위해 우리가 해야하는 것은 무엇인지다. 배차가 긴 외곽지역의 콜을 시계열 분석과 예측을 통해 제공해준다. 마지막으로 **비용 구조다.** 비용 지출은 어떤 것들이 있는지며, 모델을 개발 하는 비용과 하드웨어 구입 비용 등이 있겠다.

---
**개인평**

다리 수술과 입원으로 2주 동안 활동하기 어려웠다. 그래도 통증 참아내며 입원실에서 개발을 했다. 

덕분에 수상까지 할 수 있었다.
