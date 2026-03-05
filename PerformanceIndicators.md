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


# Análise de métricas de Treino e Validação:
## Experimento 01:
- **Arquivo:** 03_DCL_Treinamento_de_Anotacoes_Frames
- **Configuração:** 57 frames anotados
- **Arquitetura:** ResNet-50
- **Hiperparâmetros:** 15.000 max_iterations

### 1. Métricas de Treinamento (Fase de Convergência)
- **Train Loss: 0.00225** - O erro de treino está baixo. Indica que a rede aprendeu tudo o que era possível com as 57 fotos que recebeu.
- **Valid Loss: 0.00626** - Indica que o treino está estável e a rede não está apenas "decorando" as imagens.
- **Test RMSE: 74.86 px** - A rede está na fase de "alfabetização". Ela entende o corpo do animal, mas ainda erra a distância exata dos pontos.
- **RMSE (p-cutoff 0.1): 7.32 px** - Quando a rede tem certeza do que vê, o erro é pequeno. Falta confiança para manter essa precisão no vídeo todo.
- **mAP / mAR: 33.37%** - Acurácia moderada. A rede acerta com precisão total cerca de 1/3 dos pontos.

### 2. Métricas de Validação (Generalização)
- **Train RMSE:** 167.09 
- **Test RMSE:** 74.80 

### Observação de análise:
- O Loss está baixo, o que indica que o modelo começou a aprender, porém o RMSE ainda está alto. Isso indica que a rede ainda não é especialista. 
- A diferença grande entre o RMSE de treino e de teste indica que ela entende o que é um cavalo, mas não exatamente onde fica a pata quando o ambiente ou a posição muda. 
- Há falta de dados (fotos) para chegar em métricas mais precisas.

