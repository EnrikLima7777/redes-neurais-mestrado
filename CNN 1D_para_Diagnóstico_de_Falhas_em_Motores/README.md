# redes-neurais-mestrado

a) IMPLEMENTAÇÃO DAS REDES NEURAIS;

A implementação da rede neural no projeto é baseada em uma CNN 1D (rede neural convolucional unidimensional), utilizada para a classificação de motores elétricos em duas categorias: saudáveis e com falha.

1. Estrutura do Código
   
A implementação segue os seguintes passos:

a. Importação de bibliotecas necessárias, como tensorflow.keras para criar o modelo, pandas e numpy para manipulação dos dados.

b. Carregamento dos dados: Os dados são armazenados em arquivos CSV contendo leituras de corrente elétrica (Current-A, Current-B e Current-C). Eles são organizados e rotulados (0 para motores saudáveis, 1 para motores com falha).

c. Divisão dos dados: O conjunto de dados é dividido em 70% para treino e 30% para teste, garantindo um balanceamento na amostragem.

d. Pré-processamento: Os dados são remodelados para o formato adequado à CNN 1D.

2. Estrutura da Rede Neural

A rede neural possui a seguinte arquitetura:
a. Camada de entrada: Input(shape=(3,1)), onde os três valores de corrente são usados como entrada.
b. Camada convolucional 1D (Conv1D): Utiliza 32 filtros, um kernel de tamanho 2 e ativação ReLU, com regularização L2(0.001).
c. Camada Dropout (0.5): Reduz overfitting.
d. Camada Flatten: Transforma os dados da convolução em uma única dimensão.
e. Camada densa (Dense): 64 neurônios, ativação ReLU, regularização L2(0.01).
f. Outra camada Dropout (0.3): Para reduzir overfitting.
g. Camada de saída (Dense): 1 neurônio com ativação sigmoid, que gera a classificação final (saudável ou com falha).

3. Treinamento do Modelo  
O modelo é treinado usando EarlyStopping para evitar overfitting. Ele monitora a perda da validação e interrompe o treinamento caso não haja melhorias após 10 épocas. O treinamento é feito por 50 épocas, com um batch size de 32.
