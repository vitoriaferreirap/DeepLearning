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
## Experimento 01:
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
    - função Loss
    - Gaussian Noise (modelo não ficar "viciado" em imagens perfeitas)
    - crop_sampling (escolhe onde "cortar" a imagem para treinar)

### Métricas Treino:
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


