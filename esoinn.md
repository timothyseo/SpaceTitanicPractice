# esoinn

## Esoinn

#### ESOINN-DP

<figure><img src="../../.gitbook/assets/ESOINN-DP.png" alt=""><figcaption></figcaption></figure>

#### Description

An automated NNPES training framework named enhanced self-organizing incremental neural-network deep potential (ESOINN-DP). This method has three important features: (1), the automated construction of the reference dataset that requires little human intervention and with low redundancy. (2), the automated optimization of neural network structures. (3), the self-verification of trained models.

* soinn의 진화 버전으로 비지도 학습이며 군집화 모델.

원래 모델인 soinn은 두 개의 계층으로 나누어져 있으며,

1. 첫번째 계층은 입력 데이터의 밀도의 분포를 학습하며 노드와 엣지를 이용하여 분포를 표시함.
2. 두번째 레이어는 입력 데이터의 저밀도 영역을 검출하여 클러스터를 분리하고 첫번째 계층보다 더 적은 노드를 사용하여 입력 데이터의 수치 상 위치를 표시함. 두번째 계층의 학습이 종료된 후, 클러스터의 개수와 모든 클러스터의 전형적인 프로토타입 노드를 제공.

입력된 벡터의 가장 가까운 노드와 두번째로 가까운 노드를 찾아서 유사도 기준에 부합하는지 여부를 판단해서 군집화를 진행하며 첫번째 계층에서 유사도 임계값을 업데이트 하며, 새로 입력된 노드가 가장 가까운 혹은 두번째로 가까운 노드와의 유사도가 더 크면 새로운 클래스의 첫번째 노드로 분리되며 새로운 클래스 생성이 이루어진다.

이렇게 새롭게 입력되는 값들로 인한 변화와 클래스 가장가리의 위치와 거리 간 차이로 유사도 임계값이 업데이트 된다.

esoinn은 첫번째 레이어에 대한 두번째 레이어가 받는 영향이 너무 큰 단점을 보완하기 위해 레이어를 하나로 줄이고 노드 밀도를 계산해서 각 클래스들의 겹치는 구간을 찾은 다음, 가장 가까운 그리고 두번째로 가까운 노드 간의 연결 고리 를 만들어야 하는지 아닌지 판단하게 된다. 그리고 잡음을 줄이기 위해 밀도가 떨어지는 노드를 제거하는 기능이 추가됐다.

DP버전의 경우, error indicator가 추가되어 학습과 군집화 오류도 직관적으로 알 수 있다.

아래 예시는 물 클러스터링을 진행한 결과다.



#### Basic Workflow:

<figure><img src="../../.gitbook/assets/workflow.png" alt=""><figcaption></figcaption></figure>

#### Prerequisites:

```
* Anaconda with Python 3.6 and cuda 10.0 
* TensorMol-0.1 (https://github.com/jparkhill/TensorMol) 
* conda create -n esoihdnn python=3.6
* pip –-upgrade install pip

* pip install parmed tensorflow-gpu==1.14
* conda install numpy scipy scikit-learn paramiko matplotlib seaborn
* conda install -c omnia openmm
```

#### Installation of ESOI-HDNN-MD:

```
* conda activate esoihdnn
* cd ESOI-HDNN-MD
* python setup.py install
```

#### Examples:

sample NN-PES for water cluster:

<figure><img src="../../.gitbook/assets/water_example.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/error.png" alt=""><figcaption></figcaption></figure>

#### References：

* Xu, Mingyuan; Zhu, Tong; Zhang, John ZH (2021): Automated Construction of Neural Network Potential Energy Surface: The Enhanced Self-Organizing Incremental Neural Network Deep Potential Method. ChemRxiv. Preprint. https://doi.org/10.26434/chemrxiv.14370527.v1
* Xu, Mingyuan; Zhu, Tong; Zhang, John ZH (2020): Ab Initio Molecular Dynamics Simulation of Zinc metalloproteins with Enhanced Self-Organizing Incremental High Dimensional Neural Network. ChemRxiv. Preprint. https://doi.org/10.26434/chemrxiv.13207967.v1
