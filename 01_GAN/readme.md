# GAN
## 1. GAN : Generative Adversairal Networks(적대적 생성 신경망)
![](https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=http%3A%2F%2Fcfile3.uf.tistory.com%2Fimage%2F9928E6375B75872D170654)
- 실제 데이터와 비슷한 데이터를 생성하는 Generator와 데이터를 실제 데이터와 가짜 데이터로 구분하는 Discriminator는 '적대적'인 관계를 가지고 있음
  -  Generator : 실제와 비슷한 데이터를 생성해야함
  -  Discriminator : 진짜 데이터와 가짜 데이터를 구분
- Discriminator는 데이터를 잘 구분하도록 학습 / Generator는 진짜 같은 데이터를 만들어내도록 학습 → 서로를 속이는 학습을 통해서 실제와 유사한 가짜 데이터가 만들어짐
- GAN의 기본적인 개념은 label이 필요없는 비지도학습이지만, 조건(condition)을 주는 지도학습 
- 
![](https://user-images.githubusercontent.com/37301677/84800957-85a48e80-b039-11ea-903e-8db78dd9ddcf.png)

## 2. Loss funtion
![](https://github.com/Pseudo-Lab/Tutorial-Book/blob/master/book/pics/GAN-ch1img03.png?raw=true)

- Discriminator : 데이터가 진짜이면 1, 가짜이면 0의 확률값을 가지도록 학습
- Generator : 가우시안 분포를 가지는 노이즈 데이터가 진짜 데이터와 유사한 분포를 가지도록 학습


