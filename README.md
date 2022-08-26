교통 상황과 환경 개선을 위한 공유 자동차 서비스 활용 방안🚘 
==============================================
Model
------
* xgboost
* LightGBM
* catboost
* RandomForest
* knn
* Stacking Ensemble
* Markov Clustering

Description
------------------------------------
> 1. 주제 
>> 교통상황과 환경 개선을 위한 공유 자동차 서비스 활성화 방안
> 2. 세부주제
>> 1. 신규 주차장의 선정 기준 및 구체적인 입지후보지를 제안 
>> 2. 대중교통과의 연계 시스템을 고안한 차세대 교통 허브 제안
>
> 3. 프로젝트 필요성
>> 1. ‘환경 오염’, ‘차량 혼잡도’ 를 해결하기 위해 정부는 친환경 교통 수단 도입을 통한 노력을 기울이고 있으며, 지자체 또한 대중교통 활성화 노력을 병행하고 있지만, 자동차 보유 대>> 수는 매년 증가하고 있음.  
>> 2. 또한, 추가적인 도로 인프라의 확충으로는 혼잡 등의 교통문제를 해결 할 수 없어 미래형 경제모델인 ‘공유 자동차’ 서비스 활성화 필요성 문제점을 해결하고 공유 자동차 활성화 방안>> 을 제시하기 위해 프로젝트를 실시

분석 Flow
--------------------------------
1. 데이터 수집 및 가공
 * 주 데이터 : 공유자동차 운행이력 재현데이터, 공유자동차 예약이력 재현데이터
 * 외부 데이터 : 전국 격자별 지리정보 데이터 (국토정보플랫폼) 
 ->(고속도로IC접근성, 고속화철도접근성, 병원접근성, 생활권공원접근성, 노후주택수, 주차장접근성, 전기차충전소접근성, 공연문화시설접근성)
<img width="901" alt="KakaoTalk_Image_2022-08-26-18-53-26" src="https://user-images.githubusercontent.com/108215485/186878681-8342d683-1298-49d3-a4d1-b0091e36e5d3.png">
<img width="873" alt="KakaoTalk_Image_2022-08-26-18-55-50" src="https://user-images.githubusercontent.com/108215485/186879220-47c61e4d-fe97-44a3-baea-2362b4c8677c.png">   
   
> * 독립변수 (고속도로접근성, 고속화철도접근성, 공연문화시설접근성, 노후주택수, 종합병원접근성, 생활권공원접근성, 전기차충전소접근성, 주차장접근성)
> * 종속변수 (예약 건수)
         
2. 데이터 전처리
- 변수간 상관관계, 다중공선성 확인 : 제거할 속성 없음
<img width="407" alt="KakaoTalk_Image_2022-08-26-19-00-44" src="https://user-images.githubusercontent.com/108215485/186880021-9cd61f48-1325-4d97-81e7-eb58fcd1cd72.png">   
   
> 결측치 대체 : MICE Algorithm   
> 이상치 제거 : IQR 활용   
> 스케일링 : MinMaxScaling    
> Train, Test set : Stratified Shuffle Split   
> 오버+언더 샘플링 : SMOTEENN   
   
3-1. 모델 성능비교 및 학습결과 (지도학습)
<img width="933" height="300px" alt="KakaoTalk_Image_2022-08-26-19-05-40" src="https://user-images.githubusercontent.com/108215485/186880801-9f89e414-48b2-4891-b306-ae1df2263902.png">   

>  RandomForest( n_estimators=100, max_depth=5, min_samples_leaf=8, min_samples_split=6, random_state=0, n_jobs=-1 ) 
<img width="849" height="300px" alt="KakaoTalk_Image_2022-08-26-19-09-51" src="https://user-images.githubusercontent.com/108215485/186881556-12659423-59ad-4658-abf1-7a7bad221594.png">   

>  accuracy : 81% (모델평가지표) / recall : 79% (모델평가지표)
>  변수 중요도 : 병원접근성>전기차충전소접근성>생활권공원접근성>고속도로IC접근성>...       
      
3-2. 모델 성능비교 및 학습결과 (비지도학습)
+ Markov Clustering을 활용한 운행 군집화   
   
