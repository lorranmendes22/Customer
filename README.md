### README

Este repositório contém um exemplo de aplicação de classificação binária para prever a rotatividade de clientes (churn) em uma empresa de telecomunicações, utilizando aprendizado supervisionado com Python e bibliotecas como Pandas e Scikit-Learn.

#### Descrição do Projeto

O código apresentado aqui carrega dados de um arquivo CSV que descreve diferentes variáveis relacionadas aos clientes de uma empresa de telecomunicações. O objetivo é prever se um cliente irá ou não cancelar seu serviço (churn) com base nessas variáveis.

#### Pré-requisitos

Para executar o código, é necessário ter instalado:
- Python 3
- Bibliotecas: pandas, scikit-learn

#### Instalação

1. Clone o repositório:
   ```
   git clone <URL_do_repositório>
   ```

2. Instale as dependências:
   ```
   pip install pandas scikit-learn
   ```

#### Como Utilizar

1. Importe as bibliotecas necessárias:
   ```python
   import pandas as pd
   from sklearn.svm import LinearSVC
   from sklearn.model_selection import train_test_split
   from sklearn.metrics import accuracy_score
   from sklearn.dummy import DummyClassifier
   ```

2. Carregue os dados do CSV localmente:
   ```python
   dados = pd.read_csv('Customer-Churn.csv')
   ```

3. Prepare os dados convertendo variáveis categóricas em numéricas:
   ```python
   a_trocar = {
       "Nao": 0, "Sim": 1,
       "SemServicoTelefonico": 1, "Mensalmente": 11, "UmAno": 12, "DoisAnos": 24,
       "ChequeDigital": 0, "ChequePapel": 1, "DebitoEmConta": 2, "CartaoDeCredito": 3,
       "DSL": 0, "FibraOptica": 1, "SemServicoDeInternet": 3
   }
   dados = dados.replace(a_trocar)
   ```

4. Separe os dados em variáveis de entrada (features) e saída (target):
   ```python
   x = dados.drop('Churn', axis=1)  # features - Churn
   y = dados["Churn"]  # classes
   ```

5. Divida os dados em conjuntos de treino e teste:
   ```python
   seed = 20  # pode ser qualquer valor fixo
   treino_x, teste_x, treino_y, teste_y = train_test_split(x, y, random_state=seed, test_size=0.25)
   print("Treinamento com %d elementos e testaremos com %d elementos" % (len(treino_x), len(teste_x)))
   ```

6. Crie um modelo de classificação (exemplo com LinearSVC):
   ```python
   modelo = LinearSVC()
   modelo.fit(treino_x, treino_y)
   ```

7. Avalie a acurácia do modelo:
   ```python
   previsoes = modelo.predict(teste_x)
   acuracia = accuracy_score(teste_y, previsoes) * 100
   acuracia_model_score = modelo.score(teste_x, teste_y) * 100
   print("A acurácia foi %.2f%%" % acuracia)
   print("A acurácia foi %.2f%%" % acuracia_model_score)
   ```

8. Compare com um baseline (Dummy Classifier):
   ```python
   dummy_stratified = DummyClassifier()
   dummy_stratified.fit(treino_x, treino_y)
   acuracia_dummy = dummy_stratified.score(teste_x, teste_y) * 100
   print("A acurácia do dummy stratified foi %.2f%%" % acuracia_dummy)
   ```

#### Resultados Esperados

Os resultados esperados incluem a acurácia do modelo treinado e a acurácia de um baseline para comparação. O modelo utiliza características dos clientes para prever se eles irão cancelar o serviço (churn).

#### Contribuições

Contribuições são bem-vindas! Caso queira melhorar este código, sinta-se à vontade para criar um fork do repositório e enviar um pull request com suas alterações.


#### Autores

Desenvolvido por Lorran Luciano Oliveira Mendes

