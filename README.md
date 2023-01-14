## 얼굴형 분석 시스템

- 개발기간
    - 2022.09.27 ~ 2022.09.30
- 사용 언어 및 라이브러리
    - `Python`, `Pytorch`, `sklearn`, `pandas`, `OpenCV`

## 💡 Topic

- Kaggle의 Face Shape Dataset에 대해 EfficientNet-B5 모델을 사용하여 얼굴형을 분석하는 시스템
- AI 부트캠프 Section4 Project

## ❓ 문제정의

헤어스타일에서든, 옷에 있어서든, 심지어 화장과 악세사리를 고를 때에도 최적의 선택을 하기 위해 얼굴형을 고려하는 모습이 많이 보인다. 자신의 얼굴형을 파악하고자 하는 사람들이 늘어남에 따라 유튜브, 블로그 등에서 얼굴형을 자가 진단하는 방법을 소개하는 매체가 많이 있는 것을 볼 수 있다. 그러나 개인이 매체 만을 보고 얼굴형을 파악하는 것이 번거로울 뿐 아니라 자가 진단한 것이 맞는지 의문이 들 수 있다. 

따라서 이를 쉽게 하고자 얼굴 이미지를 통해 얼굴형을 분석하는 시스템을 개발하고자 하였다.

## 🔍 프로젝트 진행과정

<img src="https://user-images.githubusercontent.com/76083173/212465637-2fd5fba7-c352-43cd-a565-d99333ccd6bd.png" height="300"/>

## 📚 데이터 셋

[Face Shape Dataset](https://www.kaggle.com/datasets/niten19/face-shape-dataset)

- Heart, Oblong, Oval, Round, Square 5개의 얼굴형으로 분류되어 있는 이미지 데이터
- 각 얼굴형 별 Training set 800개, Testing set 200개로 구성

## ✍🏻 프로젝트 수행 과정 및 결과

1. 가설설정
    - 가설 1: 얼굴형 분석을 할 수 있다.
    - 가설 2: 얼굴을 Crop한 이미지의 성능이 더 좋을 것이다.
2. 데이터 셋 분할
    - Train 데이터 셋을 9:1 비율로 Train과 Validation으로 분할함
    - Test 데이터 셋은 별도로 존재하는 것 사용
3. 모델링
    - 사전학습모델인 Efficientnet-b5를 로드
    - Validation set Accuracy 80%, Test set Accuracy 75%
    - Confusion matrix
        
        <img src="https://user-images.githubusercontent.com/76083173/212465690-f43d36db-bdc0-4724-b348-17b74cc5505b.png" height="300"/>
        
    - 예측 결과
        
        <img src="https://user-images.githubusercontent.com/76083173/212465723-c785fa51-cfc6-491c-9748-f37d9fb6eb24.png" height="400"/>
        
4. 이미지 크롭
    - OpenCV의 CascadeClassifier를 이용하여 얼굴 부분 검출하여 이미지 크롭 후 저장
5. 크롭 이미지 모델링
    - Validation set Accuracy 87%, Test set Accuracy 83%
    - Confusion matrix
        
        <img src="https://user-images.githubusercontent.com/76083173/212465750-4eb1db26-f160-4d0a-909d-95915d43d598.png" height="300"/>
        
    - 예측 결과
        
        <img src="https://user-images.githubusercontent.com/76083173/212465792-ebc3f775-17ca-4894-9dfa-3977d44623a6.png" height="400"/>
        
6. 가설 검증
    - 가설 1: 얼굴형 분석을 할 수 있다.
        - Crop 전 : 75% 정확도를 가지고 얼굴형을 분석할 수 있다.
        Crop 후 : 83% 정확도를 가지고 얼굴형을 분석할 수 있다.
    - 가설 2: 얼굴을 Crop한 이미지의 성능이 더 좋을 것이다.
        - Crop한 데이터를 가지고 분석한 결과 8% 정확도가 오른 것을 확인 할 수 있다.

## ✨ Learned

- 모델링을 바로 진행한 결과 모델의 성능이 어느 정도인지 파악하는 것에 어려움을 겪었음.
    - `baseline` 설정하여 모델의 성능을 비교해보는 것이 필요하다는 것을 다시 한번 깨닫게 되었음.
- `파이프라인`을 구축하는 이유에 대해서 배울 수 있었음.
- 이미지를 얼굴 부분만 `Crop`하는 코드를 사용해볼 수 있었음.
    - 크롭된 이미지에서 턱이나 이마가 살짝 잘리는 부분이 있어서 크기 조절하려 하였을 때 이미지의 사이즈를 벗어나는 곳이 생기는 문제가 있었음.
- 높은 성능을 바라고 무거운 버전의 EfficientNet을 사용한 결과 모델을 돌리는데 긴 시간이 걸려 프로젝트 기간 내에 다양한 모델을 시도해보지 못했음.
    - `기간과 모델 학습 시간을 고려하여 모델을 선택`하는 것이 필요하다는 것을 느낌.
