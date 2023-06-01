# opensw23-HellOSW

## Team Introduction

> 이태혁 202211350 - team_Leader
>
> 성승재 202011309 - Coder
>
> 김도현 202011257 - Github Expert
>
> 김동호 202211267 - Presentation

## -Topic Introduction

>Input에 하나의 저해상도 이미지를 넣었을 때 이를 고해상도로 변환시켜 Output으로 내보내는 문제인 **Single Image Super-Resolution**(이하 SISR)이다. SISR의 다양한 알고리즘 중 EDSR, WDSR, SRGAN 이 포함되어있다.
>
>**EDSR**은 깊은 신경망 구조를 사용하여 단일 이미지 초해상도 복원에 초점을 맞추고, **WDSR**은 넓은 활성화 함수를 사용하여 다중 이미지 초해상도 복원에 특화되어 있다.**SRGAN**은 GAN의 경쟁적인 학습을 통해 고해상도 이미지의 진짜같은 결과물을 생성하는데 초점을 맞추고 있습니다.

## -Result

<img width="860" alt="result1" src="https://github.com/albageman/opensw23-HellOSW/assets/127181219/d6914901-d6f9-4ab1-a5bf-55f3c1731595">
<img width="800" alt="result2" src="https://github.com/albageman/opensw23-HellOSW/assets/127181219/75e680f4-7ca2-4bca-8cd4-872c772b4a6b">
<img width="809" alt="result3" src="https://github.com/albageman/opensw23-HellOSW/assets/127181219/702c1c79-a662-4325-9fab-ea86b4d1f90c">


## -Analysis/Visualization

> empty

## -Installation

> conda(anaconad Prompt)가 설치 되어있어야함
>
> > 설치 방법은 installation 밑부분에 기재함.

### 1. 레파지토리를 clone 한다.

### 2. anaconda prompt를 실행한다.
<img width="586" alt="image" src="https://github.com/albageman/opensw23-HellOSW/assets/127179500/c76dfcbb-d228-4c1f-997b-cec363fdc5f8">
git clone 된 폴더로 이동한다.
<img width="864" alt="image" src="https://github.com/albageman/opensw23-HellOSW/assets/127179500/97a1cde7-4f69-4ee9-a318-dcd639c8b318">


### 3. 환경 설정

```
conda env create -f environment.yml
conda activate sisr
```
를 순차적으로 실행한다.

### 4. root파일에서 파이썬을 실행시킨다.

원하는 모델을 선택하여 그에 맞는 코드를 실행한다.

#### EDSR

```python
from model import resolve_single
from model.edsr import edsr

from utils import load_image, plot_sample

model = edsr(scale=4, num_res_blocks=16)
model.load_weights('weights/edsr-16-x4/weights.h5')

lr = load_image('demo/0851x4-crop.png')
sr = resolve_single(model, lr)

plot_sample(lr, sr)
```

![result-edsr](docs/images/result-edsr.png)

#### WDSR

```python
from model.wdsr import wdsr_b

model = wdsr_b(scale=4, num_res_blocks=32)
model.load_weights('weights/wdsr-b-32-x4/weights.h5')

lr = load_image('demo/0829x4-crop.png')
sr = resolve_single(model, lr)

plot_sample(lr, sr)
```

![result-wdsr](docs/images/result-wdsr.png)

Weight normalization in WDSR models is implemented with the new `WeightNormalization` layer wrapper of
[Tensorflow Addons](https://github.com/tensorflow/addons). In its latest version, this wrapper seems to
corrupt weights when running `model.predict(...)`. A workaround is to set `model.run_eagerly = True` or
compile the model with `model.compile(loss='mae')` in advance. This issue doesn't arise when calling the
model directly with `model(...)` though. To be further investigated ...

#### SRGAN

```python
from model.srgan import generator

model = generator()
model.load_weights('weights/srgan/gan_generator.h5')

lr = load_image('demo/0869x4-crop.png')
sr = resolve_single(model, lr)

plot_sample(lr, sr)
```

![result-srgan](docs/images/result-srgan.png)

### conda 다운 받기

miniconda Link: [miniconda][minicondalink]

[minicondalink]: https://conda.io/en/main/miniconda.html "Go miniconda download"

window용 installer을 다운받는다(다운 설정 변겅X)
anaconda prompt가 설치되었다면 완료

-Presentation

> empty
