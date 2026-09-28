# Máquina de Hits
![Status do Projeto](https://img.shields.io/badge/status-concluido-brightgreen?style=for-the-badge)
![Google Colab](https://img.shields.io/badge/google_colab-F9AB00?style=for-the-badge&logo=google-colab&logoColor=white)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)

Este repositório contém o projeto de análise preditiva e aprendizado de máquina focado na identificação de potenciais hits musicais no gênero Pop dentro do catálogo da API do Spotify. O objetivo central é fornecer uma ferramenta orientada a dados para auxílio em decisões estratégicas de gravadoras e produtores, reduzindo riscos de investimento em marketing e otimizando a seleção de faixas com elevado apelo comercial.

# Visão Geral
No mercado fonográfico, a promoção de um single exige alocação massiva de recursos financeiros em campanhas digitais, produção audiovisual e distribuição. O projeto aborda essa tomada de decisão como um problema de classificação binária da variável **is_hit**:

Classe 1 (Hit): Músicas com pontuação de popularidade $> 70 na API do Spotify.

Classe 0 (Não-Hit): Músicas com pontuação de popularidade < 70.

### A avaliação dos modelos prioriza o F1-Score e o Recall para equilibrar os custos operacionais do negócio:
Falso Positivo ($FP$): Prever um hit que fracassa (desperdício direto de orçamento de marketing).

Falso Negativo ($FN$): Prever um não-hit em uma música promissora (custo de oportunidade por falta de investimento).

# Diagnóstico de Dados
A base de dados foi construída a partir do conjunto Spotify Tracks Dataset, passando por um pipeline de filtragem e higienização estruturada:
### Escopo: 
874 faixas consolidadas e únicas pertencentes ao gênero Pop.
### Atributos: 
15 variáveis no total (14 atributos explicativos de áudio e 1 variável alvo binária is_hit).
### Valores Ausentes (NaN): 
0% de omissão na base final limpa.
### Desbalanceamento de Classes: Moderado 
Classe 0 (Não-Hit): 592 amostras (67,73%)

Classe 1 (Hit): 282 amostras (32,27%)
### Outliers: 
Manutenção consciente dos valores extremos por representarem características sonoras reais do mercado musical. A distorção no cálculo de distâncias foi eliminada pela aplicação do **StandardScaler**

# Metodologia e Pipeline de Machine Learning
1. Pré-Processamento:
   - Descarte de metadados de texto
   - Padronização das variáveis contínuas via **StandardScaler** ($\mu = 0, \sigma = 1$).
   - Amostragem estratificada na divisão entre Treino e Teste para preservar a proporção de 32,3% de hits.
2. Algoritmos Avaliados:
   - Regressão Logística: Modelo paramétrico e interpretável, utilizado como baseline.
   - K-Nearest Neighbors (KNN): Modelo não-paramétrico e não-linear, adequado para identificar agrupações locais no espaço de atributos.
3. Otimização de Hiperparâmetros:
   - Seleção via GridSearchCV com validação cruzada 5-Fold otimizando o **F1-Score**.
  
# Como Executar no Google Colab
1. Acesse o [Google Colab](https://colab.research.google.com/)
2. Importar o Repositório
- Clique em: Fazer Upload de Notebook
- Selecione a opção **Github** e cole o link desse repositório no campo de busca: https://github.com/oeduardohaag/maquina-de-hits
3. Faça o download do dataset **spotify-tracks-dataset.csv** presente nesse repositório para fazer a filtragem e higienização com o arquivo
4. Faça o upload do dataset na parte de **Arquivos** do notebook
