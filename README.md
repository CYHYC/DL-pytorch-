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
- BCE loss는 D(z) >> 1 이여도 log(D(z))는 1로 수렴하게 되어, 가짜 이미지가 Discriminator를 진짜라고 판별해도 진짜 이미지가 아닌 pearson divergence가 발생
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

## 5. pix2pix
- CGAN으로 pair로 되어있는 데이터 셋을 사용해서 image translation 하는 방법
- image to image, text to image 등 pair dataset을 사용하여 다양한 output들을 만들어 낼 수 있음
- Generator loss로 Discriminator를 속이는 GAN loss와 Generator를 통해 생성된 image와 실제 image를 비교하는 L1 loss를 사용함

- Network 구조
![](https://taeoh-kim.github.io/img/code2.PNG)
  - Discriminator : patch GAN 사용
    - patch GAN? : 기존에 DCGAN이나 CGAN 은 이미지 전체를 1개로 두고 real or fake의 확률을 계산한 loss를 사용했는데, image를 N x N 의 patch 단위로 나누어서 real or fake를 보겠다는 것 → image를 분할하여 학습시킴으로써 조금더 디테일한 학습결과가 나타남

  - Generator : UNet 사용
![](https://taeoh-kim.github.io/img/code1.PNG)
    - UNet : encoder - decoder 구조에서 downsampling할 때 정보 손실이 발생하는데, 이를 보완하기 위해 downsampling 하는 중간중간 feature map을 upsampling layer에 전달함으로 정보 손실을 보완함
    
 
![](https://taeoh-kim.github.io/img/img4-2.PNG)


## 6. CyCle GAN
- pix2pix의 경우 pair dataset으로 translation하는 방법 → 데이터 취득이 쉽지 않음
- unpair dataset에서 데이터의 스타일만 가져와 translation 하는 방법 → Cycle GAN의 Main idea
![](https://raw.githubusercontent.com/dimitreOliveira/MachineLearning/master/Kaggle/I%E2%80%99m%20Something%20of%20a%20Painter%20Myself/cyclegan_horse-zebra.jpg)

### Cycle GAN의 구조
![](https://hardikbansal.github.io/CycleGANBlog/images/model.jpg)
- X-domain → Y-domain으로의 변환해주는 1개의 Generator : GAN model
- X-domain → Y-domain → X-domin 으로 다시 돌아오는 2개의 Generator : Cycle GAN model

![](https://miro.medium.com/max/2000/1*YOhXT4gecyVgpMQHsrIvsw.png)

- Discriminator는 pix2pix와 동일하게 patct GAN을 사용함
- Generator는 ResNet을 사용
![](https://www.lyrn.ai/wp-content/uploads/2019/01/CycleGAN-arch.png)
  - 단순 Encoder-Decoder 모델 보다 Encoder의 중간 정보를 Decoder로 전달해주는 UNet이 유리하지만, bottleneck 구조는 정보 손실이 발생할 수 밖에 없음

- Loss Function
- Cycle consistency loss : Generator를 통해 생성된 Y이미지가 실제 Y이미지와 같은지 비교

$ Loss_{cycle} = |G(X) - Y| + |F(Y) - X|$

- GAN Loss : Generator를 통해 생성된 이미지를 Dicriminator에서 참으로 학습하게 함

$ Loss_{GAN} = log(D(G(X)) + log(D(F(Y)) $

- Identity Loss
