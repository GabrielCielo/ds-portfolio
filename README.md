O Projeto em questão tem como objetivo primário integrar o meu portfólio e servir como um indicador das minhas habilidades para eventualmente ocupar uma posição de Cientista de Dados Jr.
Tendo isso em mente, é importante ressaltar que o modelo final possui bastante espaço para melhoria, bem como todos os componentes do projeto como a Análise Exploratória de Dados, o Feature Engineering e a criação do Pipeline para o pré-processamento.

O problema consiste em encontrar um modelo que seja capaz de prever os preços de casas na região de King County em Washington a partir dos atributos presentes no dataset. Para tal, foi usado um método de aprendizado supervisionado por regressão com aprendizado por batch. A principal métrica de avaliação usada foi o Root Mean Squared Error (RMSE), embora o R2 Score também tenha sido levado em consideração.

Sobre o Dataset:
- Possui 21 colunas (variáveis) e 21613 linhas (instâncias);
- Não possui valores nulos e todas as variáveis são numéricas;
- 2 variáveis são irrelevantes para o modelo final (id e data);
- 4 variáveis são numérico-categóricas e representam uma nota subjetiva dada pelo avaliador do imóvel (waterfront, view, condition e grade);
- As demais variáveis possuem valores contínuos, sendo uma considerável parcela referente às áreas do imóvel e sua localização geográfica.
- Temos uma presença robusta de outliers no conjunto, porém a decisão final foi mantê-los, visto que eles não parecem ser provenientes de erro humano e são em sua grande maioria valores críveis.

O Dataset foi inicialmente dividido em um conjunto de treino com 80% das instâncias (17290 linhas) e um conjunto de teste com 4323 linhas. Para manter proporções similares entre o conjunto de teste e de treino, assumiu-se que o atributo "sqft_living" fosse um dos principais na hora de definir o preço da casa e com base nisso foi feita uma divisão estratificada entre os dois conjuntos. De fato ficou comprovado que a feature utilizada era bastante influente no resultado final do preço através da observação das correlações lineares entre variáveis.

Na etapa de Feature Engineering, foi testado a criação de 3 novas variáveis a partir das que já eram conhecidas:

graded_area = combinação de sqft_living com grade, as duas variáveis que tiveram maior índice de correlação. OBS: Grade é uma variável numérica que representa uma nota subjetiva (de 1 a 13) referente a construção e design do imóvel. Quanto maior o valor, maior a qualidade do imóvel.

lot_pctg_built = percentual do terreno construído. obs: pode ser maior do que 1 se o imóvel tiver mais de um andar.

yrs_since_last_renov = tempo passado desde a última reforma (ou idade do imóvel se nunca foi reformado).

As variáveis graded_area e yrs_since_last_renov se mostraram relevantes para as predições finais, já a lot_pctg_built não pareceu ser uma variável muito relevante para o modelo.

Durante a etapa de criação do modelo de Machina Learning foi criado um Pipeline bastante simples, cuja função única era fazer o escalonamento do dataset. Devido a grande quantidade de outliers foi escolhido o StandardScaler ao invés do MinMaxScaler.

Os modelos criados utilizavam os seguintes algoritmos: Regressão Linear, Decision Trees Regressor, Support Vector Regressor, Random Forest Regressor e Gradient Boosting Regressor.

Foi observado que a maioria dos modelos sofria de sobreajuste, porém o modelo de Gradient Boosting pareceu se ajustar bem aos dados, tendo bons resultados de modo geral. Utilizando este último modelo com o ajuste dos hiperparâmetros foi possível encontrar um R2-Score de 0.8986 e um RMSE de 124038. Os resultados para os demais modelos estão todos presentes no NoteBook do Projeto para servirem de referência.
