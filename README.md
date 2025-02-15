# 연기감지를 통한 화재 예측AI 경보시스템 구축 <br>(Fire & Smoke Detection Project(Object Detection))
<br>
     
## 0. 목차
<table>
    <thead>
        <tr align=center>
            <th>번호</th>
            <th>목차</th>   
        </tr>
    </thead>
    <tbody>
        <tr align=center>
            <td>1</td>
            <td><a href="#1">주제 선정</a></td>
        </tr>
        <tr align=center>
            <td>2</td>
            <td><a href="#2">데이터 수집</a></td>
        </tr>
        <tr align=center>
            <td>3</td>
            <td><a href="#3">데이터 전처리</a></td>
        </tr>
        <tr align=center>
            <td>4</td>
            <td><a href="#4">모델 선정</a></td>
        </tr>
        <tr align=center>
            <td>5</td>
            <td><a href="#5">모델 성능 평가</a></td>
        </tr>
        <tr align=center>
            <td>6</td>
            <td><a href="#6">결과</a></td>
        </tr>
        <tr align=center>
            <td>7</td>
            <td><a href="#7">자체 평가 의견</a></td>
        </tr>
        <tr align=center>
            <td>8</td>
            <td><a href="#8">멤버 & 역할</a></td>
        </tr>
     </tbody>
</table>
<br>
       

## 1.<a name="1">주제 선정</a>
### ○ 프로젝트 주제 
- 연기감지를 통한 화재 예측 AI 경보시스템 구축<br> 

<img width="700"  src="https://user-images.githubusercontent.com/79880476/203837688-2f6c379e-0c87-49ab-a9fd-215854ca803e.jpg">

### ○ 프로젝트 기획의도 
- 매 해 반복되는 화재사고. 기존 화재감시 및 경보 시스템의 허점 대두

<img width="700"  src="https://user-images.githubusercontent.com/79880476/203837682-aa75530f-3078-4139-ac83-6471e5065e61.jpg">

### ○ 프로젝트 기간
- 2022.08.19. ~ 2022.09.02.


### ○ 프로젝트 목적
- 화재 발생 주요징후인 연기와 불꽃을 인식 가능하도록 모델을 학습 <br>
- 화재 예측 AI 기술 개발용 데이터셋 처리 및 학습기준 사전 확보 및 경험 공유<br>

### ○ 프로젝트 기대효과
- CCTV를 통해 불씨와 연기를 인식하여 자동으로 화재 예방
- 실제 화재 예측 AI 서비스 개발시 데이터셋 학습 시행착오 경감
- 화재사고 사전 예방을 통한 인명피해 및 재산피해 경감에 기여
<br>

## 2.<a name="2">데이터 수집</a>
### ○ 데이터셋
- AI Hub 화재발생 예측 영상 데이터셋 (이미지 173만장, Bbox 199만개, Polygon 26만개) 中 Vaildation의 data를 Train의 data로 사용하여 학습시킴 (약 56,000여장)<br>
<div align=center>
  <img width="1200"  src="https://user-images.githubusercontent.com/79880476/203839675-a9d5f380-ae54-49e9-af2e-729c58e2d0fd.jpg"><br>
  <a>AI HUB 데이터 량</a>
</div>
<br>
<table width="600" style="text-align: center;">
  <tr align=center>
    <td><img src="https://user-images.githubusercontent.com/79880476/203839682-a429db74-7a74-422f-9a04-80ad35a0e2c8.jpg" ></td>
    <td><img src="https://user-images.githubusercontent.com/79880476/203839668-39833364-f878-434c-9e6f-ab7ba5c27fc5.jpg" ></td>
  </tr>
  <tr align=center>
    <td><a>데이터 정보</a></td>
    <td><a>데이터의 라벨</a></td>
  </tr>
</table>
<br>

## 3.<a name="3">데이터 전처리</a>
### ○ 리사이즈(224X224,416X416,608X608)후 패딩 처리
<table style="text-align: center;">
  <tr align=center>
    <td><img src="https://user-images.githubusercontent.com/79880476/203842479-95ca0266-442c-4d22-a345-a49ba34825cf.jpg" ></td>
  </tr>
</table>

### ○ 폴리곤 좌표 → Bbox 좌표로 변환 / 상대좌표 → 절대좌표 전환
<table style="text-align: center;">
  <tr align=center>
    <td><img src="https://user-images.githubusercontent.com/79880476/203842490-bde17b46-0a99-4eef-8d99-6a9411b0ce28.jpg" ></td>
  </tr>
