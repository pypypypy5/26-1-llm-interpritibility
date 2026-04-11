= Linear Adversarial Training
# method
복잡한 값들이 얽힌 벡터에서 특정 feature를 나타내는 벡터 추출하고 싶다. 
$\rightarrow$ 데이터를 분류하는 초평면 ($w^T h + b$)에 수직한 벡터가 바로 feature를 잘 나타내는 벡터
$\rightarrow$ [[Supervised Learning]]. 라벨이 있는 데이터에 노이즈 섞고, 그걸 강건하게 분류하는 모델을 학습시켜서 분류 초평면을 찾자.

공격자: 값에 노이즈를 섞어서 구별 어렵도록 함
판별자: 노이즈 섞인 데이터를 분류
$$\min_{\theta} \sum_{i} \max_{\|\delta\| \le \epsilon} \mathcal{L}(f_{\theta}(h_i + \delta), y_i)$$
- **$\max_{\|\delta\| \le \epsilon} \dots$**: 허용된 범위($\epsilon$) 안에서 손실(Error)을 최대화하는 최악의 노이즈를 찾습니다. (공격)
- **$\min_{\theta} \dots$**: 그 최악의 노이즈 상태에서도 손실을 최소화하도록 모델 파라미터를 업데이트합니다. (방어)
- **$f_{\theta}(h)$**: 여기서는 선형 함수 $w^T h + b$를 의미합니다.
