# Business Requirements-Based Problem Solving Projects

- 주제: CNN 기반 모델을 활용한 식물 및 식물병 인식 서비스 'Pland Doctor' 앱 개발
- 기간: 2022.04.04 ~ 2022.05.13
- 참여 인원
  - 프론트 엔드: 김연우(팀장)
  - 백엔드 & 데이터 엔지니어: 강중모
  - 데이터 사이언티스트: 이유진, 강교철, 박혜인
- 기술 스택 : Python, Scala, Go, MySQL, Django, Hadoop, Spark, Elasticsearch, Airflow, Slack, Pytorch, Resnet50, VGG16, Yolov5s, Shellscript, HTML, CSS, Javascript, AWS EC2, AWS S3, Github

## 1. 프로젝트 기획 배경 및 목표
* 프로젝트 기획 배경
  - 코로나 19 이후 국내 홈가드닝 매출 상승
  - 많은 소비자 또한 반려식물 재배를 시작하며 식물에 대한 관심이 증가하고 있음

* 시장조사
  - 반려 식물과 관련한 서비스가 존재하지만, 다양한 문제점 존재
  - 기존 플랫폼의 문제점 : 구성 복잡, 직관적이기 어려움, 엉뚱한 결과, 글씨가 짤린다 등

* 프로젝트 목표: 시장조사의 문제점을 보완하고, 많은 소비자의 니즈에 충족하는 반려식물 서비스를 만들고자 함
  - **식물 인식 서비스** : 식물 사진을 통해 어떤 식물인지 인식함으로써 식물의 이름과 식물을 키우는 데에 필요한 정보 중심으로 관련 정보 제공
  - **식물병 인식 서비스** : 식물병이 의심되는 식물 사진을 통해 어떤 식물병에 걸렸는지 인식하고, 식물병의 종류와 예방법 정보 제공
  - **반려식물 등록** : 반려식물 등록 서비스를 통해 식물의 종류에 따라 물주는 주기, 광도 등 식물별로 맞춤형 관리 서비스를 제공
  - **유용한 정보 제공** : 사용자의 위치 정보 제공 동의를 받아 위치에 따라 식물이 예민하게 반응할 수 있는 자외선 지수나 습도 등 관련 정보를 제공

## 2. Plant Doctor 서비스 소개
* 메인 서비스 명 : Plant Doctor

* 메인 로고

![image](https://github.com/Hyeeein/PlantDoctor/assets/81239567/31029a2f-8f12-4a1d-a7ad-1b7356437906)

* 서비스 소개
  - CNN 기반 모델을 활용하여 **식물 및 식물병 인식 모델** 제공
  - 사용자들이 반려식물을 손쉽게 관리할 수 있도록, **식물의 건강에 영향을 주는 정보 제공**
  - 반려식물을 처음 키우는 사람도 **흥미롭게 이용할 수 있는 서비스** 제공
  
* 서비스 흐름도

![image](https://github.com/Hyeeein/PlantDoctor/assets/81239567/f3232cab-72ed-44d5-9d2a-e2eec05447de)

* 시스템 아키텍처

![image](https://github.com/Hyeeein/PlantDoctor/assets/81239567/c0e5c882-1406-4b37-8e4f-18b5bc3568f8)

* 사용 언어 : `GO`, `Scala`, `Python`

## 3. 데이터

### (1) 사용한 데이터 목록
* 식물 및 식물병 인식 모델에 사용하는 데이터

![image](https://github.com/Hyeeein/PlantDoctor/assets/81239567/0ca3d0d4-53a0-4c30-8851-9ecf139505e9)

* 위치정보, 온도, 습도, 날씨, 시간별 기온, 자외선 지수 API

![image](https://github.com/Hyeeein/PlantDoctor/assets/81239567/f98fbafa-f2be-4a15-910b-83fdf513c3be)

* 식물 검색 기능에 사용되는 데이터

![image](https://github.com/Hyeeein/PlantDoctor/assets/81239567/38495a66-7bfd-46ec-860c-4b8007e7aa53)

* 'Plant Doctor' ERD

![image](https://github.com/Hyeeein/PlantDoctor/assets/81239567/b051e92c-b895-46db-baa2-2895960228f8)

### (2) 데이터 전처리

* 식물 인식 모델 (YOLOv5s)
  - 크롤링한 식물 이미지 데이터 → **Annotation 라벨링 데이터의 부재**
  - **사용자가 식물을 화면 가운데에서 찍는다는 시나리오** 가정 하에 이미지 중심 좌표 윚로 임의의 바운딩박스로 라벨링 데이터 생성
  - 데이터 전처리 또한 식물이 중앙에 위치한 이미지 위주로 정제
  
  ![image](https://github.com/Hyeeein/PlantDoctor/assets/81239567/3c78c1f8-5f7e-4538-8e0f-83025d7794ca)

* 식물병 인식 모델 (YOLOv5s)
  - 이미지 및 라벨 전처리 이슈 : AIHub 노지작물 질병진단 이미지, 라벨 데이터 활용 → **동일한 파일명으로 이미지와 라벨 데이터 매치**
    
    ![image](https://github.com/Hyeeein/PlantDoctor/assets/81239567/9ec643f2-5d66-4b6c-bbe0-ebc249fc34d7)

  - YOLOv5 모델에서 필요한 라벨 데이터 형식은 .txt 파일이므로, AIHub에 업로드 되어 있는 json 파일 값을 추출하여 변환

    ![image](https://github.com/Hyeeein/PlantDoctor/assets/81239567/707322fe-3452-4735-94d4-80cb9ff8a90b)

## 4. 딥러닝 모델 구현 (CNN)
* 분석 모형

![image](https://github.com/Hyeeein/PlantDoctor/assets/81239567/e3851d59-bad9-4e2e-928c-47c29a5d8b7b)

### (1) 모델 선정 과정

* 식물 인식, 식물병 인식 모델 모두 CNN 기반 모델 중 가장 접근성이 좋은 **ResNet50, VGG16, YOLOv5 모델 성능 비교**
* **ResNet50, VGG16**은 `ImageDataGenerator`를 사용하여 데이터 증식 후 모델링 진행
* **두 가지 인식 모델 모두 YOLOv5 모델 성능이 가장 좋아, Baseline Model로 선정**
  - 식물 인식 모델 성능 비교
 
  ![image](https://github.com/Hyeeein/PlantDoctor/assets/81239567/96f06f0f-604a-4b4e-9019-e7ab26e2e4cb)
  
  - 식물병 인식 모델 성능 비교
    
  ![image](https://github.com/Hyeeein/PlantDoctor/assets/81239567/e822cf36-2128-4cd0-8be6-e8bd9216e861)

* YOLOv5는backbone을 depth multiple과 width multiple를 기준으로 하여 크기별로 s, m, l, x로 나눔
  - 이는 small, medium, large, xlarge로 생각하면 구분이 쉬움
  - 여기서 s가 가장 속도가 빠르지만 정확도가 비교적 떨어지고, x는 가장 느리지만 정확도가 향상됨
    ![image](https://github.com/Hyeeein/PlantDoctor/assets/81239567/e0a9be62-d075-41af-be65-555cf76baaf3)
    *[사진 출처](https://velog.io/@qtly_u/n4ptcz54)*
  - 주어진 시간 내에 많은 모델을 학습해보고, 정확도를 향상시키기 위해 s 모델을 선택하여 빠르게 모델링

### (2) 식물 인식 모델

* 

### (3) 식물병 인식 모델


## 5. 모델 구현 결과



## 6. 사업화 및 기대효과 / 발전 방향
