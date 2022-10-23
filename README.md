# Jetson-TX2-study

## 1. Nvidia Jetson TX2 setting     
### 1.1. Spec and components   
<img src = "https://user-images.githubusercontent.com/50664844/197373073-a68c4487-7458-4de3-a524-fe4f04ad52ca.png" width="400px">   <img src = "https://user-images.githubusercontent.com/50664844/189031340-42730b9e-e00c-4202-b4ad-f351fdbc4d81.png" width="400px">                  
* 임베디드 AI 컴퓨팅 디바이스   
* 로봇, 무인 항공기, 스마트 카메라 등의 지능형 장치에 이상적   
* [부품 소개 영상](https://youtu.be/yi6ZhDCfcPE)

### 1.2. Setting  
- 우분투 18.04가 설치된 PC
jetpack을 설치할 호스트 컴퓨터  
우분투를 가상머신에 설치하면 오류가 나기 때문에 멀티부팅 혹은 우분투 전용 pc를 준비  
**호스트 pc와 젯슨 보드가 같은 와이파이나 이더넷 네트워크를 사용해야 한다**  
[우분투 멀티부팅 튜토리얼 영상](https://youtu.be/KfxkGs3O_OM)  
- Jetson TX2 보드  
- USB Micro-B to USB A Cable  
Jetson과 호스트 pc를 연결하는 역할  
- HDMI와 연결 가능한 모니터  
젯슨은 hdmi로만 연결이 되기 때문에 hdmi와 hdmi 포트가 있는 모니터를 준비해준다  
- 마우스와 키보드  
젯슨에 연결, USB 허브가 있다면 쓰는 것을 추천한다

환경이 다 준비되었다면 초기 세팅 및 Jetapck 설치를 시작한다  
[젯슨 초기 세팅 영상](https://youtu.be/uve6d3ZoLL0)  
[Jetpack 설치 영상](https://youtu.be/Oyi-qKUcLJU)

## 2. Tensorflow installation  
[텐서플로우 설치 영상](https://youtu.be/fnkK1fUHbWM)

## 3. Jupyter notebook installation  
[주피터 노트북 설치 영상](https://youtu.be/lis633laa-A)

## 4. Google Vision API  
[구글 비젼 api 설치 영상](https://youtu.be/VjFWU1qFBWs)

## 5. Openpose  
https://github.com/CMU-Perceptual-Computing-Lab/openpose  
* 사람의 얼굴, 신체부위, 손가락을 추정하는 라이브러리로 Caffe, OpenCV 기반으로 이루어져 있다


## 6. Trt-pose  
https://github.com/NVIDIA-AI-IOT/trt_pose  

## 7. ActionAI  
https://github.com/smellslikeml/ActionAI 

## 8. My Graduation Thesis  
[A Study on Behavior Recognition Open Sources for Embedded Healthcare Monitoring System for the Elderly Living Alone](https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiView.kci?sereArticleSearchBean.artiId=ART002836081)
## 9. References
* https://developer.nvidia.com/embedded/jetson-tx2  
* https://github.com/developer0hye/TX2-JetPack-Installation-Guide-Kr  
* https://medium.com/@nomaishere/jetson-sdk-manager%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%B4-jetson-tx2%EC%97%90-%EA%B0%9C%EB%B0%9C%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%B6%95%ED%95%98%EA%B8%B0-35ac7b5b3994  
