# CNN based multi class classification <br/>for Diet evaluation and Design

## 1. 개요
바쁜 일상을 보내는 현대인들은 본인이 먹는 음식의 성분을 불균형한 식사를 하는 일이 빈번하다. 
<br/> 그렇기에 음식 이미지 촬영을 통하여, 본인이 먹는 식사의 영양 성분을 제공받을 수 있게 하는 
<br/>프로젝트를 진행하였다. 

## 2. 과제 수행방법

### 2.1 데이터
약 42000개의 이미지 데이터 : 음식 종류 : 83개 / 양 : Q1~Q5 5단계로 구성
<br/>__[예시]__
![side_건더기국류_뚝배기_갈비탕_Q4_00001](https://user-images.githubusercontent.com/37768648/208874525-9d9c816b-13ca-458c-b699-4e826d2bc197.JPG)

### 2.2 음식 종류 분류

* EfficientNet

* ReXNet

* SENet

### 2.3 음식 양 추정

* MaskRCNN + Volume Estimation

* Multi Reference CNN

* Only CNN

### 2.4 Result

#### 음식 종류 분류[Accuracy]
* __EfficientNet : 100%__

* ReXNet : 99.8%

* SeNet : 99.96%

#### 음식 양 추정 
* MaskRCNN + Volume Estimation : 비국물류 음식 탐지 및 부피 측정 우수, 국물류 추정 불가

* Multi Reference(Text, Coin size) CNN model : 84%[Accuracy]

* __Only CNN model : 96%[Accuracy]__

### 3. 최종 결과

#### 음식 종류 분류
* SeNet

#### 음식 양 추정
* Only CNN : SeNet

#### 음식 양 추정에서 Only CNN의 SeNet이 가장 성능이 좋게 나와 최종 모델로 선정했다. <br/>통일성을 위해 음식 종류 분류 또한 SeNet을 모델로 선정했다.

## 4. 프로그램 사용방법
__line3__<br/>
```python
df = pd.read_excel("/content/drive/MyDrive/DCD_2022/음식분류 AI 데이터 영양DB.xlsx", engine = "openpyxl")
```
1. "Diet Evaluation and Design.ipynb"에서 "음식분류 AI 데이터 영양DB.xlsx"부분을 본인이 저장한 경로로 수정한다.<br/>

__line7__
```python
food_model = mobilenet(num_classes=83)
vol_model = mobilenet(num_classes=5)
# Load state_dict
food_model.load_state_dict(torch.load('/content/drive/MyDrive/Types of food_SENet_weight.pt'))
vol_model.load_state_dict(torch.load('/content/drive/MyDrive/Amount of food_SENet_weight.pt'))
```
2.  이후 라인을 실행시키다가 model_weights 폴더에서 다운 받은 "Types of food_SENet_weight.pt"와 "Amount of food_SENet_weight.pt" <br/>파일의 위치를 원하는 경로로 지정한다.

<br/>__line9__
```python
today_food = ["/content/drive/MyDrive/DCD_2022/음식 이미지 및 영양정보 텍스트/val_cropped/쌀밥/side_밥류_원형배달_쌀밥_Q3_00033.JPG",
    "/content/drive/MyDrive/DCD_2022/음식 이미지 및 영양정보 텍스트/val_cropped/갈비탕/side_건더기국류_뚝배기_갈비탕_Q5_00028.JPG", 
    "/content/drive/MyDrive/DCD_2022/음식 이미지 및 영양정보 텍스트/val_cropped/갈치조림/side_생선조림_냄비_갈치조림_Q1 00001.JPG"]
```

3. today_food에 오늘 하루 먹은 이미지의 경로를 입력한다.<br/> 
4. 식단을 평가받고 설계한다.
