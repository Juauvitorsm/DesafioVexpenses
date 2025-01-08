

# Relatório de Análise de Dados e Previsão de Compras

## Objetivo
O objetivo deste projeto foi analisar os dados de compras de clientes e construir um modelo preditivo para classificar se um cliente realizará ou não uma compra, com base em variáveis como idade, renda anual, tempo no site, entre outras. Também foram realizadas análises estatísticas, segmentações para entender melhor o comportamento dos clientes e o treinamento do modelo de classificação. O projeto foi desenvolvido em 5 fases: 1. Realização de análise inicial dos dados:
1. Análise Estatística, 2. Pré-processamento dos Dados, 3. Construção do Modelo de Classificação, 4. Interpretação dos Resultados, 5.Extra.

## Análise Estatística

### Qualidade da Exploração dos Dados
A exploração dos dados foi feita com o objetivo de entender as distribuições e relações entre as variáveis e o comportamento de compra:
Objetivo: 
    Realização de análise inicial dos dados:
   - Verificação a distribuição das variáveis (idade, renda, tempo no site, etc.).
   - Identificação valores ausentes ou inconsistências nos dados.
   - Exploração possíveis relações entre as variáveis independentes e a variável alvo (Compra).

Verificação a distribuição das variáveis (idade, renda, tempo no site, etc.), Identificação valores ausentes ou inconsistências nos dados.:

Utilizei os seguintes códigos de visualização e limpeza no intuito de tratar meus dados, para começar a fazer análises

```python
print(data.info()) 
print(data.head())
print(data.isnull().sum())
data = data.dropna()
print(data.describe())
data.rename(columns={'Tempo no Site (min)': 'Tempo_Site','Idade': 'Idade','Renda Anual (em $)': 'Renda_Anual','Compra (0 ou 1)': 'Compra','Gênero': 'Genero','Anúncio Clicado': 'Anuncio_Clicado'}, inplace=True)
data['Compra'] = data['Compra'].astype(int)
data['Genero'] = data['Genero'].map({'Feminino': 1, 'Masculino': 2}) 
```
Exploração possíveis relações entre as variáveis independentes e a variável alvo (Compra).

Após organizar previamente meus dados comecei a relacionar a distribuição de variaveis com a variavel compra, afim ter noção estatística de cada variavel. Crie relações matemáticas e gráficas para facilitar a visualização, como:

```phyton

data_group= data.groupby(['Tempo_Site', 'Idade', 'Renda_Anual', 'Genero' ])["Compra"].mean()
data_group

```
E também com gráficos apresentados no arquivo desafio.ipynb que são: 
Mapa de calor (Visão geral), Distribuição de compra por gênero, Distribuição de compra por anúncio clicado, Média de tempo no site por compra e renda anual por compra.

Em seguida, realização de testes estatísticos. Afim de encontrar relações significativas, no qual encontrei valores que já começam sugerir qual modelo de classificação usar 

```phyton
#Teste para comparar "Tempo_Site" entre as duas classes de "Compra"
compra = data[data['Compra'] == 1]['Tempo_Site']
nao_compra = data[data['Compra'] == 0]['Tempo_Site']

t_stat, p_val = ttest_ind(compra, nao_compra)
print(f'Teste T para Tempo_Site: T-statistic = {t_stat}, P-value = {p_val}')

# Teste para comparar "Renda_Anual" entre as duas classes de "Compra"
compra_renda = data[data['Compra'] == 1]['Renda_Anual']
nao_compra_renda = data[data['Compra'] == 0]['Renda_Anual']

t_stat_renda, p_val_renda = ttest_ind(compra_renda, nao_compra_renda)
print(f'Teste T para Renda_Anual: T-statistic = {t_stat_renda}, P-value = {p_val_renda}')

```

### Pré-processamento dos Dados:

Realização do pré-processamento dos dados:

   - Normalizar ou padronizar variáveis numéricas, se necessário.
   - Realizar codificação para variáveis categóricas, transformando-as em valores numéricos.

     
Como já tinha padronizado as variáveis numéricas no tratamento inicial, restou padronizar e transformar as variáveis categóricas e transforma-las em numéricos, nesse passo fiz uma aplicação de MinMaxScaler e sklearn importando de LabelEncoder

