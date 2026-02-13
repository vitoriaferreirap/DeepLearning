# DeepLearning 

Repositório dedicado ao estudo da introdução ao Deep Learning, incluindo a implementação, visualização de algoritmos e aplicação em análise de movimento animal.

Este repositório faz parte da Iniciação Científica: **"Técnicas de Aprendizado Profundo e IA Generativa Aplicadas a Ecossistemas Inteligentes"**.

##  Referências

A base teórica de álgebra linear, cálculo e os primeiros modelos de redes neurais foram consolidados a partir da combinação de materiais de acesso aberto e orientação acadêmica específica:

* **Material Didático Público:**
    * **Repositório de Implementações:** [RC18EE - Intro to Deep Learning (Dalcimar)](https://github.com/dalcimar/RC18EE---Intro-to-Deep-Learning) – Base para os primeiros algoritmos em Python.
    * **Conteúdo em Vídeo:** [Playlist Introdução ao Deep Learning](https://www.youtube.com/watch?v=0VD_2t6EdS4&list=PL9At2PVRU0ZqVArhU9QMyI3jSe113_m2-) – Suporte teórico complementar.

* **Instrução Acadêmica:**
    * **Aulas de Mestrado:** Ciclo de 5 aulas ministradas pelo professor orientador desta Iniciação Científica, abordando tópicos avançados de aprendizado profundo, otimização e a fundamentação teórica necessária para o inicio do desenvolvimento deste projeto.

#  Anotações de Estudo

## Neural_Networks_MLP
Nesta pasta encontram-se os fundamentos necessários para entender como uma rede neural processa dados, desde um único neurônio até camadas empilhadas.

### Diferenças entre:  
* **Single Nuron (Redes Neurais de 1 Neurônio):** Foco no funcionamento básico — Pesos ($W$), Viés ($b$), Função de Soma e Ativação. É a base de tudo.
* **Multilayer Perceptron (MLP):** Quando empilhamos vários neurônios em camadas "Densa" (Dense). Aqui, a rede já é considerada "Deep Learning", mas ela ainda é "cega" para estruturas espaciais, pois precisa que a imagem seja achatada (`Flatten`) em uma única linha de números.

### Files
* **`01_tensors_vectors_matrices.ipynb`**: Estudo da base matemática para manipulação de imagens e dados multidimensionais (Tensores).
* **`02_linear_regression_gd.ipynb`**: Estudo sobre Regressão Linear e a intuição do algoritmo de Gradiente Descendente para otimização automática de pesos.
* **`03_perceptron_v1.ipynb`**: Demonstração do fluxo completo de um neurônio artificial: carregamento de classes, treinamento incremental e animação da fronteira de decisão.
* **`04_vectorization_numpy.ipynb`**: Implementação eficiente do produto escalar (Dot Product), representando o "coração" matemático do neurônio utilizando processamento paralelo com NumPy.
* **`05_fashion_mnist_mlp.ipynb`**: Aplicação de Redes Densas (MLP) na classificação de imagens. Exploração de matrizes de pixels, normalização de dados e uso da função Softmax para classificar 10 categorias de roupas.

## CNN_Computer_Vision
Nesta pasta foi iniciado o estudo de **Redes Neurais Convolucionais (CNNs)**, que são a evolução tecnológica específica para o tratamento de imagens e vídeos.

### Por que usar CNNs em vez de MLP?
* **MLP (Pasta 01):** Analisa pixels isolados. Se a orelha de um cavalo mudar de posição na foto, a MLP pode não entender que ainda é uma orelha, pois ela olha apenas para o "endereço" fixo do pixel.
* **CNN (Pasta 02):** Utiliza **Filtros (Convoluções)** que escaneiam a imagem. Ela aprende a identificar características (bordas, curvas, texturas e formas) independente de onde elas estejam na imagem. 
* **Aplicação na IC:** É a arquitetura ideal para identificar claudicação, pois consegue extrair padrões de movimento e silhueta das patas dos cavalos de forma muito mais precisa.
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