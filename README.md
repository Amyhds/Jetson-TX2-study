# Jetson-TX2-study

## 1. Nvidia Jetson TX2 setting     
### 1.1. Spec and components   
<img src = "https://user-images.githubusercontent.com/50664844/197373073-a68c4487-7458-4de3-a524-fe4f04ad52ca.png" width="400px">   <img src = "https://user-images.githubusercontent.com/50664844/189031340-42730b9e-e00c-4202-b4ad-f351fdbc4d81.png" width="400px">                  
* 임베디드 AI 컴퓨팅 디바이스   
* 로봇, 무인 항공기, 스마트 카메라 등의 지능형 장치에 이상적   
* [부품 소개 영상](https://youtu.be/yi6ZhDCfcPE)

### 1.2. Setting  
- 준비물
  - 우분투 18.04가 설치된 PC
jetpack을 설치할 호스트 컴퓨터  
우분투를 가상머신에 설치하면 오류가 나기 때문에 멀티부팅 혹은 우분투 전용 pc를 준비  
**※ 호스트 pc와 젯슨 보드가 같은 와이파이나 이더넷 네트워크를 사용해야 한다**  
[우분투 멀티부팅 튜토리얼 영상](https://youtu.be/KfxkGs3O_OM)  
  - Jetson TX2 보드  
  - USB Micro-B to USB A Cable  
Jetson과 호스트 pc를 연결하는 역할  
  - HDMI와 연결 가능한 모니터  
젯슨은 hdmi로만 연결이 되기 때문에 hdmi와 hdmi 포트가 있는 모니터를 준비해준다  
  - 마우스와 키보드  
젯슨에 연결, USB 허브가 있다면 쓰는 것을 추천한다

- 환경이 다 준비되었다면 초기 세팅 및 Jetapck 설치를 시작한다  
  - [젯슨 초기 세팅 영상](https://youtu.be/uve6d3ZoLL0)  
  - [Jetpack 설치 영상](https://youtu.be/Oyi-qKUcLJU)

## 2. Tensorflow installation  
[텐서플로우 설치 영상](https://youtu.be/fnkK1fUHbWM)

## 3. Jupyter notebook installation  
[주피터 노트북 설치 영상](https://youtu.be/lis633laa-A)

## 4. Google Vision API  
[구글 비젼 api 설치 영상](https://youtu.be/VjFWU1qFBWs)

## 5. Openpose  
https://github.com/CMU-Perceptual-Computing-Lab/openpose  
* 사람의 얼굴, 신체부위, 손가락을 추정하는 라이브러리로 Caffe, OpenCV 기반으로 이루어져 있다  
### 5.1. Openpose 설치  
*공식 깃허브에도 설치 메뉴얼이 있으니 참고*
```bash
git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose
cd openpose/
git submodule update --init --recursive –remote

cd {OpenPose_folder}
mkdir build/
cd build/
cmake-gui ..
```
<img src="https://user-images.githubusercontent.com/50664844/197374173-70aba59f-0e1e-4463-b6b8-64c7c1d604a9.png" width="500px">  
<img src="https://user-images.githubusercontent.com/50664844/197374176-c877ea05-a5e6-4ecf-9bd9-577d2a18969f.png" width="500px">
<img src="https://user-images.githubusercontent.com/50664844/197374223-a09e3ea6-9794-4622-b72d-823ce8e178d3.png" width="500px">

1. BUILD_PYTHON flag를 활성화시키고 Configure를 다시 클릭  
2. GPU_MODE flag는 변형하지 않고 Configure 누르기  
3. 문제가 없다면 Configuring done이 아래 박스의 마지막 줄에 뜬다  
4. Generate를 누르고 compilation이 완료되면 CMake를 끈다  
```bash
cd build/
make -j`nproc`
```
탐색기의 openpose 폴더에 들어간 후 터미널을 실행한다  
다음 명령어를 입력하면 예시동영상이 실행된다  
```bash
./build/examples/openpose/openpose.bin --video examples/media/video.avi
```
<img src = "https://user-images.githubusercontent.com/50664844/197374360-180f2ef7-a364-4538-a7bc-2baac5578f6a.png" width="400px"> 
웹캠 실행을 위해서는 다음 명령어 중 하나 입력

```bash
./build/examples/openpose/openpose.bin
./build/examples/openpose/openpose.bin --camera 0
./build/examples/openpose/openpose.bin --camera 1
```

## 6. Trt_pose  
https://github.com/NVIDIA-AI-IOT/trt_pose  
* trt_pose는 NVIDIA Jetson 환경에서 실시간 행동 인식을 목표로 한다  
* pytorch(PyTorch는 Python을 위한 오픈소스 머신 러닝 라이브러리), torchvision, alexnet을 사용  
* pytorch를 tensorRT로 변환  
### 6.1. pytorch 설치  
<img src = "https://user-images.githubusercontent.com/50664844/197374500-1d4a3801-c2fb-4f90-b1e3-521f92428247.png" width="400px">   

1. 배경화면의 Jetson Zoo 클릭   
2. pytorch 목차 클릭   
3. Jetpack 4.5, python 3.6이므로 해당하는 wheel 파일 선택   
4. 다운로드한 파일을 home 디렉토리로 옮겨줌   
5. 아래 명령문들을 그대로 입력   

```bash
# Python 2.7 (download pip wheel from above)
$ sudo apt-get install libopenblas-base libopenmpi-dev
$ pip install future torch-1.4.0-cp27-cp27mu-linux_aarch64.whl

# Python 3.6 (download pip wheel from above)
$ sudo apt-get install libopenblas-base libopenmpi-dev libomp-dev python3-pip
$ pip3 install Cython
$ pip3 install numpy torch-1.6.0-cp36-cp36m-linux_aarch64.whl
```
<img src = "https://user-images.githubusercontent.com/50664844/197374591-f173e88b-c51c-4b4d-a689-d6021691788a.png" width="500px">   

6. python으로 들어가서 import torch 입력   
7. print(torch.__version__) 입력하고 버전이 올바르게 나오면 설치 완료   

### 6.2. torchvision 설치  

```bash
sudo apt-get install libjpeg-dev zlib1g-dev
git clone -b v0.3.0 https://github.com/pytorch/vision torchvision
cd torchvision
sudo python setup.py install
(or simply - python setup.py install - if you aren't the root user)
cd ../
```  
<img src ="https://user-images.githubusercontent.com/50664844/197374881-a5134a5c-de1b-4a6d-9fe3-10e101d86e2d.png" width="500px">  

터미널에서 python으로 들어가서 import torch, import torchvision 입력 후 print(torchvision.__version__) 입력 후 버전 정보가 나오면 설치 성공   

**※ 만약 “ImportError: cannot import name ‘PILLOW_VERSION’”오류가 생긴다면 다음 명령어를 입력해서 다운그레이드 해줍니다**  
```bash
pip install pillow==6.2.1
```  

**※ 만약 “error: command ‘aarch64-linux-gnu-gcc’ failed with exit status 1”오류가 생긴다면 다음 명령어 입력**
```bash
Control + d  
sudo apt-get install -y libssl-dev zlib1g-dev gcc g++ make  
git clone https://github.com/edenhill/librdkafka  
cd librdkafka
./configure --prefix=/usr
make
sudo make install
cd ../
```

### 6.3. pre-trained model 다운로드
https://github.com/NVIDIA-AI-IOT/trt_pose#step-3---run-the-example-notebook  
위 링크에서 resnet18을 다운로드하고 tasks/human_pose 디렉토리에 옮긴다

### 6.4. torch2trt, trt_pose, jetcam 다운로드 
1. torch2trt  
```bash
git clone https://github.com/NVIDIA-AI-IOT/torch2trt
cd torch2trt
sudo python3 setup.py install –plugins
sudo pip3 install tqdm cython pycocotools
sudo apt-get install python3-matplotlib
```
2. trt_pose  
```bash
git clone https://github.com/NVIDIA-AI-IOT/trt_pose
cd trt_pose
sudo python3 setup.py install
```
3. jetcam  
```bash
git clone https://github.com/NVIDIA-AI-IOT/jetcam
cd jetcam
sudo python3 setup.py install
```

### 6.5. trt_pose 실행  
<img src ="https://user-images.githubusercontent.com/50664844/197375362-89a88688-0159-4346-ae3f-58d83b5ae06a.png" width="500px">

1. Chromium 실행  
2. 터미널 열고 jupyter notebook 입력  
3. trt_pose/tasks/human_pose/live_demo.ipynb 실행  
4. Run으로 셀 하나씩 실행  

**※ 만약 OSError: /usr/lib/aarch64-linux-gnu/libgomp.so.1: cannot allocate memory in static TLS block 라는 오류가 생기면 주피터 노트북을 종료 후 다음 명령어를 입력한다**
```bash
$ export LD_PRELOAD=/usr/lib/aarch64-linux-gnu/libgomp.so.1 
$ source ~/.bashrc 
```

## 7. Multi-person Real-time Action Recognition Based-on Human Skeleton    
https://github.com/felixchenfy/Realtime-Action-Recognition  
‘stand’, ‘walk’, ‘run’, ‘jump’, ‘sit’, ‘squat’, ‘kick’, ‘punch’, ‘wave’의 9가지 동작을 구분할 수 있는 행동인식 오픈소스  
### 7.1. tf-pose-estimation 설치  
```bash
export MyRoot=$PWD
cd src/githubs  
git clone https://github.com/felixchenfy/ildoonet-tf-pose-estimation
mv ildoonet-tf-pose-estimation tf-pose-estimation
```
### 7.2. MRAR 설치
```bash
conda create -n tf tensorflow-gpu
conda activate tf

cd $MyRoot/src/githubs/tf-pose-estimation
pip3 install -r requirements.txt
pip3 install jupyter tqdm

# Install tensorflow.
# You may need to take a few tries and select the version that is compatible with your cuDNN. If the version mismatches, you might get this error: "Error : Failed to get convolution algorithm."
pip3 install tensorflow-gpu==1.13.1
# Compile c++ library as described [here](https://github.com/felixchenfy/ildoonet-tf-pose-estimation#install-1):
sudo apt install swig
pip3 install "git+https://github.com/philferriere/cocoapi.git#egg=pycocotools&subdirectory=PythonAPI"
cd $MyRoot/src/githubs/tf-pose-estimation/tf_pose/pafprocess
swig -python -c++ pafprocess.i && python3 setup.py build_ext –inplace
cd $MyRoot
pip3 install -r requirements.txt
```
설치가 완료되면 다음 명령어를 실행시켜 예시 이미지를 확인  

```bash
cd $MyRoot/src/githubs/tf-pose-estimation
python run.py --model=mobilenet_thin --resize=432x368 --image=./images/p1.jpg
```

```bash
python src/s5_test.py \
    --model_path model/trained_classifier.pickle \
    --data_type webcam \
    --data_path 0 \
    --output_folder output
#model_path는 훈련 모델의 경로
data_type은 입력 데이터의 종류(비디오, 이미지, 웹캠 가능)
output_folder는 출력 결과의 경로
```
## 8. ActionAI  
https://github.com/smellslikeml/ActionAI  
* 행동분류 머신러닝 모델의 훈련을 위한 파이썬 라이브러리  
* 자세 추정 시 키포인트 추출을 위해 trt-pose를 사용  
* 기본 모델은 squat와 spin만 구분 가능  
* 각자가 이미지 파일을 각 클래스별로 수집해서 custom 모델을 훈련시킬 수 있음  

### 8.1. tensorflow 2.0 version
https://docs.nvidia.com/deeplearning/frameworks/install-tf-jetson-platform-release-notes/tf-jetson-rel.html#tf-jetson-rel  
여기서 텐서플로우와 jetpack 버전 호환성을 확인 후,  
https://docs.nvidia.com/deeplearning/frameworks/install-tf-jetson-platform/index.html  
이 링크를 참고해서 텐서플로우를 설치하면 된다
### 8.2. Scikit-learn, pandas 설치
```bash
pip install –U scikit-learn
pip install pandas
```
### 8.3. ActionAI 설치
```bash
git clone https://github.com/smellslikeml/ActionAI
cd ActionAI
# Assuming your python path points to python 3.x 
$ pip install -r requirements.txt
```
**※ pip install 하기 전에 requirements 문서에 들어가서 tensorflow 버전을 자신의 버전에 맞게 수정해야 한다**  
https://drive.google.com/file/d/1SkPn4vzZofCtwReodtAsnwYgVkONR5-G/view 에서 아래의 두 개의 파일을 받고 ActionAI/models에 저장한다  
<img src="https://user-images.githubusercontent.com/50664844/197375865-87d054e8-c525-41e7-95a7-599dcabb498b.png" width="400px">  

파일 저장 후 다음 명령어를 입력하면 프로그램이 실행된다
```bash
python iva.py 0
```
결과 영상은 out.mp4로 저장된다

## 9. My Graduation Thesis  
[A Study on Behavior Recognition Open Sources for Embedded Healthcare Monitoring System for the Elderly Living Alone](https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiView.kci?sereArticleSearchBean.artiId=ART002836081)
## 10. References
* https://developer.nvidia.com/embedded/jetson-tx2  
* https://github.com/developer0hye/TX2-JetPack-Installation-Guide-Kr  
* https://medium.com/@nomaishere/jetson-sdk-manager%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%B4-jetson-tx2%EC%97%90-%EA%B0%9C%EB%B0%9C%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%B6%95%ED%95%98%EA%B8%B0-35ac7b5b3994  
* https://medium.com/hackers-terminal/installing-pytorch-torchvision-on-nvidias-jetson-tx2-81591d03ce32   
