
# Comparing the Embeddings of Two National Cuisines with Flavor Profiling 

### Paper : 
[Paper Link](https://www.dbpia.co.kr/pdf/pdfView.do?nodeId=NODE11705201&googleIPSandBox=false&mark=0&minRead=5&ipRange=false&b2cLoginYN=false&icstClss=010000&isPDFSizeAllowed=true&accessgl=Y&language=ko_KR&hasTopBanner=true)


#### 진행 기간 : 2023.07~2023.10

#### 주제 : Flavor Profiling 기반 두 국가의 음식 임베딩 비교 및 유사 음식 추천

#### 주최 : 한국정보과학회 - 2023 한국소프트웨어종합학술대회

#### 참여 : 소프트웨어학과([niluminous](https://github.com/niluminous)), 컴퓨터공학과([rla124](https://github.com/rla124))

각 나라는 지리적 및 문화적 배경에 따라 고유한 식문화를 형성하며, 이로 인해 음식의 다양성과 차이점이 발생한다. 이 연구는 우즈베키스탄과 한국의 음식을 비교하고, 맛 정보를 반영하여 음식을 표현하는 새로운 방법인 Flavor Profiling을 소개한다. BERT 모델과 FoodBERT 모델의 한계를 분석하고, FlavorDB를 활용하여 음식의 풍미를 고려한 재료 표현을 만들었다. 이를 통해 두 나라의 음식을 비교하고, 음식의 맛 정보를 잘 포착하는 중요성을 강조한다.

### Dataset
|  | 한국 요리 | 우즈베키스탄 요리 |
|:--------:|:--------:|:--------:|
| 데이터 사이즈 (요리의 수)   | 387(en) + 384(kor) = 771   | 628   |
|언어  | 한국어, 영어   | 러시아어   |
| 고유한 재료 수   | 318(kor), 438(eng)  | 419 |
| 출처   | lampcook.com, maangchi.com  | russianfood.com   |


### Method
#### Bert-base-multilingual-uncased
러시아어, 한국어, 영어 데이터셋에서 고유한 재료를 추출하고  Hugging Face의 "transformers" 라이브러리를 이용하여 이 모델의 마지막 은닉층에서 임베딩을 얻어 재료 표현으로 활용했다. 하지만 t-SNE를 사용하여 시각화를 한 결과 BERT의 tokenizer 어휘에 없는 단어는 서브 워드로 분해하고 학습 데이터가 위키피디아에 제한이 되어있기 때문에 모델이 맛과 음식의 맥락을 파악하는데 한계를 지니고 있음을 확인했다. 
#### FoodBert
FoodBert도 bert-multilingual 모델보다 푸드 도메인을 더 많이 학습하여 컨텍스트를 고려해 임베딩을 생성함에도 불구하고 위와 동일한 시각화 방법을 적용한 결과 충분히 음식 재료의 맛에 대한 정보가 반영되지 않았음을 확인했다.
#### Flavor Profiling
위 언어모델들의 한계점을 극복하고자 Flavor Profiling을 제안했다.
936가지 재료에 대해 풍미를 유발하는 25,595개의 분자 정보를 제공하는 FlavorDB 데이터 베이스를 크롤링 하였다. 레시피 데이터 셋의 고유한 재료 종류와 FlavorDB에서 추출한 재료를 일대일 대응시켰고 TF-IDF 기법을 통해 각 재료에 대한 임베딩을 얻었다. 요리를 구성하는 모든 재료의 TF-IDF 임베딩의 평균을 내어 하나의 요리 임베딩을 만듦으로써 유사한 두 나라의 음식을 대응시켰다. Flavor Profiling이라는 새로운 기법을 이용하여 맛이 반영된 요리의 표현을 생성한 뒤 두 나라의 요리를 비교했으며 유사한 음식을 추출한다는 점에서 음식의 표현에서 맛의 정보를 포착하는 것의 중요성을 입증했다. 
