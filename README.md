# 9월 11일 스터디 모임
### 오늘의 한 일: 서로 다같이 구글 meet로 모여서 한사람(나)이 코드를 작성하면 다른 사람들이 피드백을 주었음
### data 로드, train, test분리, train set 시각화, 하이퍼 파라미터 설정
### 모델 fit, test, visulization 등 간단한 코드 러프하게 짜놓음!


# 9월 15일 스터디 모임
### learning rate decay를 linear로 설정하고 싶었는데 linear 라이브러리도 안보이고, 인터넷에 코드를 찾아봐도 보이지 않았다.
### 결국 exponential decay를 팀원분이 인터넷에서 코드를 찾아주셔서 learning rate를 exponential로 설정함.
### model.compile로 돌렸는데 accurarcy는 높게나오나 loss가 자꾸 변동되며, 10이하로 떨어지지 않는 문제가 발생하여 epoch이 문제인가? 싶어서 epoch를 이리저리 만져보았다.
### epoch을 만져도 loss값은 계속해서 줄지않고, 결과가 매번 다르게 나와서 weight문제인가? 하다가 문제를 발견함.
### data를 정규화하지 않았던 것이다. data를 MinMaxScaler를 통해 0~1사이 값으로 변환하니까 loss값이 0.0n값으로 확연히 줄어든 것을 확인 함. 
### model.predict를 돌렸으나 y_pred값이 전부 0.4이하로 나와서 Y의 1값을 제대로 탐지하지못한다는 것을 알아냄.
### 나랑 팀원 김**은 어떤게 문제인지 찾기 시작함. predict코드의 문제인지 코드를 다시 살펴보았음.
### 팀원 김**은 종속변수 Y의 데이터가 불균형해서 생긴 문제가 아니냐고 지적.
### Y의 value_counts()를 해보니 실제로 0과 1의 데이터 불균형 문제가 심각했음.
### 데이터 불균형때문에 이 모델이 예측을 제대로 못하나? 싶어서 나는 recall_score를 확인했음.
### 실제로 recall_score가 0임을 확인.(모델의 정확도는 높으나 재현율이 떨어짐.)
### Y의 데이터 불균형 해결을 위해 SMOTE방법을 이용하여 Oversampling하면 어떠하냐고 제안함.
### SMOTE방법으로 predict까지 돌리고 recall_score를 조회하니 0.96정도로 재현율이 눈에띄게 올라감.
### 다음 스터디 모임에서는 weight초기화를 다른방법으로 해보기, learning rate decay를 다른 방법으로 해보기로함.
