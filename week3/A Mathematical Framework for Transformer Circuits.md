# 개요
간단한 1, 2 attention 레이어로 이루어진 모델에서부터 출발하여 transformer의 동작 역공학.
# method
단순한 모델부터 시작하여 레이어 층이 깊어짐에 따라 어떤 능력이 생겨나는지 분석했습니다.

- **0-Layer 트랜스포머:** 모델 내부를 보면 단순히 "바이그램(Bigram, 두 단어가 연달아 나오는 빈도)" 통계만을 모델링합니다. (예: 'San' 다음에는 'Francisco'가 온다)
    
- **1-Layer 트랜스포머:** 바이그램 모델뿐만 아니라, "스킵 트라이그램(Skip-trigram, A... B C)" 모델이 모인 앙상블처럼 작동합니다. 중간에 다른 단어가 있어도 과거의 문맥을 참조하여 다음 단어를 예측하는 기초적인 능력을 보여줍니다.
    
- **2-Layer 트랜스포머:** 여기서부터 어텐션 헤드들 간의 **결합(Composition)**이 일어나며 훨씬 복잡한 알고리즘을 구현할 수 있게 됩니다. 이 과정에서 가장 핵심적인 발견인 **귀납 헤드(Induction Heads)**가 형성됩니다.
## 결과
- **잔차 스트림 (Residual Stream을 통신 채널로 해석):** 트랜스포머 내부의 중심 데이터 흐름인 잔차 스트림을 정보가 오가는 '통신 채널'로 봅니다. 모든 어텐션 헤드는 이 스트림에서 정보를 읽어와 처리한 뒤, 그 결과를 다시 스트림에 더합니다(Additive).
    
- **QK 회로와 OV 회로 분리:** 하나의 attention head 내의 연산을 두 가지 독립적인 회로로 나누어 분석합니다.
    - **[[QK head]]:** 어느 위치의 토큰에 집중(Attend)할지 **어텐션 패턴**을 결정합니다.
    - **[[OV head]]:** 집중한 토큰의 정보가 출력(다음 단어 예측 등)에 **어떤 영향을 미칠지**를 결정합니다.
      $\rightarrow$ "Transformer is RNN" $\rightarrow$ FWP is all you need ([[Fast weight programming and linear transformers from machine learning to neurobiology]])

- [[induction heads]] 발견
# 참고
https://transformer-circuits.pub/2021/framework/index.html