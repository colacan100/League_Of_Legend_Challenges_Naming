# League_Of_Legend_Challenges_Naming_Project

---

## 주제 <br>
리그오브레전드 도전과제 작명

## 기획배경 <br>
2022년 5월 10일에 리그오브레전드의 도전과제가 출시되었다. <br>
앞으로의 도전과제의 업데이트에 있어서 네이밍이 지속적으로 이어져야한다. <br>
감정, 게임을 잘 나타내는 키워드를 통해서 작명에 도움을 줄 예정이다. <br>

## 내부 디렉토리 구조

```python

Kartrider_Meta_Analysis
┖ .vscode
┖ Crawl # twitter api를 이용한 관련 트윗 조회
  ┖ twitter_crawl.ipynb 
┖ KeyBERT # 주요 키워드 추출
  ┖ keybert.ipynb
  ┖ keybert2.ipynb
┖ Presentation
  ┖ Project_PPT.pdf
  ┖ Project_Video.mp4
┖ dataset
  ┖ emotion_list # 감정분류뒤의 data
    ┖ ad_emotion.csv
    ┖ jungle_emotion.csv
    ┖ keyword_emotion.csv
    ┖ mid_emotion.csv
    ┖ sup_emotion.csv
    ┖ top_emotion.csv
    ┖ total_emotion.csv
  ┖ external_data 
    ┖ 감정단어사전0603.xlsx # 단어 대치를 위한 data
    ┖ 한국어_단발성_대화_데이터셋.xlsx # model 학습을 위한 data
  ┖ tweet_list # 조회한 트윗 data
    ┖ ad_list.csv
    ┖ jungle_list.csv
    ┖ mid_list.csv
    ┖ sup_list.csv
    ┖ top_list.csv
    ┖ tweet_list.csv
  ┖ result.csv # 작명된 키워드
┖ koBERT # 키워드의 감정분석
  ┖ emotion_response.ipynb
  ┖ kobert_colab.ipynb

```

## 데이터 가져오기

**Twitter API**
> 트위터 API를 통해서 각 라인, 티어등에 관련한 자연어 수집 <br>
> 
> 중복제거 : retweet인 경우<br>
> 
> 스팸제거1 : https:// 포함시 필터<br>
> 
> 스팸제거2 : 줄바꿈 문자 포함 중 조건에 맞지 않는 것 필터 (줄바꿈이 너무 많은 경우, 팔로워가 너무 적은 경우)<br>
> 
> 기간 : 2022-05-13부터 2022-05-20까지 (twitter에서 일주일간의 데이터만 허용하기 때문이다.)<br>
> 
> 키워드 : '리그오브레전드', '롤 탑', '롤 미드', '롤 정글', '롤 원딜', '롤 서폿'<br>
> 
> 수집된 데이터를 csv파일로 변형<br>

## 키워드 추출

**KeyBERT**
> 형태소 분석 : 단어들의 형태소 분석 후 품사 태깅
> 
> CountVectorizer : 단위별 등장횟수를 카운팅하여 수치벡터화 (Trigram으로 단어뭉치 생성) 
> 
> 다국어 SBERT load : BERT의 문장 임데딩 성능을 개선시킨 모델
> 
> 문서와 가장 유사한 키워드 추출

## 감정 분석

**감정분류 데이터셋**
> AI허브를 통한 38595개의 감정 데이터셋 준비
> 
> 7개 감정 class 숫자에 대응
> 
> 훈련,테스트셋 분류
> 
> tokenization, int encoding, padding 진행
> 
> torch형식의 데이터셋 생성

**KoBERT**
> 파라미터 조정 : max_len = 64, batch_size = 64, warmup_ratio = 0.1, num_epochs = 5, max_grad_norm = 1, log_interval = 200, learning_rate =  5e-5
> 
> 감정 데이터셋 KoBERT에 학습
> 
> train acc : 0.7929007553101757
> 
> test acc : 0.5494344670481034
> 
> 단순 1개로만 예측했을시 정확도는 0.142 이므로 학습이 어느정도 이루어짐

## 도전과제 작명
> 앞서 만든 트위터 데이터셋에 감정분석
> 
> 만들어진 감정의 비율을 확인 후 키워드와 결합
>
> 앞서 만들어진 감정을 감정단어 목록과 대응 (경희대학교 BK21+ 데이터과학기반 경영전문 연구인력 양성사업 게시판)
> 
> 키워드와 감정단어 목록을 조합하여 도전과제 작명
