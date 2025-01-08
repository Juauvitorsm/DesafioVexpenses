## Relatório de Análise de Dados e Previsão de Compras

# Relatório de Análise de Dados e Previsão de Compras

## Objetivo
O objetivo deste projeto foi analisar os dados de compras de clientes e construir um modelo preditivo para classificar se um cliente realizará ou não uma compra, com base em variáveis como idade, renda anual, tempo no site, entre outras. Também foram realizadas análises estatísticas e segmentações para entender melhor o comportamento dos clientes.

## Análise Estatística

### Qualidade da Exploração dos Dados
A exploração dos dados foi feita com o objetivo de entender as distribuições e relações entre as variáveis e o comportamento de compra:

- **Distribuição de Compras por Gênero:** Através de um gráfico de barras, foi analisada a quantidade de compras por gênero para verificar possíveis diferenças de comportamento entre homens e mulheres.
- **Análise de Tempo no Site e Renda Anual:** Gráficos de dispersão ajudaram a identificar padrões entre essas variáveis e o comportamento de compra.
- **Relação entre Idade e Renda Anual:** Visualizações dessas variáveis foram usadas para segmentar o público-alvo.

### Testes Estatísticos (ANOVA)
Foi realizada uma análise de variância (ANOVA) para verificar se o gênero influencia a decisão de compra. O p-valor indicou uma leve influência, mas não significância estatística.

## Modelo de Previsão

### Implementação do Modelo
Foi implementado um modelo de **Random Forest** para prever a compra (variável binária: 0: Não Comprou, 1: Comprou). O Random Forest foi escolhido pela sua eficácia em tarefas de classificação.

#### Etapas de Implementação:
1. **Pré-processamento:** Exclusão de valores ausentes e transformação de variáveis categóricas em numéricas.
2. **Divisão de Dados:** Separação entre variáveis independentes (X) e dependentes (y), com divisão entre treino e teste.
3. **Treinamento e Predição:** Treinamento no conjunto de dados de treino e realização de previsões no conjunto de teste.
4. **Avaliação de Desempenho:** O modelo obteve uma acurácia de **66,67%**, com boa performance para a classe "Não Comprou", mas dificuldades em prever os compradores.

#### Resultados da ANOVA
Embora o gênero tenha mostrado certa influência na compra, a análise revelou que outros fatores são mais determinantes.

### Segmentação de Clientes
Utilizando o algoritmo **KMeans**, foram identificados diferentes perfis de clientes, úteis para campanhas de marketing direcionadas.

## Implementações Adicionais
Além da modelagem, foram realizadas as seguintes implementações:

- **Visualizações de Dados:** Diversos gráficos, como de dispersão e boxplots, foram gerados para facilitar a leitura e interpretação.
- **Análise de Outliers:** A análise de outliers ajudou a identificar comportamentos extremos que podem impactar negativamente o modelo.

## Conclusões Finais

### Interpretação Inicial do Modelo
O modelo base indicou que **tempo no site** e **idade** são as variáveis mais relevantes para a previsão de compras. Identificou-se um **desequilíbrio de classes**, o que impactou a previsão da classe "Comprou".

### Testes e Resultados

1. **Modelo Inicial:**
   - F1-Score: 0,24
   - Precisão: 0,40
   - Recall: 0,17
   - **Problema:** Desequilíbrio de classes e métricas inconsistentes.

2. **Modelo Ajustado (Hiperparâmetros):**
   - F1-Score: 0,38
   - Precisão: 0,44
   - Recall: 0,33
   - **Limitação:** Melhora limitada, mas sem capturar adequadamente os compradores.

3. **Modelo com SMOTE (Balanceamento de Classes):**
   - F1-Score: 0,78
   - Precisão: 0,70
   - Recall: 0,88
   - **Resultado:** Melhor captura dos padrões de compradores.

### Melhoria Proposta
- **Engenharia de Variáveis:** Criar novas variáveis para melhorar as previsões.
- **Aumento do Tamanho da Amostra:** Coletar mais dados para uma análise mais robusta.
- **Ajustes Futuros no Modelo:** Evitar overfitting, mantendo um bom equilíbrio entre recall e outras métricas.