```phyton
# Padronização
columns_to_scale = ['Idade', 'Renda_Anual', 'Genero', 'Tempo_Site']
scaler = MinMaxScaler()
data[columns_to_scale] = scaler.fit_transform(data[columns_to_scale])

# Categórica para numérica
categorical_columns = ['Genero', 'Anuncio_Clicado'] 
for col in categorical_columns:
    X[col] = encoder.fit_transform(X[col])

```
 - Dividir os dados em conjuntos de treino e teste.

```phyton

# Dividindo os dados em treino e teste (80% treino, 20% teste)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

```

## Construção do Modelo de Classificação

Realização da contrução do modelo de classificação:

○ Treinar um modelo simples de classificação (como Regressão Logística,
Árvore de Decisão, ou Random Forest).
○ Avaliar o modelo utilizando métricas apropriadas
Adicionar visualizações gráficas para complementar a análise.
Usar técnicas de validação cruzada para uma avaliação mais robusta.
Explorar o impacto de hiperparâmetros no desempenho do modelo.

### Implementação do Modelo
Foi implementado um modelo de **Random Forest** para prever a compra (variável binária: 0: Não Comprou, 1: Comprou). A escolha do Random Forest foi feita pela sua capacidade de lidar com dados complexos e desbalanceados, e a facilidade de interpretação dos resultados. Além disso, ele apresentou um bom equilíbrio entre performance e capacidade de generalização, mesmo em um cenário inicial desafiador, pois pelas análises estastísticas iniciais os dados pareciam desbalanceados, pois com o número de compradores aproximadamente 50% menor do que os de não compradores, o modelo com foco em recall, conseguiu recuperar (menos com desbalanceamento) o balanceamento, me entregando com boas métricas. Pois com o Random Forest consigo adequar para que eu consigo verificar melhor o comportamento de compradores.

#### Etapas de Implementação:
1. **Pré-processamento:** Exclusão de valores ausentes e transformação de variáveis categóricas em numéricas.
2. **Divisão de Dados:** Separação entre variáveis independentes (X) e dependentes (y), com divisão entre treino e teste.
3. **Treinamento e Predição:** Treinamento no conjunto de dados de treino e realização de previsões no conjunto de teste.
4. **Avaliação de Desempenho:** O modelo obteve uma acurácia de **66,67%**, com boa performance para a classe "Não Comprou", mas dificuldades em prever os compradores.
5. **Hiperparâmetros**: Utilizando o grid para verificar métricas afim de ajustar o modelo de classificação
6. **Balanceamento**: Utilização do SMOTE para balancear

### Interpretação Inicial do Modelo
O modelo base indicou que **tempo no site** e **idade** são as variáveis mais relevantes para a previsão de compras. Identificou-se um **desequilíbrio de classes**, o que impactou a previsão da classe "Comprou". Após inserir o primeiro modelo de classificação e observando a árvore preditiva do random forest, percebi que está o modelo estava encontrando desafios, seja por desbalanceamento ou por hiperparâmetros. Além de possuir uma matriz confusão que não agregava na análise dividi o projeto em testes até encontrar as métricas desejadas.

### Testes e Resultados

1. **Modelo Inicial:**
   - F1-Score: 0,24
   - Precisão: 0,40
   - Recall: 0,17
   - **Problema:** Desequilíbrio de classes e métricas inconsistentes, valor não favorável, arurácia enganosa: 0,67 devido ao balanceamente, pois a precisão acusava o mesmo valor e o f1 score mostrava um desequilibrio entre precisão (especificidade) e recall (sensibilidade)
   - No modelo inicial somente Random forest e pré-processamento.
 

2. **Modelo Ajustado (Hiperparâmetros):**
   - F1-Score: 0,38
   - Precisão: 0,44
   - Recall: 0,33
   - **Limitação:** Melhora limitada, mas sem capturar adequadamente os compradores, foram alterados valores de hiperparêmetros: n_estimators=50, random_state=42,max_depth=10, min_samples_split=2 , min_samples_leaf=4 , class_weight='None'


3. **Modelo com SMOTE (Balanceamento de Classes):**
   - F1-Score: 0,78
   - Precisão: 0,70
   - Recall: 0,88
   - **Resultado:** Melhor captura dos padrões de compradores.
   - Mesmo com os ajustes de hiperparâmetros a melhora foi insatisfatória, visto que o nosso objetivo maior é capturar padrão dos compradores.
