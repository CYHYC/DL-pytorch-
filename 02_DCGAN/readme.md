# DCGAN
## 1. DCGAN
- 기존의 GAN 구조에서 Deep Convolutional 구조로 Genernator와 Discriminator 구조를 발전시킴

### 1-1. 기존 GAN의 문제점
- MNIST 같은 단순한 이미지에서 괜찮은 성능이 나왔지만, 고해상도 이미지에 대해서 성능이 나오지 않음
- 학습시 불안정함
- latent vector가 생성하는 중간단계의 결과값이 무엇을 의미하는지 알 수 없음

### 1-2. DCGAN의 구조
![](https://camo.githubusercontent.com/60933cb11ca968e4d462a84d80728adef200ac48/68747470733a2f2f7079746f7263682e6f72672f7475746f7269616c732f5f696d616765732f646367616e5f67656e657261746f722e706e67)
1. Conv layer을 사용하여 CNN 구조를 만듦
2. CNN model과 비슷하지만, pooling layer는 사용하지 않음
3. FC layer 사용하지 않음

## 2. Latent vector
![](https://greeksharifa.github.io/public/img/2019-03-18-DCGAN/06.png)
- 학습된 모델에 z값을 바꿔가면서 생성된 이미지를 관찰해보면 Latent vector의 의미를 파악할 수 있게됨
- z 벡터의 연산, interpolation 등을 통해서 원하는 이미지 생성 가능