![KakaoTalk_Image_2022-08-26-19-06-59,](https://user-images.githubusercontent.com/108215485/186881892-bf5b64a4-7a8f-41d3-9136-8d022342ee8a.png)
   
>  공유자동차 운행이력이 많은, 통행의 중심점이 될 지점을 도출   
   
4. 분석결과 및 활용방안
> 1. 주차장 우선 신설 기준 제안
>>전기차충전소, 종합병원과의 접근성이 높은 곳 
>2. 주차장 입지 제안
>> (1) 경기도 성남시 분당구    
>> ![KakaoTalk_Image_2022-08-26-19-07-05](https://user-images.githubusercontent.com/108215485/186882765-86521487-e590-4e8f-8403-5be1dc91fd7f.png)   
>> (2) 서울시 강서구   
>> ![KakaoTalk_Image_2022-08-26-19-07-10](https://user-images.githubusercontent.com/108215485/186882841-0e57c9f1-df10-4d0d-85cb-6548cc5e385b.png)      
>> (3) 경기도 안산시 단원구   
>> ![KakaoTalk_Image_2022-08-26-19-07-13](https://user-images.githubusercontent.com/108215485/186882903-92ab5586-73e9-4547-9c7b-1fb784c082f9.png)      
>> (4) 인천광역시 서구   
>> ![KakaoTalk_Image_2022-08-26-19-07-17](https://user-images.githubusercontent.com/108215485/186882969-a889f9a4-b02d-4487-8f01-d90a458a172f.png)        
> 3. 교통 허브
>> - 마코프 클러스터링 결과   
>> <img width="620" alt="KakaoTalk_Image_2022-08-26-19-22-04" src="https://user-images.githubusercontent.com/108215485/186883643-82694e24-a4dd-4bab-9b8c-a2ebcbced26f.png">            
> 4. 공유 자동차 주요 권역 설정               
>> * 4개의 권역을 다시 두 개로 나눔            
>> ![KakaoTalk_Image_2022-08-26-19-07-29](https://user-images.githubusercontent.com/108215485/186883870-2e33dea5-7f12-46c3-9c3c-95cecf041ff9.png)         
>> 서울 도심은 낮 시간, 업무 용도 이용			경기, 인천은 야간 시간, 출퇴근, 여가 용도      
>> <img width="706" alt="KakaoTalk_Image_2022-08-26-19-25-05" src="https://user-images.githubusercontent.com/108215485/186884194-bb520379-750f-47e3-8701-c4976371a15f.png">      
>> 이를 이용하여 아래와 같은 요금 할인 전략 제안         
>> <img width="945" height="300px" alt="KakaoTalk_Image_2022-08-26-19-26-30" src="https://user-images.githubusercontent.com/108215485/186884416-82999d6f-067e-41a3-b607-81eeca528c3b.png">                 
>>* 공유 자동차 이용 증가와 운영의 차질 감소 기대             
>>* 각 지역의 이용이 잦은 시간대에 차량 배치가 원활하게 이루어져 이용자의 서비스 만족도 상승 예상      

5. 기대효과 및 한계점   
* 기대효과    
> 1. 공유 자동차 주차장 입지 선정에 관한 사회적 변수들을 확인하여, 향후 여러 연구에 사용될 수 있을 것이라 기대됨   
> 2. 공유 자동차 시장의 활성화로 인한 교통 혼잡도와 환경오염 같은 여러 문제들 해결 및 기업이익 증가, 사용자의 편리성 증대    
> 3. 예측 모델의 지속적인 훈련으로 다른 지역이나 공유 자동차의 인프라가 구축되지 않은 곳에 진출 시, 초기 결정이 용이    
* 한계점    
> 전체 기간의 모든 데이터가 아니며, 익명 재현 데이터로 인해 노이즈가 존재함   
> 주차장 입지 제안에서의 주관적 해석의 개입   
> 원 ‘예약현황 데이터’를 그대로 사용하고 싶었지만, 위치 속성이 없어 운행데이터를 가공하여 사용해 정확한 데이터가 아닐 수 있음   
> 데이터의 양이 불충분하여 시계열 모델 사용 불가   
> 운행 데이터의 시간 속성이 1시간 단위로만 표현되어 있어 정확한 시간대 분석 불가   
* 향후 과제   
> 적정한 수요 추정과 이용요금에 대한 경제성 검토 등에 대한 추가 연구가 필요할 것으로 판단됨   
> 이진분류가 아닌 다중분류 모델을 사용하면 풍부한 인사이트 도출 가능 할 것으로 예상   
> 더 다양한 변수들을 포함시켜 여러 측면에서 분석한다면 다양한 전략을 도출할 수 있을 것이라 기대      

6. Environment     
- Python 3.9   
- Google Colab GPU   

7. 데이터 실행 사항
> * 재현데이터로 원데이터 제공할 수 없어, 모의데이터로 코드 검정 
> > 공유자동차예약이력.csv -> 모의예약.csv  
> > 공유자동차운행이력.csv -> 모의운행.csv 
> * pd.read_csv(' 경로에 맞게 수정 필요 ') -> 구글 코랩에서 실행하였음    
>> 모의데이터는 1000 행으로 원 재현 데이터와의 범위가 달라서 모의데이터를 넣었을 때, 코드 구현이 가능하도록 시계열 분석에서의 설정을 다르게 해서 '모의코드.csv'추가 제출함.       
>> 모의코드에서 마코프 클러스터링의 결과가 잘 안나올 수 있음 (데이터 행수가 적어)
























