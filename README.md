교통 상황과 환경 개선을 위한 공유 자동차 서비스 활용 방안 
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
<img src="/path/to/img.jpg" width="450px" height="300px" title="px(픽셀) 크기 설정" alt="RubberDuck"></img><br/>
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
>  변수 중요도  :  병원접근성  >  전기차충전소접근성  >  생활권공원접근성  >  고속도로IC접근성  > 등등       
      
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
- 마코프 클러스터링 결과   
<img width="620" alt="KakaoTalk_Image_2022-08-26-19-22-04" src="https://user-images.githubusercontent.com/108215485/186883643-82694e24-a4dd-4bab-9b8c-a2ebcbced26f.png">   
> 4. 공유 자동차 주요 권역 설정   
* 4개의 권역을 다시 두 개로 나눔      
![KakaoTalk_Image_2022-08-26-19-07-29](https://user-images.githubusercontent.com/108215485/186883870-2e33dea5-7f12-46c3-9c3c-95cecf041ff9.png)   
> 서울 도심은 낮 시간, 업무 용도 이용			경기, 인천은 야간 시간, 출퇴근, 여가 용도      
<img width="706" alt="KakaoTalk_Image_2022-08-26-19-25-05" src="https://user-images.githubusercontent.com/108215485/186884194-bb520379-750f-47e3-8701-c4976371a15f.png">
> 이를 이용하여 아래와 같은 요금 할인 전략 제안

























