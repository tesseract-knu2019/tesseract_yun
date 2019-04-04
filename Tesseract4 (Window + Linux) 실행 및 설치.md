# Tesseract4 (Window + Linux) 실행 및 설치

## 목표
### <span style="color:#eb6420">"한글+영어 동시 분석"</span>

**Tesseract**
ocr 오프라인 라이브러리로 다른 OCR과 달리 학습을 통해 특정 언어에 대해 향상시킬 수 있다. 이 점을 고려하여 기존에 학습된 데이터에 영어를 학습시켜 영어와 한글을 동시에 해석 가능하게 만드는 것이 최종목표이다.

* 테서렉트를 이해하고, 이를 응용하여 사진, 기사캡쳐 파일등을 해석하여 테스트를 해보자.
* 테서렉트 트레이닝 튜토리얼 ( https://github.com/tesseract-ocr/tesseract/wiki/TrainingTesseract-4.00 ) 에 따라 character단위의 +,-를 학습시켜 보자.
* 한글+영어 10%, 30%, 50%의 dataset을 학습시켜보자.


## 윈도우 환경의 테서렉트

위의 사진을 tesseract test.png out -l kor 한 결과 높은 적중률로 나오는 것을 확인하였다. 
하지만 https://github.com/tesseract-ocr/tesseract/wiki/TrainingTesseract-4.00#hardware-software-requirements 에 들어가 테서렉트를 학습시키기위한 조건을 살펴본다면 아래와 같이 리눅스와 맥에만 지원된다는 것을 알았다. 우분투에 다시 실행시켜보도록 하자!


## 리눅스 환경의 테서렉트

현재 테서렉트 최신버전 4.1.0은<span style="color:#eb6420"> 우분투 18</span>버전과 적합하다. 설치시 주의하길 바란다.

1) 관련 패키지 설치

```
$ sudo apt update
$ sudo apt install git
$ sudo apt install pkg-config
$ sudo apt install pkgconf
$ sudo apt install build-essential cmake
$ sudo apt install mesa-common-dev libglu1-mesa-dev
$ sudo apt install libglew-dev libdevil-dev libglm-dev freeglut3-dev libassimp-dev libglfw3-dev
$ sudo apt install libexiv2-dev libpulse-dev
$ sudo apt install libcanberra-gtk-module
```
2) tesseract 설치
```
git clone https://github.com/tesseract-ocr/tesseract
```
3) leptonica 설치 (cd tesseract)
```
git clone https://github.com/DanBloomberg/leptonica
cd leptonica 
mkdir build 
cd build 
cmake .. 
make 
sudo make install
```
4) tesseract lib 설치 (cd ~/tesseract )
```
sudo apt-get install libtiff5-dev
./autogen.sh
./configure ENABLE_TRAINING_TRUE=true
make
sudo make install
sudo ldconfig
make training
sudo make training-install

```
5)tessdata 넣기
별다른 지시를 하지 않는 한   /usr/local/share/tessdata 에 폴더를 확인 할 수 있을 것 이다. traineddata를 잘못 넣을시 dafafile을 열 수 없다는 오류를 볼 수 있을것이다.
https://github.com/tesseract-ocr/tesseract/wiki/Data-Files
여기 데이터를 저 폴더에 넣는것을 권장한다.

### **결과**

윈도우에서 실행시켰던 test.jpg를 실행시킨 결과 특정 기호를 제외하고는 잘 해석되는 것을 확인 하였다.



## TODO

언어 이전에 작은 단위의 기호를 먼저 학습시켜보자
