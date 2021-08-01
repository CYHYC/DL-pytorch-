# LSGAN

## 1.LSGAN
- Least Square Generative Adversarial Networks
- 기존의 GAN의 Discriminator는 sigmoid 함수를 사용하여 최종 출력은 0-1사이의 확률값
- GAN의 loss function은 Binary cross entropy loss로 latent vector가 만들어내는 가짜 이미지가 Discriminator를 속이기만 하면 됨
  - D = 1인 이미지가 실제 이미지와 다른 경우 발생(pearson divergence)(그림 b)
  - D(z) >> 1 인 데이터에 패널티를 줌으로써 실제 이미지의 분포에 가까운 이미지를 생성하게 함(그림 c)
![](https://user-images.githubusercontent.com/37301677/84801100-b5539680-b039-11ea-9f42-ffdcf4090603.png)

## 2. Loss function
![image](https://user-images.githubusercontent.com/86611410/127760955-bbea6775-e15b-493a-9b85-07a6e4059db7.png)
- 이름에서 추측할 수 있듯이 loss function을 기존의 BCE loss에서 L2 loss로 변경
  - Discriminator의 sigmoid 삭제
- BCE와 다르게 L2 loss는 한점에서 최소값을 가지기 때문에 학습이 안정적이고 gradient vanishing 현상 x
