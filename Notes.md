# MLP & CNN 
* **Single Neuron (Rede Neural de 1 Neurônio):** Foco no funcionamento básico — Pesos ($W$), Viés ($b$), Função de Soma e Ativação. É a base de tudo.
* **Multilayer Perceptron (MLP):** Quando empilhamos vários neurônios em camadas "Dense" (Densas). Aqui, a rede já é considerada "Deep Learning", mas ainda é "cega" para estruturas espaciais, pois precisa que a imagem seja achatada (`Flatten`) em uma única dimensão de números.

### Por que usar CNNs em vez de MLP?
* **MLP (Pasta 01):** Analisa pixels isolados. Se a orelha de um cavalo mudar de posição na foto, a MLP pode não reconhecer que ainda é uma orelha, pois observa apenas o "endereço" fixo do pixel.
* **CNN (Pasta 02):** Utiliza **Filtros (Convoluções)** que percorrem a imagem. Aprende a identificar características (bordas, curvas, texturas e formas) independentemente de onde estejam posicionadas na imagem. 

# 19/02
- Preparar dados (Rotulagem/Anotação) — ensinando o modelo onde estão os objetos.
- Criar uma base de dados organizada de imagens.
- Aprender a rotular manualmente.
- Exportar arquivo no formato COCO JSON.
- Validação das anotações (verificar se as caixas estão corretas nas imagens).

## YOLOv8 (Arquitetura)
- Iniciando entendimento sobre a Arquitetura YOLOv8

## Entendendo conceitos:
### Detecção (Object Detection)
- Identifica a localização de vários objetos na imagem.
- Entrada: uma imagem.
- Saída: uma lista de objetos detectados dentro da imagem, com suas respectivas classes e bounding boxes.

### Classificação 
- Identifica classes na imagem, mas **não** a localização.
- Entrada: uma imagem.
- Saída: classe atribuída à imagem inteira.

### Segmentação
- Classifica cada pixel da imagem.
- Pode ser semântica (todas as instâncias da mesma classe juntas) ou por instância (cada objeto separado).

### Pose
- Estima a posição de pontos-chave (keypoints) de um objeto ou ser vivo.
- Saída: coordenadas dos pontos anatômicos relevantes.

### Predição
- Inferência realizada pelo modelo treinado.
- Entrada: novos dados que o modelo nao conhece.
- Saída: estimativa baseada no que foi aprendido durante o treinamento.

# 20/02

## Arquiterua YOLOv8
- Compreensão da base da arquitetura: imports, configurações, treinamento (.train()), validação (.val()) e inferência (.predict()).
https://docs.ultralytics.com/models/yolov8/#segmentation-coco
### Escolha da Técnica e Modelos
- Detection: yolov8n.pt
- Instance Segmentation: yolov8n-seg.pt
- Pose/Keypoints: yolov8n-pose.pt
- Oriented Detection: yolov8n-obb.pt
- Classification: yolov8n-cls.pt
- Escalabilidade: Cada tamanho de modelo (n, s, m, l, x) possui um equilíbrio diferente entre performance (precisão) e consumo de hardware (velocidade/memória).
- Parâmetros:
    - Argumentos Básicos: São universais (ex: epochs, imgsz, batch).
    - Argumentos Específicos: Existem parâmetros que só fazem sentido para certas técnicas (ex: parâmetros de máscara ou pontos de articulação).
- Segmentação engloba a Detecção: Ao treinar um modelo de Segmentação (-seg.pt), o resultado sempre terá o atributo .boxes (a caixa) preenchido além do .masks (a máscara). A lógica da arquitetura segue esta ordem:
    - 1.Extração de Características: Identifica se "algo" existe na imagem.
    - 2.Detecção: Desenha um quadrado (Bounding Box) em volta desse "algo" para delimitar o espaço.
    - 3.Segmentação: Dentro do quadrado delimitado, a rede pinta pixel por pixel para encontrar o contorno exato.
- Para o YOLO fazer a máscara, ele obrigatoriamente precisa localizar o objeto primeiro. A Detecção é o "esqueleto" e a Segmentação é a "pele".

