# CAMUS AI

CAMUS 프로젝트에서 생성한 AI모델에 대한 README입니다.

각 모델은 부적절한 한국어 채팅을 단계적으로 쉽게 필터링 할 수 있도록 하기위해 설계되었습니다.

---

### 목차

 [single-chatting-filtering model](##single-chatting-filtering) 

[context-chatting-filtering model](##context-chatting-filtering)

---

## 🔍 single chatting filtering

단문 채팅을 (욕설, 혐오표현, 중립)으로 분류하는 KcELECTRA 기반 다중 클래스 분류 모델입니다.
<br>
<br>

### 🔰 **Requirements**
*****

- `pytorch ~= 1.8.0`
- `transformers ~= 4.11.3`


### 🔰 model
****

- 사용 모델 : KcELECTRA 
- KcELECTRA는 ELECTRA 기반 모델로 한국어 댓글이 많은 뉴스, 
기사들의 댓글과 대댓글을 수집해서 사전 학습한 모델로 다양한 악성 채팅에 적용하기 좋은 모델입니다.
<br>

### 🔰 dataset
****

한국어 기사 댓글 중 혐오발언에 대한 다중 레이블 분류 데이터를 활용했습니다.
다음과 같이 전처리를 수행했습니다.

- 욕설(3)이 있다면 => 0
- 욕설이 없고 혐오표현(0,1,2,4,5,6,7)이 있다면 => 1
- 욕설과 혐오표현이 없다면 => 2
<br>

### 🔰 evaluation
****
![eval](https://github.com/Camus-chat/ai-model/blob/readme-asset/eval.png)

- 결과에 따라 90%의 정확도를 보이는 모델을 선정하였습니다.

<br>

----

## 🔍 context chatting filtering


다중 채팅을 (욕설/비하/모욕, 성희롱/혐오, 스팸/도배, 중립)으로 맥락에 따라 분류하는 KcELECTRA 기반 다중 클래스 분류 모델입니다.

### 🔰 model
****

한국어에 적합한 모델인 HyperClOVA 를 사용하여 다중 채팅에 대한 맥락 필터링을 수행하고자 했습니다.
* clova studio 튜닝 API의 HCX-003모델을 사용하였습니다.

<br>

### 🔰 dataset
****

* 단문 필터링에서 사용한 ‣데이터를 채팅 데이터처럼 전처리하여 활용, 이후 약 1500개의 데이터를 무작위 추출했습니다.
* youtube data api를 사용해서 얻은 100개의 댓글 데이터 묶음 직접 라벨링하여 도배/스펨 데이터를 확보하였습니다.
* 각 데이터는 1~10개의 댓글에 대해 유저번호를 부여하여 전처리 되었습니다.