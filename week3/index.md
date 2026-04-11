# index
## [[induction heads]]
1. implementation on architecture - 어떻게 돌아가는지 이해했으니 인사이트를 바탕으로 다시 모델 설계
   → transformer is rnn ([[Linear Attention]]) 
   → [[FWP]] 계열, ttt 연구들의 흐름 ([[Fast weight programming and linear transformers from machine learning to neurobiology]])
   → [[nested learning]]
   → meta-rl 계열
2. [[representation vector]] - 사고 과정 뜯어보기, alignment
   [[In-Context Learning Creates Task Vectors]]
3. [[Many-Shot ICL]] - 더 극단적인 상황에서 새로운 성질이
4. math - 더 엄밀하게


## [[Path Patching]]
1. [[ACDC]]
2. Representation Engineering a.k.a [[RepE]] ([[persona axis]] 같은)
3. 수학적 보장, [[SAE]]… (여기부터는 다음 회차에 ㄱㄱ)

# [[induction heads]]

그럼 이 icl이 실제로 어떻게 수행될까?
### [[representation vector]]
> 사고 과정 뜯어보기, alignment

[[In-Context Learning Creates Task Vectors]]
### implementation on architecture
>어떻게 돌아가는지 이해했으니 인사이트를 바탕으로 다시 모델 설계하자!

결국은 그냥 hidden state에 정보 넣고, 꺼내고 하는거잖아?
→ transformer is rnn ([[Linear Attention]])
→ [[FWP]] 계열, ttt 연구들의 흐름 ([[Fast weight programming and linear transformers from machine learning to neurobiology]] (리뷰 논문))

이후에도 이런 관점에서 연구 활발히 진행 중.

개인적으로 [[nested learning]]이 굉장히 중요하다 생각. 
겉보기에는 걍 뻔한 ttt 계열이 아닌가 싶을 수 있지만, 나는 agi를 향한 구글의 포부가 숨겨져 있다 생각.

관련해 추가적인 볼거리: 
문제: [[Does Reinforcement Learning Really Incentivize ReasoningCapacity in LLMs Beyond the Base Model]] (Neurips 2025 best paper, sparse-reward rl 관점에서)
가능한 해결: r^2 (openai, 2025) 계열을 찾아보면 좋을듯.

아무튼 qk, ov circuit, induction heads 같은 추론 방식을 밝히고자 하는 연구가 이런 프론티어 연구까지 진척 시키고 있다, 하는 이야기.
# [[Path Patching]]
### [[ACDC]]
> path patching 걍 노가단데 자동화하자

이거 이후로는 superposition 문제 때문에 sae와 같은 분리 방법 없이 무식하게 노이즈 넣고 결과 보고하는 방법론이 진척 어려움.
후속 연구는 테일러 근사 이용한 연산량 줄이기(EAP)나, sae를 써먹는 방법론

### Representation Engineering a.k.a [[RepE]] 
> 내부 상태를 뜯어봐서 모델의 동작 이해하고, 조작하기

path patching과는 다른 방향.
[[RepE]] 원논문

개인적으로 재밌던거 + mz: [[persona axis]], [[Emotion Concepts and their Function in a Large Language Model]]
### 수학적 보장, [[SAE]]… 
(여기부터는 다음 회차에 ㄱㄱ)