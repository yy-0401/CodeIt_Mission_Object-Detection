# CodeIt_Mission_Object-Detection
객체 인식에 대한 강의 이론을 미션 7 실습을 통해 확인한다.

# 계획서
## 연구 목적 : 객체 인식에 대한 강의 이론을 미션 7 실습을 통해 확인한다.
  참고 코드잇 [AI] 스프린트 미션 7 https://www.codeit.kr/topics/sprint-ai-mission-7/lessons/11967
## 데이터정보 및 환경설정
### 데이터셋 소개 (The Oxford-IIIT Pet Dataset)
**출처: 캐글 - 옥스포드-IIIT 반려동물 데이터셋, https://www.kaggle.com/datasets/devdgohil/the-oxfordiiit-pet-dataset**

**Context**

<br>Oxford-IIIT Pet Dataset은 옥스퍼드 대학교 시각 기하학 그룹에서 제작한 37개 카테고리의 반려동물 데이터셋으로, 각 카테고리별로 약 100장의 이미지가 포함되어 있습니다. 이미지들은 크기, 자세, 조명 등에서 큰 변화를 보입니다. 모든 이미지에는 품종, 머리 영역(ROI), 픽셀 단위의 트라이맵 분할에 대한 정답 주석이 함께 제공됩니다.

**README**

<br>Omkar M Parkhi, Andrea Vedaldi, Andrew Zisserman, CV Jawahar 저희는 각 클래스당 약 200장의 이미지로 구성된 37개 카테고리의 반려동물 데이터셋을 제작했습니다. 이미지들은 크기, 자세, 조명 면에서 큰 변화를 보입니다. 모든 이미지에는 품종, 머리 ROI, 픽셀 수준의 트라이맵 분할에 대한 정답 주석이 함께 제공됩니다. 
구성: 

-------- 

trimaps/ 데이터셋의 모든 이미지에 대한 트리맵 주석 
				<br>픽셀 주석: 1: 전경 2: 배경 3: 분류되지 않음 
<br>xmls/ PASCAL VOC 형식의 머리 경계 상자 주석 list.txt 데이터셋의 모든 이미지 목록 파일의 각 항목은 다음과 같은 형식을 갖습니다. 
<br>이미지 CLASS-ID SPECIES BREED ID 
<br>ID: 1~37 클래스 ID 
<br>SPECIES: 1 == 고양이, 2 == 개 
<br>BREED ID: 1~25 == 고양이, 1~12 == 개 
<br>첫 글자가 대문자인 이미지는 고양이 이미지이고, 첫 글자가 소문자인 이미지는 개 이미지입니다. trainval.txt 논문에서 사용된 분할 방식을 설명하는 파일입니다. test.txt 임의의 분할 방식을 시도해 보는 것을 권장합니다. 
<br>지원: 

------- 

문의 사항은 Omkar Parkhi(omkar@robots.ox.ac.uk)에게 연락하십시오. 
<br>참고 문헌: 

---------- 

[1] OM Parkhi, A. Vedaldi, A. Zisserman, CV Jawahar Cats and Dogs IEEE Conference on Computer Vision and Pattern Recognition, 2012 
참고: 

---- 

데이터 세트는 연구 목적으로만 제공됩니다. 이 이미지를 사용할 때는 원본 웹사이트의 이용 약관을 준수해야 합니다. 웹사이트 목록은 [1]을 참조하십시오.
  - 데이터 불러오기
  <br>- 환경 설정
  <br>- 
### EDA
- 바운딩 박스는 올바르게 되어있나?
  <br>목적 : 라벨이 똑바로 안돼어 있으면 학습에 지장을 주기에 확인한다.
  <br>-> print : xml 라벨 각 클래스별로 2개씩 랜덤으로 확인하기 
  <br>-> 바운딩 박스가 없는 이미지가 있는가?
- 리드미에서 말한 데이터대로 되어 있나? 
  <br>목적 : 설명 자체가 신뢰할 수 있는지 확인한다.
  <br>-> 1은 고양이, 2는 개가 맞는가?
  <br>-> 고양이는 1~25개의 품종이고 개는 1~12 품종이 맞는가?(BREED)
- 데이터 균형은 맞는가?(특정 품종의 사진이 적거나 많거나 하지 않는가?)
  <br>목적 : 정규화가 잘 진행되었는지 확인한다.
  <br>-> 리드미에서 클래스별로 약 200장이라는데 맞는가? 총 37개의 클레스에 몇장씩 있는지 확인하자
  <br>이건 표로 print해서 확인한다.   
- 파일 싸이즈는 다 같은가? (정규화로 픽셀을 바꾼거지 이미지 싸이즈는 그대로일듯)
  <br>목적 : 
  <br>-> 이미지 싸이즈가 너무 다른 것들은 없는가?
데이터 전처리 및 분할 (Train / Test Split)
- 하드웨어 및 소프트웨어 개발 환경
- **방법론**
    - Custom CNN + Sliding Window 아키텍처
    - SSD (Single Shot MultiBox Detector) 아키텍처
    - YOLO (You Only Look Once) 아키텍처
    - 모델별 객체 인식 접근 방식 및 특징 비교
- **실험 결과 및 분석**
    - 평가지표 정의 (mAP, Inference Time, FPS, IoU)
    - 모델별 성능 평가 비교 (종합 결과 테이블)
    - 학습 성능 곡선 분석 (Loss / Accuracy Graph)
    - 실제 객체 탐지 바운딩 박스 시각화 결과 비교
- **결론 및 향후 과제**
    - 연구 결론 요약
    - 한계점 및 향후 연구 발전 방향
