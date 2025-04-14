# 🛒 Big Mart Sales Analysis


## ✨ Sobre o Projeto
Este projeto tem como objetivo explorar o conjunto de dados das vendas da Big Mart, analisando fatores importantes que impactam nos resultados de vendas. 🔍  
- **Objetivo:** Identificar padrões e fornecer insights estratégicos 📊  
- **Ferramentas Utilizadas:** Python, Pandas, Matplotlib, Seaborn 🐍  
- **Resultados:** Documentação detalhada e preparação para modelagem futura 🚀


---

## Motivação
Ao trabalhar com o conjunto de dados da Big Mart, a motivação foi:
1. Aprender a tratar e explorar dados, com foco em limpeza e visualizações.
2. Identificar os principais fatores que impactam nas vendas, tanto numéricos (como preços) quanto categóricos (como tipo de outlet e localização).
3. Criar insights claros e bem documentados, com base em análises exploratórias.
4. Usar visualizações para destacar padrões importantes e preparar os dados para possíveis modelos futuros.

---

## Etapas do Projeto
Abaixo, detalho as etapas realizadas no projeto:

### 1. Importação de Bibliotecas
### 🖥️ Configuração Inicial
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns



### 2. Carregamento do Conjunto de Dados
O conjunto de dados foi carregado e estruturado em um DataFrame:

python
D_big = pd.read_csv(r'C:\Users\frann\Documents\Projeto_Big_mart\Train-Set.csv')

3. Entendimento Inicial do Conjunto de Dados
Foram feitas verificações para entender as características do DataFrame:

python
 Verificando os tipos de dados
print(D_big.dtypes)
![Descrição da Imagem](imagens/sua_imagem.png)


 Identificando valores ausentes
print(D_big.isnull().sum())

4. Tratamento de Valores Ausentes
Os valores ausentes foram tratados para garantir a consistência dos dados:

Substituí os valores ausentes na coluna Weight pela média.

Substituí os valores ausentes na coluna OutletSize pela moda.

python
 Tratamento da coluna 'Weight' (numérica)
weight = D_big['Weight'].mean()
D_big['Weight'] = D_big['Weight'].fillna(weight)

 Tratamento da coluna 'OutletSize' (categórica)
mode_outlet_size = D_big['OutletSize'].mode()[0]
D_big['OutletSize'] = D_big['OutletSize'].fillna(mode_outlet_size)


5. Análises Explorando Padrões
5.1. Distribuição de Dados
Verifiquei a distribuição da coluna Weight para entender como os valores estão distribuídos após a substituição pela média:

python
sns.histplot(D_big['Weight'], kde=True)
plt.title('Distribuição do Peso Após Correção')
plt.xlabel('Peso')
plt.ylabel('Frequência')
plt.show()




5.2. Correlações Numéricas
Criei uma matriz de correlação para entender as relações entre as variáveis numéricas, com um destaque para MRP e OutletSales:

python
numeros = D_big.select_dtypes(include=['float64', 'int64'])
matriz_de_correlação = numeros.corr()

 Heatmap da correlação
sns.heatmap(matriz_de_correlação, annot=True, cmap="coolwarm")
plt.title('Mapa de Calor da Correlação entre Variáveis')
plt.show()


5.3. Relações Categóricas
Explorei como variáveis categóricas, como OutletType e LocationType, afetam OutletSales:

python
sns.boxplot(x=D_big['OutletType'], y=D_big['OutletSales'])
plt.title('Impacto do Tipo de Outlet nas Vendas')
plt.xlabel('Tipo de Outlet')
plt.ylabel('Vendas')
plt.show()

sns.boxplot(x=D_big['LocationType'], y=D_big['OutletSales'])
plt.title('Impacto da Localização do Outlet nas Vendas')
plt.xlabel('Localização do Outlet')
plt.ylabel('Vendas')
plt.show()


5.4. Análise Temporal
Verifiquei como o ano de estabelecimento (EstablishmentYear) dos outlets impacta nas vendas:

python
sns.lineplot(x=D_big['EstablishmentYear'], y=D_big['OutletSales'])
plt.title('Ano de Estabelecimento vs. Vendas')
plt.xlabel('Ano de Estabelecimento')
plt.ylabel('Vendas')
plt.show()
5.5. Outliers
Identifiquei potenciais outliers nas variáveis numéricas:

python
sns.boxplot(x=D_big['MRP'])
plt.title('Boxplot do Preço Máximo de Varejo')
plt.show()

sns.boxplot(x=D_big['OutletSales'])
plt.title('Boxplot de OutletSales')
plt.show()


6. Documentação e Insights
Com base nas análises, documentei os principais insights e preparei a base de dados para futuras modelagens.



6. Documentação e Insights
Com base nas análises, documentei os principais insights e preparei a base de dados para futuras modelagens.

Principais Resultados
Correlação: Identifiquei uma forte correlação positiva entre MRP e OutletSales (+0.57), indicando que produtos mais caros geram mais receita.

Impacto Categórico:

Supermercados (OutletType) têm desempenho superior em vendas, enquanto Grocery apresenta valores mais baixos.

Outlets localizados em áreas urbanas (LocationType) superam em vendas os localizados em áreas rurais ou suburbanas.

Tendências Temporais: Outlets mais novos (fundados em anos recentes) apresentaram leve aumento nas vendas.

Outliers: Identifiquei valores extremos em MRP e OutletSales, que podem ser explorados ou tratados futuramente.


Próximos Passos
Refinar o tratamento de outliers.

Codificar variáveis categóricas para machine learning.

Implementar modelos preditivos básicos para prever OutletSales.

Como Executar
Clone o repositório:

bash
git clone https://github.com/seu-usuario/Projeto-Big-Mart.git
Instale as dependências:

bash
pip install pandas matplotlib seaborn
Abra o arquivo analysis.ipynb em um ambiente Jupyter Notebook para explorar as análises.
