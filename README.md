1. Configuração Inicial
  O código inicia com a instalação das bibliotecas essenciais: scikit-learn, pandas, numpy, matplotlib, tensorflow e shap. A verificação da GPU é realizada para otimizar o treinamento do modelo.

3. Carregamento e Pré-processamento dos Dados
 
Parâmetros de Configuração:

•	WINDOW_SIZE: 60 amostras (equivalente a 1 segundo de dados).

•	STEP_SIZE: 30 amostras (50% de sobreposição entre janelas).

Função de Janelamento

A função create_sequences é responsável por criar sequências temporais a partir dos dados. Ela verifica a consistência temporal e ignora janelas com gaps maiores que 100ms.

5. Leitura dos Dados
6. 
Os dados são carregados de arquivos CSV representando dados saudáveis (healthy.csv) e dados com falha (0.7inner-200watt.csv).
Padronização dos Nomes das Colunas

Uma função clean_column_name é utilizada para remover espaços, hífens e padronizar a nomenclatura. Além disso, a coluna de timestamp é renomeada para timestamp.

Rotulagem dos Dados

•	healthy['label'] = 0

•	faulty['label'] = 1

8. Engenharia de Features
 
A função calculate_phase_features calcula estatísticas adicionais, como:

•	current_avg: Média das correntes das fases A, B e C.

•	imbalance: Desvio padrão das fases.

•	max_phase e min_phase: Máximos e mínimos das fases.

•	thd: Distorção harmônica total.

10. Criação das Janelas Temporais
 
A função create_sequences gera janelas deslizantes de dados temporais, considerando oito características extraídas de cada amostra.

12. Definição do Modelo
 
Arquitetura do Modelo:

•	Camada convolucional Conv1D para extração de características.

•	Camada Bidirectional LSTM para captura de padrões temporais.

•	Camadas de combinação Concatenate.

•	Camada final densa Dense com ativação sigmoide para classificação binária.

O modelo é compilado com o otimizador Adam e a função de perda binary_crossentropy.

14. Divisão dos Dados
 
Os dados são divididos temporalmente em 80% para treinamento e 20% para teste.

16. Treinamento do Modelo

O treinamento ocorre com callbacks para early stopping e salvamento do melhor modelo com base na métrica AUC.
17. Avaliação do Modelo

O modelo salvo é carregado e avaliado em diferentes conjuntos de dados de teste (de healthy.csv a 1.7inner-200watt.csv). Anomalias são detectadas com base em um limiar de 0.5.
