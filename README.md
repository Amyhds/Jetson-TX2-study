# Jetson-TX2-study
젯슨 삽질




Jetson TX2
SDKmanager
Jetpack 4.4

구글링해서 나온 포스트들에서 하라는 대로 다 했는데 자꾸 sdkmanager STEP 3에서 막힌다
dependency error, install error, skipped...별게 다뜬다
일단 jetpack 4.3으로 버전을 낮춰보았다...도 실패
네트워크에서 문제가 일어나는 듯 한데 분명히 같은 랜선 포트에 꼽았는데 뭐가 문제인건지..

일단 OS를 깔고 SDK를 따로 다시 깔아보았다
계속 에러가 생기지만 인내심을 갖고 retry하면 결국 깔린다!
젯슨의 터미널로 들어가서 nvcc --version을 입력하면 드디어 버전이 출력된다!!!!!!!!!

이제 YOLO를 깔아봐야겠다
