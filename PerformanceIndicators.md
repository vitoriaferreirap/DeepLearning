Este documento registra a comparação de métricas entre duas arquiteturas de Redes Neurais aplicadas ao dataset **Fashion MNIST**. O objetivo é validar a eficiência da extração de características espaciais em modelos de Visão Computacional.

- Arquitetura: MLP (Denso) | CNN 
- Acurácia (Treino):  89.4 | 92.0% 
- Acurácia (Teste):  87.1% | 90.0%
- Loss (Teste):  0.34 | 0.27
- Generalização: Perdeu ~2.3% | Perdeu ~2.0%

## Análise dos Resultados
### 1. Superioridade da CNN
A Rede Neural Convolucional (CNN) apresentou um desempenho superior tanto no treino quanto na generalização. Isso ocorre porque a CNN utiliza **filtros (kernels)** que preservam a relação entre os pixels vizinhos, enquanto a MLP "achata" a imagem, perdendo a noção de estrutura.

### 2. Capacidade de Generalização
A queda de acurácia entre o treino e o teste foi menor na CNN. (Gap de Generalização)
Isso indica que a CNN é mais robusta e menos propensa a "decorar" (overfitting) a posição exata dos pixels.

### 3. Conclusão
Para o diagnóstico de imagens e vídeos, a arquitetura convolucional é melhor, pois o menor valor de **Loss (0.27)** demonstra que o modelo tem maior confiança em suas predições em comparação aos modelos densos tradicionais.

- Usando mátematica básica para achar o numero adquado de epocas e interações para cada banco de dados, pensando em seu tamanho.

# Análise de métricas de Treino e Validação:
## Experimento 1:
- **Arquivo:** 03_DCL_Treinamento_de_Anotacoes_Frames
- **Configuração:** 270 frames anotados e 15 para teste
- **Arquitetura:** ResNet-50 / engine: tensorflow
- **Resolução Imagens** 448 x 448
- **Hiperparâmetros:** - Épocas: 700;
    - Batch_size= 8;
    - displayiters=100;
    - augmenter_type='imgaug';
        - Rotação (Rotation): 30 graus
        - Escala (Scaling): Entre 0.5 e 1.25
        - Motion Blur: Ativado (True). Isso simula o rastro de movimento
    - Learning_rate inicial = lr: 0.0005
    - scheduler: (MultiStep Scheduler ajuste fino no momento do treino)
        - lr_list:
            - lr_list: [0.0001, 1e-05]
            - Milestones: [300, 600]
- **Parâmetros de configuração YAML**
    - p-cutoff: 0.5
    - Gaussian Noise (modelo não ficar "viciado" em imagens perfeitas)
    - crop_sampling (escolhe onde "cortar" a imagem para treinar)
### Métricas Treino:
    - train loss 0.00099
    - valid loss 0.00421
    - metrics/test.rmse:           27.75
    - metrics/test.rmse_pcutoff:   5.86
    - metrics/test.mAP:            86.08
    - metrics/test.mAR:            88.00
### Métricas de Validação (Generalização)
    - train rmse             24.92
    - train rmse_pcutoff      6.36
    - train mAP             83.91
    - train mAR             87.81
    - test rmse             27.75
    - test rmse_pcutoff      8.43
    - test mAP              86.08
    - test mAR              88.00
## Refinamento (Fine-tuning)
## Experimento 1.1:
- **1)** O aumento do p-cutoff para 0.8 demonstrou que a rede ResNet-50 já possui um alto grau de aprendizado, e que o erro anterior de 8.43 era causado por oclusões momentâneas. Ao filtrar pontos com confiança inferior a 80%, obteve-se um erro de generalização de 5.44 pixels, validando a eficácia do primeiro treinamento.
- **2)** Identificar frames com problemas de coerência física, focando no problema principal:A Confiança (0.8) com intuito de corrigir notação manual. O DeepLabCut escolhe dos 77 erros os 30 mais representativos dos encontrados (os piores erros ou os mais variados) para não perder tempo corrigindo frames que são muito parecidos entre si.
    - Observaçãoes sobre correção de frames com erro: ao corrigir manualmente os frames extraidos com erros, notei muitas trocas no ponto dos cascos, onde o modelo erra muito em identificar cascos traseiros e dianteiros, assim como externos e internos, outro erro menos aparente são pontos flutuantes e existentes onde a parte em si está ocluida, pontos dos quais exclui na edição. (necessário fazer merge entre arquivos editados e dataset)
- **3)** Em vez de começar do zero, o modelo carrega tudo o que já sabe sobre o cavalo.Ele foca apenas em aprender a corrigir os erros desses novos frames corrigidos. Em vez de 700 épocas, roda 200 épocas em cima do que já tem. O modelo "ajusta a mira". O conhecimento antigo é preservado e os erros novos são corrigidos.
### Métricas Treino:
    - train loss 0.00191
    - valid loss 0.00347
    - metrics/test.rmse:          99.51
    - metrics/test.rmse_pcutoff:   7.89
    - metrics/test.mAP:           38.47
    - metrics/test.mAR:           46.67
### Métricas de Validação (Generalização)
    - train rmse             89.82
    - train rmse_pcutoff      3.26
    - train mAP              38.10
    - train mAR              45.19
    - test rmse             118.68
    - test rmse_pcutoff       4.22
    - test mAP               38.72
    - test mAR               44.67