</table>
<br>

## 4.<a name="4">모델 선정</a>
### ○ YOLO v4 - CSPDarknet53을 Backbone으로 사용하여 실시간 객체인식 성능이 우수함
<img width="800"  src="https://user-images.githubusercontent.com/79880476/203839698-9d1cce01-933a-48db-b405-0518cb55cb93.jpg"><br>

## 5.<a name="5">모델 성능 평가</a>
### ○ 이미지 리사이즈별 성능 확인 (224X224, 416X416, 608X608)
<table style="text-align: center;">
  <tr align=center>
    <td><img src="https://user-images.githubusercontent.com/79880476/203845376-89d96aa8-665b-4ec3-b77c-d643f0cb210e.jpg" ></td>
  </tr>
</table>

### ○ ignore_thresh 설정 (max_batches = 22000 → 5500변경)
<table style="text-align: center;">
  <tr align=center>
    <td><img src="https://user-images.githubusercontent.com/79880476/203844482-7be7425c-29f9-4927-97fd-3984e22999ea.jpg" ></td>
  </tr>
</table>

### ○ IoU_thresh 설정
<table style="text-align: center;">
  <tr align=center>
    <td><img src="https://user-images.githubusercontent.com/79880476/203844474-c754ec1e-ecca-46f9-963e-a1cf966ac6c1.jpg" ></td>
  </tr>
</table>
<br>

## 6.<a name="6">결과</a>

### ○ 미세조정 
<table width="600" style="text-align: center;">
  <tr align=center>
    <td><img src="https://user-images.githubusercontent.com/79880476/203844470-a8028424-4aea-4693-aeeb-ef77c857f087.jpg" ></td>
    <td><img src="https://user-images.githubusercontent.com/79880476/203844480-3712ffbd-7c75-4826-8afc-405d49986589.jpg" ></td>
  </tr>
  <tr align=center>
    <td><a>데이터의 mAP, avg loss, precision, recall, F1-score</a></td>
    <td><a>각 클래스별 Average Precision 값</a></td>
  </tr>
</table>

### ○ 구동 예시
<table width="600" style="text-align: center;">
  <tr align=center>
    <td><img src="https://user-images.githubusercontent.com/79880476/203846874-718264d2-c73a-47fe-a5c0-c084cf5be1b8.jpg" ></td>
    <td><img src="https://user-images.githubusercontent.com/79880476/203846882-4be20492-a97a-4d12-aae4-4d2a46def792.jpg" ></td>
  </tr>
  <tr align=center>
    <td><a>이미지로 구동한 실례</a></td>
    <td><a>영상으로 구현한 실례</a></td>
  </tr>
</table>
<br>

## 7.<a name="7">자체 평가 의견</a>
### ○ 성능의 한계점 - 80% 이상의 mAP 정확도 확보에도 불구하고 실제 검출 정확도는 높지 않다.
<br>
<img width="700"  src="https://user-images.githubusercontent.com/79880476/203847522-b63ec643-f8bc-4674-95f8-6da9c6a18f0c.jpg">

### ○ 추정원인 
- 인식 대상 객체의 비정형성 (불, 연기, 안개, 구름, 빛 등)
- 학습 이미지 내용의 획일성 (장소만 바꾸어 모닥불 지핌)
- 제공해준 데이터 내의 객체 간 데이터의 불균형
<br>
<img width="700"  src="https://user-images.githubusercontent.com/79880476/203847499-3f8a28b3-6fe0-44f9-8300-3963a93a6f91.jpg">

### ○ 보완책
- 데이터 수집량 및 학습량 증대 - 더 많은 데이터를 학습시키고 추가적인 미세조정을 통한 모델 성능 개선을 실시
- 학습 이미지의 다양성 확보 - 실제 화재현장 사진이나 다양한 각도와 구도 등 보다 다양한 상황에서의 화재 데이터를 수집
- 데이터 불균형 해소 - 비교적 적은 양의 데이터를 추가로 수집하여 라벨간의 데이터 양을 동일하게 만듬
<br>

<br>

## 8.<a name="9">멤버 & 역할</a>
- 김용재 : 데이터 핸들링 (416x416), 모델 구축, 코드정리, 성능개선
- 이훈석(조장) : 모델 구축 & 성능 개선
- 오혜인 : 데이터 핸들링 (224x224), Project Manager, 성능개선
- 석민재 : 데이터 전처리, 성능 개선
- 한서연 : 데이터 핸들링 (608x608), 성능 개선

