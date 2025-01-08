Relatório de Análise de Dados e Previsão de Compras
Objetivo
O objetivo deste projeto foi analisar os dados relacionados a compras de clientes e, a partir dessa análise, construir um modelo preditivo para classificar se um cliente irá ou não realizar uma compra, com base em características como idade, renda anual, tempo no site, e outras variáveis. Além disso, foi realizada uma análise estatística e a segmentação dos clientes, para entender melhor os padrões de comportamento.

1. Análise Estatística: Qualidade da Exploração dos Dados
A exploração dos dados foi feita de maneira cuidadosa e detalhada, com o objetivo de entender a distribuição das variáveis e como elas se relacionam com o comportamento de compra dos clientes. Algumas das análises realizadas incluem:

Distribuição de Compras por Gênero: Foi feito um gráfico de barras para verificar a quantidade de compras realizadas por cada gênero. Isso ajudou a entender se há diferenças no comportamento de compra entre homens e mulheres.

Análise de Tempo no Site e Renda Anual: Utilizando gráficos de dispersão, observamos se existiam relações claras entre essas variáveis e a compra. Isso ajudou a identificar padrões de clientes que, por exemplo, gastam mais tempo no site ou têm maior renda anual.

Relação entre Idade e Renda Anual: A visualização dessas duas variáveis ajudou a segmentar o público-alvo para o modelo de previsão.

Testes Estatísticos (ANOVA): Realizou-se uma análise de variância (ANOVA) para testar se há diferenças significativas entre as médias de compras para os gêneros masculino e feminino. O p-valor obtido indicou que o gênero pode influenciar a decisão de compra, mas não foi possível concluir que há uma diferença estatisticamente significativa.

Essas etapas de exploração ajudaram a entender melhor os dados e a planejar a modelagem.

2. Modelo: Implementação Correta de um Modelo Básico de Classificação
Foi implementado um modelo de Random Forest para prever a variável alvo (Compra), que é binária (0: Não Comprou, 1: Comprou). A escolha do modelo Random Forest foi baseada na sua robustez e eficácia para tarefas de classificação, especialmente quando temos um número razoável de variáveis e queremos lidar com dados de forma eficiente. Além disso é 

A implementação do modelo envolveu as seguintes etapas:

Pré-processamento: Os dados foram preparados, com a exclusão de valores ausentes e a transformação de variáveis categóricas em numéricas, quando necessário.

Divisão de Dados: O dataset foi dividido em variáveis independentes (X) e dependentes (y), e a divisão entre dados de treino e teste foi feita para avaliar o modelo.

Treinamento e Predição: O modelo foi treinado com o conjunto de dados de treino, e em seguida, fez-se as previsões sobre o conjunto de dados de teste.

Avaliação de Desempenho: A acurácia do modelo foi de 66,67%, com valores de precision e recall variando conforme a classe. Isso indica que o modelo teve um bom desempenho para prever a classe "Não Comprou", mas apresentou dificuldades para prever os casos de clientes que realizaram compras.

A interpretação dos resultados foi feita de maneira objetiva e clara:

A acurácia do modelo foi usada como um dos principais indicadores de desempenho, mas também foram analisados precision, recall e f1-score, principalmente para a classe 1 (Comprou), para avaliar o quão bem o modelo consegue identificar os compradores.

Uso de hyperparâmetros para testes de métricas no random, afim de chegar relações melhores

Balanceamento

Validação cruzada para melhoria de resultados

Resultados da ANOVA: O teste de ANOVA forneceu uma visão interessante sobre a diferença de compras entre os gêneros, embora a significância estatística não tenha sido forte. Isso indicou que, embora o gênero tenha alguma influência, outros fatores podem ser mais determinantes para a decisão de compra.

A segmentação de usuários através do algoritmo KMeans ajudou a identificar diferentes perfis de clientes, e isso poderia ser útil para campanhas de marketing mais direcionadas ou para entender os diferentes comportamentos de compra.

4. Extras: Implementações Adicionais ou Insights Inovadores
Além da modelagem e análise básica, algumas implementações adicionais foram feitas:


Visualizações de Dados: Diversos gráficos foram gerados para visualizar os dados de forma mais intuitiva, como gráficos de dispersão, boxplots, e gráficos de barras. As visualizações foram ajustadas para facilitar a leitura e a interpretação.

Análise de Outliers: Uma análise de outliers nas variáveis contínuas poderia ser realizada para entender se há clientes cujos comportamentos são extremados e impactam o modelo de maneira negativa.

Conclusões Finais
 Interpretação Inicial
Modelo Base (Random Forest): Identificou que o tempo no site e a idade são as variáveis mais relevantes.
Problema Identificado: Desequilíbrio de classes, levando a baixo desempenho na previsão de compras (classe 1).
2. Testes e Resultados
Teste 1 (Modelo Inicial):

Desempenho Fraco para Classe 1 (Compra):
f1-score: 0,24
Precisão: 0,40
Recall: 0,17
Problema: Desequilíbrio severo nas classes e métricas inconsistentes.
Teste 2 (Hiperparâmetros Ajustados):

Ajustes:
n_estimators=50, max_depth=10, min_samples_split=2, min_samples_leaf=4, class_weight='None'.
Melhoras Moderadas:
f1-score: 0,38
Precisão: 0,44
Recall: 0,33
Limitação: Melhora limitada, não atingindo o objetivo de capturar compradores.
Teste 3 (Balanceamento com SMOTE):

Estratégia Utilizada:
Balanceamento (SMOTE) com proporção de 0,8 entre não compras e compras.
Ajustes adicionais no hiperparâmetro de scoring para recall.
Melhoria Significativa nas Métricas:
f1-score: 0,78
Precisão: 0,70
Recall: 0,88
Resultado: Modelo ajustado para captar melhor os padrões de compradores.
3. Melhoria Proposta
Engenharia de Variáveis:

Criar novas variáveis que possam aprimorar as previsões.
Aumento do Tamanho da Amostra:

Coletar mais dados para análises robustas.
Ajustes Futuros no Modelo:

Evitar overfitting mantendo o recall alto e equilibrado com outras métricas.

Como Executar
Clone o repositório:
bash
Copiar código
git clone 
Instale as dependências:
bash
Copiar código
pip install -r requirements.txt
Execute o código:
bash
Copiar código
Tecnologias Utilizadas:
Python
Pandas para manipulação de dados
Matplotlib e Seaborn para visualizações
Scikit-learn para construção e avaliação do modelo de Machine Learning

