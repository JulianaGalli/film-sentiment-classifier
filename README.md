# Film Sentiment Classifier: Explorando do TF-IDF ao BERT

- Este projeto foi desenvolvido para a comunidade Film Junky Union, com o objetivo de automatizar a classificação de sentimentos em resenhas de filmes clássicos.
- O desafio central foi superar a meta de 0.85 no F1-score, garantindo robustez e capacidade de generalização.

# Visão Geral do Projeto
- O pipeline percorre a evolução das técnicas de NLP, partindo de modelos estatísticos simples (Bag of Words) até o estado da arte com Transformers, comparando como cada abordagem lida com a subjetividade da linguagem humana para classificação das resenhas em positivas ou negativas.

# Tecnologias Utilizadas
- Linguagem: Python
- Processamento de Texto: NLTK, spaCy (Lematização)
- Vetorização: TF-IDF, BERT Embeddings (bert-base-uncased)
- Modelagem: Regressão Logística, Regressão Linear, LightGBM
- Métricas: F1-Score, ROC AUC, APS (Average Precision Score)

# Resultados

A tabela abaixo consolida a performance de todos os modelos testados durante o projeto.

| ID | Modelo | Pré-processamento | F1-Score (Teste) | ROC AUC (Teste) | Tempo de Inferência |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | **Dummy Classifier** | N/A (Constante) | 0.67 | 0.50 | 0.0047s |
| 1 | **Regressão Linear** | NLTK + TF-IDF | 0.75 | 0.81 | 0.0106s |
| 2 | **Regressão Logística** | **NLTK + TF-IDF** | **0.88** | **0.95** | **0.0011s** |
| 3 | **Regressão Logística** | spaCy + TF-IDF | 0.88 | 0.95 | 288.60s |
| 4 | **LightGBM** | spaCy + TF-IDF | 0.86 | 0.93 | 288.96s |
| 5 | **BERT** | **Embeddings** | **0.87** | **0.93** | **1.8071s** |

# Insights e Conclusões Analíticas

**1. O Equilíbrio entre Métrica e Velocidade** 
- O Modelo 2 (TF-IDF + Logística) apresentou o maior F1-score bruto (0.88) com uma latência quase nula (0.0011s). É a solução ideal para sistemas que exigem baixo custo computacional e alta velocidade de resposta.

**2. A Superioridade Semântica do BERT**
- Apesar do F1 ligeiramente inferior em amostras pequenas, o Modelo 5 (BERT) demonstrou uma capacidade superior de Generalização Contextual.
- Exemplo Real: Em frases com estruturas negativas que escondem um elogio final (ex: "I did not expect... so good"), o BERT captou a nuance positiva, enquanto modelos baseados em palavras isoladas (TF-IDF) falharam.
- Polarização: O BERT apresentou decisões mais nítidas e confiantes (probabilidades próximas de 0 ou 1).

**3. Falha da Regressão Linear**
- O experimento com Regressão Linear serviu para validar que problemas de classificação binária em textos de alta dimensionalidade sofrem com a falta de regularização, resultando em predições instáveis fora do intervalo $[0, 1]$.

# Como Executar o Projeto

**Clone o repositório:**
- Bash
- git clone https://github.com/JulianaGalli/film-sentiment-classifier.git

**Instale as dependências:**
- Bash
- pip install -r requirements.txt

# Conclusão
- O projeto demonstra que a escolha do modelo ideal depende do equilíbrio entre precisão semântica e custo operacional.
- Para a Film Junky Union, o modelo recomendado para o ambiente de produção é o **Modelo 5 (BERT + Regressão Logística)**.
- Diferente das abordagens de "saco de palavras" (TF-IDF), o BERT compreende a ordem e o contexto das palavras, sendo capaz de identificar sarcasmo, ironia e estruturas linguísticas complexas que os modelos lineares ignoram. Apesar de demandar mais processamento, sua capacidade de generalização para resenhas de filmes inéditos e a segurança de suas predições garantem uma filtragem de sentimentos muito mais confiável e humana, mitigando o risco de falsos positivos em dados críticos do cliente.

# Autora
- Projeto desenvolvido por Juliana Galli, Cientista de Dados em formação, entusiasta de NLP e Deep Learning.
