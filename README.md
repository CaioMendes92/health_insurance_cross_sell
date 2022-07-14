# Health Insurance Cross Sell

![alt text](https://github.com/CaioMendes92/health_insurance_cross_sell/blob/main/img/insurance-capa.jpg?raw=true)

## 1. Problema de Negócio
Disclaimer: O Contexto a seguir, é completamente fictício, a empresa, o contexto, o CEO, as perguntas de negócio existem somente na minha imaginação. 

A Insurance All é uma empresa que fornece seguro de saúde para seus clientes e o time de produtos está analisando a possibilidade de oferecer aos assegurados, um novo produto: Um seguro de automóveis.

Assim como o seguro de saúde, os clientes desse novo plano de seguro de automóveis precisam pagar um valor anualmente à Insurance All para obter um valor assegurado pela empresa, destinado aos custos de um eventual acidente ou dano ao veículo.

A Insurance All fez uma pesquisa com cerca de 380 mil clientes sobre o interesse em aderir a um novo produto de seguro de automóveis, no ano passado. Todos os clientes demonstraram interesse ou não em adquirir o seguro de automóvel e essas respostas ficaram salvas em um banco de dados junto com outros atributos dos clientes.

O time de produtos selecionou 127 mil novos clientes que não responderam a pesquisa para participar de uma campanha, no qual receberão a oferta do novo produto de seguro de automóveis. A oferta será feita pelo time de vendas através de ligações telefônicas.

Contudo, o time de vendas tem uma capacidade de realizar 20 mil ligações dentro do período da campanha.

## 2. Premissas do Negócio
* Foi feita uma divisão dos dados, em que 80% dos dados foram utilizados para treino e 20% para validação.

### 2.1 Descrição das features
* **id**	Identificador do cliente (único)
* **Gender**	Sexo do cliente
* **Age**	Idade do cliente
* **Driving_License**	0: Cliente não possui licença para dirigir - 1: Cliente possui licença para dirigir
* **Region_Code**	Código único para região do cliente
* **Previosly_Insured**	0: Cliente não possui seguro automóvel - 1: Cliente já possui seguro automóvel
* **Vehicle_Age**	Idade do veículo
* **Vehicle_Damage**	0: Cliente já se envolveu em sinistros - 1: Cliente nunca se envolveu em sinistros
* **Annual_Premium**	Valor do prêmio anual pago pelo cliente
* **Policy_Sales_Channel**	Código contento o meio de contato com o cliente (Correio, telefone, e-mail, pessoalmente...)
* **Vintage**	Número de dias que o cliente esteve associado à empresa
* **Response**	0: Cliente não está interessado no seguro automóvel - 1: Cliente está interessado

## 3. Planejamento da Solução
A partir do pedido do time de produto, é possível observar que esse é um claro problema de learn to rank. Para solucioná-lo, será usado um modelo de Machine Learning para a posição do rank. Depois disso, será gerado um arquivo .csv com o dataset original + rank, informando os clientes em ordem de ligação. 

Será utilizado o método cíclico CRISP-DM (Cross-Industry Process - Data Science) , que é um metodo de gerenciamento de projetos para ciência de dados. A vantagem desse método é que se entrega o valor de uma forma mais rápida. O processo consiste nas seguintes etapas:

**0.** Aquisição dos Dados
* Nesse projeto, os dados vieram do Kaggle: https://www.kaggle.com/c/rossmann-store-sales/data

**1.** Descrição dos Dados
* A partir de métricas estatísticas encontra-se valores mínimos, máximos, outliers, médias, dados faltantes entre outros problemas que serão enfrentado durante o projeto.

**2.** Feature Engineering
* Nesta etapa serão encontrados novos atributos, a partir das variáveis originais, de forma que melhore a análise exploratória de dados. Além disso, cria-se hipóteses que serão validadas (ou rejeitadas) na análise.

**3.** Filtragem de Dados
* A principal motivação para realizar este passo é por restrição de negócios. Alguns atributos podem impactar no resultado, mas não estarão disponíveis antes do modelo em produção.

**4.** Análise Exploratória de Dados
* O objetivo de uma análise exploratória de dados (EDA - do inglês: Exploratory Data Analysis) é entender como as variáveis impactam no fenômeno a ser modelado e encontrar insights que ajudem a solucionar o problema. 

**5.** Preparação dos Dados
* Aqui é feito a preparação dos dados para aplicar os modelos de aprendizado de máquina.

**6.** Seleção de Atributos
* Nesta etapa serão selecionadas as variáveis mais relevantes para o modelo.

**7.** Modelos de Machine Learning
*	Seleciona-se alguns algoritmos de aprendizagem de máquina e realiza-se o treinamento e o teste para observar qual modelo performa melhor.

**8.** Ajuste Fino dos Hiperparâmetros
* Ajuste dos hiperparâmetros de forma que o modelo de aprendizado de máquina performe ainda melhor.

**9.** Model Performance
* A partir do melhor modelo encontrado nos passos 7 e 8, é feito o rankeamento e gerado um arquivo com a tabela + ranking.

## 4. Top 3 Insights

**1.** Usuários com automóveis com menos de um ano de uso possuem menos interesse em contratar um seguro.
**VERDADEIRO.** Usuários com menos de um ano de uso possuem menos interesse em contratar um seguro. Usuários com carros entre 1 e 2 anos tem mais interesse em seguros.

![alt text](https://github.com/CaioMendes92/health_insurance_cross_sell/blob/main/img/insight1.png?raw=true)

**2.** A maioria dos usuários que desejam um seguro de saúde são mulheres.
**Falso.** Homens desejam mais seguros que mulheres
![alt text](https://github.com/CaioMendes92/health_insurance_cross_sell/blob/main/img/insight2.png?raw=true)

**3.**Usuários com idade maior que 40, estão mais interessadas em contratar um seguro.
**Verdadeiro.** Usuários com mais de 40 anos tem interesse em contratar um seguro.
![alt text](https://github.com/CaioMendes92/health_insurance_cross_sell/blob/main/img/insight3a.png?raw=true)
![alt text](https://github.com/CaioMendes92/health_insurance_cross_sell/blob/main/img/insight3b.png?raw=true)

## 5. Modelos de Machine Learning

Os modelos utilizados neste passo foram:

* KNN
* Logistic Regression
* Extra Trees
* XGBoost
* AdaBoost

## 6. Performance dos modelos de machine learning
A performance foi avaliada a partir do Precision @k e pelo Recall @k. A performance real dos modelos (após o Cross-Validation) é dada pela média dos erros +/- o desvio padrão do erro,

![alt text](https://github.com/CaioMendes92/health_insurance_cross_sell/blob/main/img/modelos_cv.png?raw=true)

O algoritmo escolhido foi o XG Boost (Recall: 91,42%).

## 7. Performance após ajuste fino dos hiperparâmetros (Hyperparameter Fine Tuning)
![alt text](https://github.com/CaioMendes92/health_insurance_cross_sell/blob/main/img/output_final.png?raw=true)

