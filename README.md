# DeepLearning 

Repositório dedicado ao estudo introdutório de Deep Learning, incluindo implementação, visualização de algoritmos e aplicação em análise de movimento animal.

Este repositório faz parte da Iniciação Científica: **"Técnicas de Aprendizado Profundo e Visão Computacional"**.

Os estudos aqui realizados foram desenvolvidos a partir do consumo de materiais de acesso público e de instrução acadêmica, disponíveis em [**Visualizar Documento de Referência**](Reference.md)

## Notas de Estudo
Anotações feitas ao longo dos estudos diários, com o intuito de agrupar os conhecimentos estudados e as etapas dos processos, disponíveis em [**Visualizar Documento Notas de Estudo**](Notes.md)

## Analises
Analises de performace feitas ao longo dos estudos disponíveis em [**Visualizar Documento PerformanceIndicators**](PerformanceIndicators.md)

## Pastas:
### Neural_Networks_MLP
Nesta pasta encontram-se os fundamentos necessários para entender como uma rede neural processa dados, desde um único neurônio até camadas empilhadas.

### Files
* **`01_tensors_vectors_matrices.ipynb`**: Estudo da base matemática para manipulação de imagens e dados multidimensionais (tensores).
* **`02_linear_regression_gd.ipynb`**: Estudo sobre Regressão Linear e a intuição do algoritmo de Gradiente Descendente para otimização automática dos pesos.
* **`03_perceptron_v1.ipynb`**: Demonstração do fluxo completo de um neurônio artificial: carregamento de dados, treinamento incremental e animação da fronteira de decisão.
* **`04_vectorization_numpy.ipynb`**: Implementação eficiente do produto escalar (dot product), representando o núcleo matemático do neurônio utilizando operações vetorizadas com NumPy.
* **`05_fashion_mnist_mlp.ipynb`**: Aplicação de Redes Densas (MLP) na classificação de imagens. Exploração de matrizes de pixels, normalização de dados e uso da função Softmax para classificar 10 categorias de roupas.

### CNN_Computer_Vision
Nesta pasta foi iniciado o estudo de **Redes Neurais Convolucionais (CNNs)**, que são arquiteturas específicas para o processamento de imagens e vídeos.

---

## Cronograma de Estudos e Implementações

### 01. Fundamentals
- [x] **Tensores, Vetores e Matrizes:** Base matemática para manipulação de imagens.
- [x] **Vectorization Example:** Implementação eficiente do produto escalar.
- [x] **Linear Regression & Gradiente Descendente:** Fundamentos de otimização.
- [x] **Perceptron Animation:** Visualização do aprendizado de um neurônio único.

### 02. Convolutional Neural Networks (CNN)
- [x] **Introdução às CNNs:** Estudo de filtros (kernels),rotulagem, padding, stride e mapas de características.
- [ ] **Técnicas Clássicas:** Entendendo e aplicando detecção, classificação, segmentação semântica, predição e estimativa de pose.
- [ ] **Arquiteturas Clássicas:** Entendendo o fluxo de arquiteturas de redes.
- [ ] **Data Augmentation:** Técnicas de expansão de dataset para imagens de campo (fazenda).

### 03. Applied Project: Horse Gait Analysis
- [ ] **Pose Estimation:** Pesquisa e implementação com frameworks como DeepLabCut ou SLEAP.
- [ ] **Análise de Trajetória:** Extração e tratamento de dados das patas por meio de marcadores adesivos.
- [ ] **Escrita do Artigo:** Compilação dos resultados obtidos nos testes com os cavalos.