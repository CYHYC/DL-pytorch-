# [Study] GAN

![](https://user-images.githubusercontent.com/37301677/94356821-94392200-00cd-11eb-8f57-5a2c2b18a2a1.png)

## 1. GAN
- 생성자(Generator)와 구별자(Discriminator) 2개의 네트워크 구조
- 정규분포를 가지는 노이즈 데이터(latent vector)로 가짜 이미지를 생성하는 생성자와
- 진짜 이미지와 가짜 이미지를 구분하는 구별자간
- 서로를 구분/속이려는 '적대적'관계를 통해서 결국은 진짜 이미지를 구분하기 어려울 정도로 가짜 이미지를 진짜 이미지처럼 생성하게 됨
![](https://user-images.githubusercontent.com/37301677/84800957-85a48e80-b039-11ea-903e-8db78dd9ddcf.png)


## 2. DCGAN
- Deep Convolution Generative Adverarial Networks
- 기존의 GAN 네트워크에 CNN을 도입

![](https://user-images.githubusercontent.com/37301677/84800962-876e5200-b039-11ea-9aaa-e59397c5fe4a.png)

## 3. LSGAN
- Least Square Generative Adversarial Networks
- 기존의 GAN의 Discriminator 사용하던 Binary(sigmoid) cross entropy loss function을 L2 loss(Least square loss)로 적용
- BCE loss는 D(z) >> 1 이여도 log(D(z))는 1로 수렴하게 되어, 가짜 이미지가 Descriminator를 진짜라고 판별해도 진짜 이미지가 아닌 pearson divergence가 발생
- L2 loss를 적용함으로써 D(z) >> 1 일 때 Loss가 커지게 설계함으로써 pearson divergence를 방지함


![](https://user-images.githubusercontent.com/37301677/84801100-b5539680-b039-11ea-9f42-ffdcf4090603.png)


- BCE loss에서 발생하는 gradient vanishing가 L2 loss에는 생기지 않기때문에 stable한 모델링 가능

![](https://user-images.githubusercontent.com/37301677/84801102-b5ec2d00-b039-11ea-9b4c-309dc37adff5.png)

## 4. CGAN
- Conditional Generative Adversarial Networks
- Generator 모델에 조건을 정의
- latent vector에 생성모델에 대한 조건(MNIST 데이터셋의 경우 0~9까지의 값)을 input으로 함
- Discriminator는 조건에 맞는 이미지인지를 판단함(GAN의 경우 이미지가 진짜/가짜 인지만 구분)

![](https://camo.githubusercontent.com/c28a6315c9c2f6bcad02c9e0e99f8ae6ff9403ef/68747470733a2f2f626c6f672e6b616b616f63646e2e6e65742f646e2f434d5950652f627471786a3047344e68342f727a57524653307a7735344c68314d79685a3437414b2f696d672e706e67)