Entretanto, com o SMOTE foi realizado o balanceamento de 0,8 de não compras, para compras. Com o balanceamento mais o hiperparâmetro(scoring= recall), as métricas se apresentaram mais equilibradas com têndencia forte para o recall mostrando que o modelo capturou bem os insights e "comportamentos" de compradores.

### Melhoria Proposta

## 1. Engenharia de Variáveis
- **Criação de Variáveis Derivadas:** Introduzir novas variáveis baseadas em interações entre as variáveis existentes. Por exemplo, criar uma variável que combine o tempo no site com a idade ou a renda anual com o tempo de navegação.

## 2. Aumento do Tamanho da Amostra
- **Coleta de Mais Dados:** Buscar aumentar a base de dados, garantindo uma melhor representação dos compradores, especialmente da classe minoritária. O aumento da amostra ajudaria a melhorar a performance do modelo, reduzindo os problemas de desbalanceamento.
- **Estratégias de Amostragem:** Além do SMOTE, outras técnicas de amostragem, como o undersampling da classe majoritária, podem ser aplicadas para melhorar o equilíbrio entre as classes.

## 3. Melhoria do Modelo
- **Uso de Modelos Mais Complexos:** Avaliar a aplicação de modelos mais avançados, como Gradient Boosting, que pode oferecer um desempenho superior em cenários de desbalanceamento de classes.
- **Ajuste de Hiperparâmetros Avançado:** Implementar técnicas como busca em grade ou otimização bayesiana para encontrar a melhor combinação de hiperparâmetros, com mais precisão, de forma a aumentar a performance do modelo.

## 4. Avaliação de Métricas Diversificadas
- **Aprofundar a Análise de Métricas:** Ampliar a análise das métricas além de precisão e recall, considerando a curva ROC, AUC, e a matriz de confusão. Essas métricas podem fornecer insights mais detalhados sobre o desempenho do modelo.

## 5. Testes com Variáveis Externas
- **Incluir Dados Externos:** Integrar dados externos, como tendências de mercado, sazonalidade ou dados econômicos, que possam influenciar o comportamento de compra e melhorar as previsões.



- ## Conclusões Finais


O modelo preditivo desenvolvido para classificar a compra de clientes foi uma experiência interessante, mas apresentou desafios importantes, especialmente relacionados ao desbalanceamento das classes.

Após realizar a análise estatística e pré-processamento dos dados, foi possível observar que variáveis como **tempo no site** e **idade** se mostraram relevantes para a previsão de compras, mas o modelo enfrentou dificuldades para classificar corretamente os clientes compradores, especialmente devido ao desbalanceamento das classes.

Os modelos iniciais, como o Random Forest, mostraram boa acurácia geral, mas dificuldades em capturar a classe "Comprou" de forma eficiente. A aplicação de técnicas de balanceamento, como o **SMOTE**, ajudou a melhorar o desempenho do modelo. A alteração dos hiperparâmetros também resultou em pequenas melhorias nas métricas.

A partir dos testes realizados, é possível concluir que a **melhoria do balanceamento de classes** foi fundamental para melhorar o **recall**, que é uma métrica importante quando se quer capturar compradores. O **f1-Score** e a **precisão** também apresentaram melhorias, mas o foco deve ser em capturar os compradores, pois o objetivo principal é melhorar a compra.

Portanto, as melhorias propostas incluem:
- **Engenharia de Variáveis**: A criação de novas variáveis pode melhorar as previsões, fornecendo mais informações ao modelo.
- **Aumento do Tamanho da Amostra**: A coleta de mais dados pode tornar a análise mais robusta e ajudar a melhorar a performance do modelo.
- **Ajustes Futuros no Modelo**: É importante continuar ajustando os hiperparâmetros e explorar novas técnicas para balanceamento de classes, a fim de evitar overfitting e melhorar o equilíbrio entre as métricas.

A análise do comportamento dos clientes e a previsão de compras são cruciais para a otimização de estratégias de marketing e vendas, e com as melhorias propostas, espera-se obter um modelo mais robusto e preciso, capaz de identificar os clientes com maior chance de realizar compras.






