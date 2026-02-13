Este documento registra a comparação de métricas entre duas arquiteturas de Redes Neurais aplicadas ao dataset **Fashion MNIST**. O objetivo é validar a eficiência da extração de características espaciais em modelos de Visão Computacional.

Arquitetura | Acurácia (Treino) | Acurácia (Teste) |Loss (Teste) | Generalização
MLP (Denso)        89.4%               87.1%          0.34          Perdeu ~2.3% de precisão ao ver imagens novas.
CNN                92.0%               90.0%          0.27          Perdeu ~2.0% de precisão ao ver imagens novas.

## Análise dos Resultados
### 1. Superioridade da CNN
A Rede Neural Convolucional (CNN) apresentou um desempenho superior tanto no treino quanto na generalização. Isso ocorre porque a CNN utiliza **filtros (kernels)** que preservam a relação entre os pixels vizinhos, enquanto a MLP "achata" a imagem, perdendo a noção de estrutura.

### 2. Capacidade de Generalização
A queda de acurácia entre o treino e o teste foi menor na CNN. (Gap de Generalização)
Isso indica que a CNN é mais robusta e menos propensa a "decorar" (overfitting) a posição exata dos pixels.

### 3. Conclusão
Para o diagnóstico de imagens e vídeos, a arquitetura convolucional é melhor, pois o menor valor de **Loss (0.27)** demonstra que o modelo tem maior confiança em suas predições em comparação aos modelos densos tradicionais.