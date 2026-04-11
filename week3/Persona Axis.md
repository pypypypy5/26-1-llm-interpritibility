---
dg-publish: true
localGraph: true  # 로컬 그래프 활성화
globalGraph: true  # 글로벌 그래프 (선택)
---
# experiments
### 1. 다양한 캐릭터 데이터 수집 (Role-playing Prompts)

연구진은 모델이 취할 수 있는 다양한 정체성을 확인하기 위해 **275가지의 캐릭터 아키타입(Archetypes)**을 선정했습니다. 여기에는 '편집자', '광대(Jester)' 같은 현실적인 역할부터 '유령', '고대 유물' 같은 환상적인 존재까지 포함되었습니다.

- **추출 방법:** 각 캐릭터를 연기하도록 시스템 프롬프트를 준 뒤, 모델이 답변을 생성하게 합니다. 이때 모델 내부에서 발생하는 수만 차원의 숫자 배열인 '활성화 값(Activations)'을 기록합니다.
    

### 2. 활성화 벡터 추출 (Extracting Residual Stream)

모델의 여러 층(Layer) 중 정보가 통합되는 통로인 **'잔차 연결(Residual Stream)'**에서 활성화 데이터를 추출했습니다.

- **대상:** 주로 모델의 **중간 레이어**(예: Gemma 2 27B의 경우 22번째 레이어)를 타겟으로 합니다. 너무 앞쪽 레이어는 단순 문법을 처리하고, 너무 뒤쪽은 최종 단어 선택에 집중하기 때문입니다.
    
- **평균화:** 한 페르소나에 대한 여러 답변 내의 모든 토큰(단어 조각)에서 나온 활성화 값을 평균 내어, 해당 캐릭터의 고유한 '지문'과 같은 **역할 벡터(Role Vector)**를 만듭니다.
    

### 3. 주성분 분석(PCA)을 통한 공간 지도화

추출된 275개의 고차원 역할 벡터들을 **주성분 분석(PCA)**이라는 통계 기법을 통해 저차원(2D 또는 3D)으로 시각화했습니다. PCA는 데이터에서 변동성이 가장 큰 방향을 찾아내는 기법입니다.

- **결과:** 놀랍게도 이 공간에서 가장 큰 변동을 설명하는 첫 번째 축(PC1)이 바로 **'도움이 되는 비서(Assistant)'인지 아닌지**를 결정하는 축임이 드러났습니다. 이를 **'Assistant Axis'**라고 명명했습니다.

# 결과
## llm의 hidden state

word embedding vector들의 sequence -attention→ hidden vector sequence

이때 hidden vector sequence를 행렬로 볼 수 있으니 이걸 hidden state.

## [[linear subspace]]

## persona axis

hidden state를 이루는 벡터들은 모두 하나의 2,3차원짜리 linear subspace안에 존재하는데, 이 subspace가 대화에서의 persona를 정의한다.

특히 이 평면 안에서도 특정 방향으로 갈수록 해당 페르소나의 성향이 짙어지는데, 이걸 persona axis라고 부르기로 한거.

+) 시스템 프롬프트 필요없이, assistant 방향으로 더해주기만 해도 같은 효과가 나온다.

## persona drift

처음에 assistant로 설정해둬도, 대화 도중에 감정, 철학적 질문과 같은게 섞이면 subspace에서 이탈하여 다른 subspace로 이동하는 현상 발생한다.

이유는 attention 과정에서 새로 들어온 감정, 철학 벡터가 hidden state에 추가로 더해지며 기존의 persona가 약해지고 감정적 표현에 맞는 페르소나 쪽으로 이동하는 것.

→ persona drift!

## 분포

초기 층: 시퀀스에서 국소적인 의미, 문법 등을 처리하는 부분이라 persona 강하지 않다

중간 층: hidden state를 받아 본격적인 사고를 진행하는 층이라 persona 경향성이 가장 강하다

후기 층: 사고 바탕으로 구체적인 단어 선택에 집중해야 해서 persona 경향이 다시 약해짐

# 참고
[https://arxiv.org/abs/2601.10387](https://arxiv.org/abs/2601.10387)
