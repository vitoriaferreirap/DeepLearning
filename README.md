# DeepLearning 

Repositório dedicado ao estudo da introdução ao Deep Learning, incluindo a implementação, visualização de algoritmos e aplicação em análise de movimento animal.

Este repositório faz parte da Iniciação Científica: **"Técnicas de Aprendizado Profundo e IA Generativa Aplicadas a Ecossistemas Inteligentes"**.

##  Referências (Fundamentals)

A base teórica de álgebra linear, cálculo e os primeiros modelos de redes neurais foram consolidados a partir da combinação de materiais de acesso aberto e orientação acadêmica específica:

* **Material Didático Público:**
    * **Repositório de Implementações:** [RC18EE - Intro to Deep Learning (Dalcimar)](https://github.com/dalcimar/RC18EE---Intro-to-Deep-Learning) – Base para os primeiros algoritmos em Python.
    * **Conteúdo em Vídeo:** [Playlist Introdução ao Deep Learning](https://www.youtube.com/watch?v=0VD_2t6EdS4&list=PL9At2PVRU0ZqVArhU9QMyI3jSe113_m2-) – Suporte teórico complementar.

* **Instrução Acadêmica:**
    * **Aulas de Mestrado:** Ciclo de 5 aulas ministradas pelo professor orientador desta Iniciação Científica, abordando tópicos avançados de aprendizado profundo, otimização e a fundamentação teórica necessária para o inicio do desenvolvimento deste projeto.

##  Anotações de Estudo

###  /Fundamentals
Nesta pasta encontram-se os fundamentos necessários para entender como a rede neural processa dados:

* **01_tensores_vetores_matrizes**: Estudo da base matemática para manipulação de imagens e dados multidimensionais.
* **vectorization_example.ipynb**: Implementação eficiente do produto escalar, representando o mecanismo de soma e ativação (núcleo) de um neurônio.
* **linear_regr_gd2**: Estudo sobre Regressão Linear e a intuição do algoritmo de Gradiente Descendente para otimização de pesos.
* **perceptron_animation.ipynb**: Demonstração do fluxo completo de um neurônio artificial (Perceptron):
    * Carregamento e visualização da distribuição das classes.
    * Treinamento incremental com registro de pesos e bias.
    * Animação da evolução da fronteira de decisão durante o aprendizado.

---

##  Cronograma de Estudos e Implementações

### 01. Fundamentals
- [x] **Tensores, Vetores e Matrizes:** Base matemática para manipulação de imagens.
- [x] **Vectorization Example:** Implementação eficiente do produto escalar.
- [x] **Linear Regression & Gradiente Descendente:** Fundamentos de otimização.
- [x] **Perceptron Animation:** Visualização do aprendizado de um neurônio único.

### 02. Convolutional Neural Networks (CNN)
- [ ] **Introdução às CNNs:** Estudo de Filtros (Kernels), Padding, Stride e Mapas de Características.
- [ ] **Arquiteturas Clássicas:** Entendendo o fluxo de redes como LeNet-5 e ResNet.
- [ ] **Data Augmentation:** Técnicas de expansão de dataset para imagens de campo (fazenda).

### 03. Applied Project: Horse Gait Analysis
- [ ] **Pose Estimation:** Pesquisa e implementação com frameworks como DeepLabCut ou SLEAP.
- [ ] **Análise de Trajetória:** Extração e tratamento de dados das patas via marcadores adesivos.
- [ ] **Escrita do Artigo:** Compilação dos resultados obtidos nos testes com os cavalos.