## Objetivo Validação:
- Verificar se o modelo aprendeu a generalizar ou se ele apenas decorou as imagens de treino (o que chamamos de Overfitting). Se a métrica no treino está ótima, mas na validação está péssima, modelo não serve para a vida real.
## Métricas de Performance
- As métricas são geradas após a etapa de Validação.
### Forma de análise por técnica:
- Na Detecção (.pt): olha o mAP50.
- Na Segmentação (-seg.pt): olha o Mask mAP
- Na Pose (-pose.pt): olha o OKS ou Pose mAP.
- Na Classificação (-cls.pt): olha o Top-1 e Top-5 Accuracy.
## Obs:
### A Matemática "Escondida"
- Toda a complexidade de Convoluções, Pooling, Backpropagation e funções de ativação está "encapsulada" dentro do código da Ultralytics. Ao dar o comando .train(), o YOLO ativa esse motor matemático.
- O Rótulo (Label): As imagens precisam estar rotuladas (anotadas) de acordo com a técnica.  O modelo não "adivinha" o que é segmentação sozinho. A técnica que foi escolhida no modelo (.pt vs -seg.pt) tem que dar "match" com o tipo de rótulo criado.
    - Para Detecção: Entrega para o modelo uma imagem e um arquivo de texto com 5 valores: classe x_centro y_centro largura altura. É a coordenada de um quadrado simples.
    - Para Segmentação: Entrega para o modelo a mesma imagem, mas o arquivo de texto contém dezenas de coordenadas: classe x1 y1 x2 y2 x3 y3... que formam o polígono (contorno exato).
    -  Para Pose: O arquivo de texto é mais denso. Ele combina a caixa da detecção com os pontos específicos (articulações): classe x y w h x1 y1 v1 x2 y2 v2.
- erro: Se carregar um modelo de segmentação (-seg.pt), mas entregar rótulos que só têm caixas (detecção), o modelo vai dar erro ou não vai aprender a segmentar, porque ele "esperava" polígonos e recebeu apenas quadrados.

# 24 e 25/02
## Notação de Imagens
### Softwares de Rastreamento (Sistemas Optoeletrônicos)
- São sensores de contraste que necessitam de pontos físicos (marcadores retroreflexivos ou ativos) no objeto. São ideais para ambientes controlados (laboratórios), mas limitados em campo.

### CVAT (Computer Vision Annotation Tool)
- Ferramenta de anotação de imagens com interface intuitiva, possibilitando trabalhar com anotações de keypoints (pontos-chave anatômicos) e também esqueletos. Permite exportar arquivos em vários formatos e utiliza IA genérica para interpolação (técnica matemática de preenchimento de dados entre dois pontos conhecidos) em vídeos através de tracks (rastreamento dinâmico baseado em fluxo óptico ou algoritmos de detecção).

### DeepLabCut (DLC)
- Framework especializado em aprendizado supervisionado (método de treinamento onde a IA aprende a partir de exemplos rotulados por um humano), baseado em Deep Learning (aprendizado profundo baseado em redes neurais artificiais complexas), que carrega diversas arquiteturas para treinar modelos.

# 04/03
## Camada 1 - Treinamento, validação e predição com DeepLabCut
- Entendendo o ciclo de vida do treinamento de uma rede neural (ResNet-50), a avaliação e a predição no restante do vídeo, com base em anotações manuais de 60 frames feitas na interface gráfica (Napari).

### Processo:
- Testando, estudando e analisando valores de épocas, cálculos e métricas, com valores de iterações diferentes.
- Entendendo métricas, possíveis erros e suas causas.

