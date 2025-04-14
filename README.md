# 🛒 Analisando Big Mart Sales


## ✨ Sobre o Projeto
Este projeto tem como objetivo explorar o conjunto de dados das vendas da Big Mart, analisando fatores importantes que impactam nos resultados de vendas. 🔍  

---
## Objetivo
Identificar padrões e fornecer insights estratégicos. 📊

## Ferramentas Utilizadas
Python, Pandas, Matplotlib, Seaborn 🐍

## Resultados
Documentação detalhada e preparação para modelagem futura. 🚀
---

## 💡 Motivação
Ao trabalhar com o conjunto de dados da Big Mart, a motivação foi:
1. Aprender a tratar e explorar dados, com foco em limpeza e visualizações.
2. Identificar os principais fatores que impactam nas vendas, tanto numéricos (como preços) quanto categóricos (como tipo de outlet e localização).
3. Criar insights claros e bem documentados, com base em análises exploratórias.
4. Usar visualizações para destacar padrões importantes e preparar os dados para possíveis modelos futuros.

---

## 🗺️ Etapas do Projeto
Abaixo, detalho as etapas realizadas no projeto:

### 1. Importação de Bibliotecas
### 🖥️ Configuração Inicial

import pandas as pd

import matplotlib.pyplot as plt

import seaborn as sns



## 2. Carregamento do Conjunto de Dados
Carregando e estruturando os dados em um DataFrame:

D_big = pd.read_csv(r'C:\Users\frann\Documents\Projeto_Big_mart\Train-Set.csv')

## 3. Entendimento Inicial do Conjunto de Dados
Foram feitas verificações para entender as características do DataFrame:

## Verificando os tipos de dados
print(D_big.dtypes)
![Dtypes](https://github.com/user-attachments/assets/c10ba250-cd31-4ea5-b769-b86c8d537ddf)


## Identificando valores ausentes
print(D_big.isnull().sum())
![Image](https://github.com/user-attachments/assets/edc1c546-96e1-4fff-ac79-7ed05f444bea)

## 4. Tratamento de Valores Ausentes
Os valores ausentes foram tratados para garantir a consistência dos dados:

Substituí os valores ausentes na coluna Weight pela média.

Substituí os valores ausentes na coluna OutletSize pela moda.


## Tratamento da coluna 'Weight' (numérica)
weight = D_big['Weight'].mean()

D_big['Weight'] = D_big['Weight'].fillna(weight)

## Tratamento da coluna 'OutletSize' (categórica)
mode_outlet_size = D_big['OutletSize'].mode()[0]

D_big['OutletSize'] = D_big['OutletSize'].fillna(mode_outlet_size)


## 5. Análises Explorando Padrões
5.1. Distribuição de Dados
Verifiquei a distribuição da coluna Weight para entender como os valores estão distribuídos após a substituição pela média:

sns.histplot(D_big['Weight'], kde=True)

plt.title('Distribuição do Peso Após Correção')

plt.xlabel('Peso')

plt.ylabel('Frequência')

plt.show()

![Distribuição do Peso Após Correção](https://github.com/user-attachments/assets/115b5d82-c9a7-4d23-abed-f05c7e1c2848)



## 5.2. Correlações Numéricas
Criei uma matriz de correlação para entender as relações entre as variáveis numéricas, com um destaque para MRP e OutletSales:

numeros = D_big.select_dtypes(include=['float64', 'int64'])

matriz_de_correlação = numeros.corr()

## Heatmap da correlação

sns.heatmap(matriz_de_correlação, annot=True, cmap="coolwarm")

plt.title('Mapa de Calor da Correlação entre Variáveis')

plt.show()

![Mapa de Calor da Correlação entre Variáveis](https://github.com/user-attachments/assets/d3a75169-c2ab-4ee2-914c-773a48ae218c)

## 5.3. Relações Categóricas
Explorei como variáveis categóricas, como OutletType e LocationType, afetam OutletSales:

sns.boxplot(x=D_big['OutletType'], y=D_big['OutletSales'])

plt.title('Impacto do Tipo de Outlet nas Vendas')

plt.xlabel('Tipo de Outlet')

plt.ylabel('Vendas')

plt.show()

![Impacto do Tipo de Outlet nas Vendas](https://github.com/user-attachments/assets/35e1e216-8d8b-4d33-887a-18252254d6e6)



Explorei como variáveis categóricas, como LocationType e OutletSales:

sns.boxplot(x=D_big['LocationType'], y=D_big['OutletSales'])

plt.title('Impacto da Localização do Outlet nas Vendas')

plt.xlabel('Localização do Outlet')

plt.ylabel('Vendas')

plt.show()

![Impacto da Localização do Outlet nas Vendas](https://github.com/user-attachments/assets/29c016c5-0714-4a22-8e9f-980e8eaf6bee)

## 5.4. Análise Temporal
Verifiquei como o ano de estabelecimento (EstablishmentYear) dos outlets impacta nas vendas:

sns.lineplot(x=D_big['EstablishmentYear'], y=D_big['OutletSales'])

plt.title('Ano de Estabelecimento vs. Vendas')

plt.xlabel('Ano de Estabelecimento')

plt.ylabel('Vendas')

plt.show()

![Ano de Estabelecimento vs. Vendas](https://github.com/user-attachments/assets/3579fca7-6aa6-47fc-b554-afd1deaf2ccb)

## 5.5. Outliers
Identifiquei potenciais outliers nas variáveis numéricas:


sns.boxplot(x=D_big['MRP'])
plt.title('Boxplot do Preço Máximo de Varejo')

plt.show()

![Boxplot do Preço Máximo de Varejo](https://github.com/user-attachments/assets/10bfbb45-49b8-4e9b-be81-ca97c603298a)

sns.boxplot(x=D_big['OutletSales'])

plt.title('Boxplot de OutletSales')

plt.show()

![Boxplot de OutletSales](https://github.com/user-attachments/assets/8faebe97-a0fd-4c01-aaa1-bc69f4f24d3e)

## 6. Documentação e Insights
Com base nas análises, documentei os principais insights e preparei a base de dados para futuras modelagens.



## Principais Resultados
Correlação: Identifiquei uma forte correlação positiva entre MRP e OutletSales (+0.57), indicando que produtos mais caros geram mais receita.

## Impacto Categórico:

Supermercados (OutletType) têm desempenho superior em vendas, enquanto Grocery apresenta valores mais baixos.

Outlets localizados em áreas urbanas (LocationType) superam em vendas os localizados em áreas rurais ou suburbanas.

Tendências Temporais: Outlets mais novos (fundados em anos recentes) apresentaram leve aumento nas vendas.

Outliers: Identifiquei valores extremos em MRP e OutletSales, que podem ser explorados ou tratados futuramente.


## Próximos Passos
Refinar o tratamento de outliers.

Codificar variáveis categóricas para machine learning.

Implementar modelos preditivos básicos para prever OutletSales.

Como Executar
Clone o repositório:


git clone https://github.com/frannsantos7/Projeto-Big-Mart.git

Instale as dependências:

pip install pandas matplotlib seaborn

Abra o arquivo analysis.ipynb em um ambiente Jupyter Notebook para explorar as análises.
