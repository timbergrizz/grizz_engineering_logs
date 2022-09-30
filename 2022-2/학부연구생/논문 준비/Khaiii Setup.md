# 사용 데이터 / 스펙
- 모두의 말뭉치 데이터를 바탕으로 실험을 진행할 것이다.
- 실험 PC 
	- CPU : Intel i7-12700 / RAM : 32GB / GPU : RTX 3080 TI
	- OS : Windows 11 / WSL2 Ubuntu 22.08
	- Docker Version : Desktop 4.12.0
- 실험 서버
	- CPU : AMD EPYC 7282 / RAM : 128GB / GPU : RTX 3080 * 2
	- OS : Ubuntu 18.08

# 도커 이미지
- 공식 문서에서 제공하는 도커 파일이 개판이다. 신난다 아주.
	- pytorch 기존 이미지에 cmake랑 gcc같은게 포함되어있는지 모르겠어서 뭐라 말은 못하겠는데 여튼 잘 안된다. 
- 우선 처음은 WSL에서 설치를 진행했고, 이후 서버로 옮겨서 이미지를 생성했다.

- 여튼 도커파일 수정해서 다음과 같이 작성했다.
	- 빌드파일 생성 + 빌드까지는 도커 파일에 포함해도 될 것 같다.
```Dockerfile
FROM pytorch/pytorch:latest
MAINTAINER nako.sung@navercorp.com

RUN apt-get update -y
RUN apt-get install -y language-pack-ko
RUN apt-get install -y git
RUN apt-get install -y build-essential

RUN git clone https://github.com/kakao/khaiii.git
WORKDIR /workspace/khaiii

RUN pip install cython
RUN pip install --upgrade pip
RUN pip install -r requirements.txt

RUN mkdir build
WORKDIR /workspace/khaiii/build

RUN cmake ..
RUN make all
RUN make resource

RUN locale-gen en_US.UTF-8
RUN update-locale LANG=en_US.UTF-8
```

## 이후 도커 셋업
- 작성된 도커파일을 바탕으로 이미지를 다음과 같이 생성하고 실행할 수 있다.
```bash
docker build . -t khaiii_test:latest
docker run -d -it --gpus=all khaiii_test
```
- 이후 컨테이너에 접속하여 pip에 추가적인 세팅을 필요로 한다.
	- 도커파일에 반영을 하면 좋을 듯 하다. 지금은 귀찮아서 나중에 하도록 하자.
- 그와중에 vim도 안깔려있어서 apt-get으로 neovim 깔아줬다
``` shell
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install neovim
```


# 레퍼런스
https://provia.tistory.com/56