### Conceitos métricas
- **Train Loss:** - Erro dentro da imagem de treino. Quanto mais próximo de 0, melhor.
- **Valid Loss:** - Erro em uma pequena amostra de validação. Quanto mais próximo de 0, melhor.
- **Test RMSE:** - Distância média em pixels entre a anotação real e onde a rede acha que o ponto está.
- **RMSE (p-cutoff 0.1):** - Erro médio considerando apenas pontos onde a rede tem confiança superior a 0.1 (yaml). Se > 10px, a rede ainda pode precisar de mais treino ou mais dados para atingir o nível de um especialista.
- **mAP** - Acurácia média. Indica a porcentagem de acertos da rede com alta precisão.
- **maR** - Capacidade da rede de "encontrar" todos os pontos anotados.
### 2. Métricas de Validação (Generalização)
- **Train RMSE:** - O que o modelo decorou (erro nas imagens que foram usadas para ajustar os pesos).
- **Test RMSE:** - O que o modelo aprendeu (erro em imagens que a rede nunca viu, indicando a capacidade de generalização).

### Teste 1: Desenvolvimento de Modelo Próprio (Customizado)
* **O que é:** Treinamento via Transfer Learning (ResNet-50) no DeepLabCut com anotação manual de ~300 frames.
* **Objetivo:** Criar um modelo proprietário para automatizar a rotulagem do dataset da Iniciação Científica.
* **Observações Pessoais:** O modelo aprendeu bem posições estáticas, mas falha na continuidade (interpolação). Notei que a falta de "pontos vizinhos" confunde a rede, fazendo-a trocar as patas dianteiras pelas traseiras, pois ela não tem contexto anatômico para entender onde cada membro deveria estar.
* **Próximos Passos:** 1. **Refinar o Esqueleto:** Adicionar novos keypoints estratégicos (como tronco e articulações intermediárias) para criar uma conexão estrutural que sirva de guia lógico para a rede.
    2. **Aumentar Dataset de Oclusão:** Anotar especificamente frames onde há cruzamento de membros para ensinar a rede a diferenciar as identidades das patas.

# Registro de Experimentos - Estimativa de Pose Equina
# 17/03

### Teste 1: Desenvolvimento de Modelo Próprio (Customizado)
* **O que é:** Treinamento via Transfer Learning (ResNet-50) no DeepLabCut com anotação manual de ~300 frames.
* **Objetivo:** Criar um modelo próprio para automatizar a rotulagem do dataset da Iniciação Científica.
* **Observações Pessoais:** O modelo aprendeu bem posições estáticas, mas falha na continuidade (interpolação). Notei que a falta de "pontos vizinhos" confunde a rede, fazendo-a trocar as patas dianteiras pelas traseiras, pois ela não tem contexto anatômico para entender onde cada membro deveria estar.

### Teste 2: Modelo Pré-treinado (Automatizado)
* **O que é:** Implementação de um modelo de benchmark (teste de comparação) para o Teste 1, previamente treinado em datasets massivos e especializados em morfologia equina, para execução de rotulagem automática.
* **Objetivo:** Comparar o desempenho de uma rede robusta com os resultados obtidos no Teste 1.
* **Observações Pessoais:** O modelo apresentou um resultado visual muito mais elegante e estável. Percebi que ele utiliza muito mais pontos de anotação e exibe um retângulo (Bounding Box) de detecção de objeto, o que parece limitar a área de aprendizado e facilitar a organização dos pontos no corpo do cavalo.

## Próximos Passos:
Ao analisar os dois testes (1 e 2), os seguintes passos serão aplicados para alcançar o objetivo de desenvolver um modelo próprio para automatizar futuramente as anotações:

- **Refinar o Esqueleto:** Adicionar novos keypoints estratégicos (como tronco e articulações intermediárias) para criar uma conexão estrutural que sirva de guia lógico para a rede.

- **Aumentar Dataset de Oclusão:** Anotar mais imagens, especificamente frames onde há cruzamento de membros, para ensinar a rede a diferenciar as identidades das patas.
- **Integração de Detecção de Objeto:** Implementar uma camada de detecção (Bounding Box) para isolar o animal e definir uma Região de Interesse (ROI). Isso permitirá que a rede de pose foque exclusivamente na anatomia do cavalo, reduzindo o campo de visão e minimizando erros de interpolação causados por ruídos do cenário.