# 0.0 - Análise de Perfil de Clientes
>**[Nota]**:
 A descrição presente nesta seção consta no case fornecido para seleção da vaga de Cientista de Dados. Recebido, via email, em 01/10/2024.

A análise de perfil de clientes ajuda uma empresa a adaptar seus produtos com base nos diferentes segmentos de clientes. Por exemplo, em vez de gastar dinheiro para promover um novo produto para todos os clientes da base de dados da empresa, é possível analisar quais segmentos de clientes têm maior probabilidade de comprar o produto e, então, direcionar a campanha de marketing especificamente para esses segmentos.

A parte mais importante da análise de personalidade do cliente é responder a algumas perguntas, tais como:

- O que as pessoas dizem sobre o seu produto? Isso revela a atitude dos clientes em relação ao produto.
- O que as pessoas fazem? Isso mostra o comportamento dos clientes, o que eles estão realmente fazendo em vez do que dizem sobre o produto.

Com base nestas informações, sua tarefa será realizar uma análise de um conjunto de dados fictícios de clientes. Seu objetivo é identificar segmentos de clientes e recomendar ações de marketing baseadas no comportamento e nas opiniões dos clientes sobre o produto.


---
# 1.0 Entendimento do Problema de Negócio
## 1.0.1 Objetivos de negócio

**Contexto**: A atuação de times de marketing, sobretudo no contexto do comércio eletrônico, é de suma importância para o sucesso das empresas em um ambiente de negócios cada vez mais competitivo. Melhorias na assertividade de posicionamento de marca, na atração de público e na personalização de ofertas, são alguns dos pontos de atenção para profissionais da área.

A equipe de marketing da empresa MIW deseja compreender em detalhes o comportamento de seus clientes e identificar padrões em suas ações, a fim de desenvolver ações personalizadas para cada perfil de cliente.

**Objetivos**:
- Identificar padrões nas ações de clientes;
- Ilustrar o comportamento de clientes;
- Identificar segmentos de clientes;
- Recomendar ações de marketing baseadas no comportamento e nas opiniões dos clientes sobre o produto.

## 1.0.2 Avaliação da situação
A disponibilidade de recursos para a execução deste projeto são:
- Dataset disponibilizado pelo time de marketing;
- Python e suas bibliotecas;
- 01 Cientista de Dados;
- 01 semana de prazo

## 1.0.3 Objetivos da mineração de dados
A fim de cumprir os objetivos de negócio propostos, propõem-se a execução das seguintes etapas:
- Elaboração de documentação executiva;
- Condução de análise exploratória de dados;
- Execução de processo de agrupamento de clientes em *clusters*;
- Elaboração de um modelo de classificação de clientes, por meio de aprendizado supervisionado.

Como critérios de avaliação do projeto, propõem-se:
- a
- b
- c

--- 
# 2.0 Compreensão dos Dados
Conforme supracitado, os dados disponíveis para este projeto foram anteriormente disponbilizados e são os únicos recursos disponíveis para a elaboração deste protótipo.

## 2.1 Descrição dos Dados
O *dataset* disponibilizado contém um total de 2240 instâncias e 29 colunas, quais sejam:

| **#** 	|      **Coluna**     	|                             **Descrição**                            	|
|:-----:	|:-------------------:	|:--------------------------------------------------------------------:	|
|   0   	|          ID         	|                    Identificação única do cliente                    	|
|   1   	|      Year_Birth     	|                     Ano de nascimento do cliente                     	|
|   2   	|      Education      	|                    Grau de escolaridade do cliente                   	|
|   3   	|    Marital_Status   	|                        Status civil do cliente                       	|
|   4   	|        Income       	|                       Receita anual do cliente                       	|
|   5   	|       Kidhome       	|            Quantidade de crianças na residência do cliente           	|
|   6   	|       Teenhome      	|          Quantidade de adolescentes na residência do cliente         	|
|   7   	|     Dt_Customer     	|                      Data de cadastro do cliente                     	|
|   8   	|       Recency       	|            Número de dias desde a última compra do cliente           	|
|   9   	|       MntWines      	|                 Quantia gasta em vinhos no último ano                	|
|   10  	|      MntFruits      	|                 Quantia gasta em frutas no último ano                	|
|   11  	|   MntMeatProducts   	|                 Quantia gasta em carnes no último ano                	|
|   12  	|   MntFishProducts   	|             Quantia gasta em frutos do mar no último ano             	|
|   13  	|   MntSweetProducts  	|                 Quantia gasta em doces no último ano                 	|
|   14  	|     MntGoldProds    	|            Quantia gasta em produtos premium no último ano           	|
|   15  	|  NumDealsPurchases  	|              Número de compras em promoção no último ano             	|
|   16  	|   NumWebPurchases   	|             Número de compras feitas na web no último ano            	|
|   17  	| NumCatalogPurchases 	|     Número de compras feitas utilizando o catálogo no último ano     	|
|   18  	|  NumStorePurchases  	|        Número de compras feitas em lojas físicas no último ano       	|
|   19  	|  NumWebVisitsMonth  	|         Número de visitas ao website da empresa no último mês        	|
|   20  	|     AcceptedCmp3    	|   1 se o cliente aceitou a oferta na 3ª campanha, 0 caso contrário   	|
|   21  	|     AcceptedCmp4    	|   1 se o cliente aceitou a oferta na 4ª campanha, 0 caso contrário   	|
|   22  	|     AcceptedCmp5    	|   1 se o cliente aceitou a oferta na 5ª campanha, 0 caso contrário   	|
|   23  	|     AcceptedCmp1    	|   1 se o cliente aceitou a oferta na 1ª campanha, 0 caso contrário   	|
|   24  	|     AcceptedCmp2    	|   1 se o cliente aceitou a oferta na 2ª campanha, 0 caso contrário   	|
|   25  	|       Complain      	|  1 se o cliente registrou reclamação no último ano, 0 caso contrário 	|
|   26  	|    Z_CostContact    	|                         *difícil inferência*                         	|
|   27  	|      Z_Revenue      	|                         *difícil inferência*                         	|
|   28  	|       Response      	| 1 se o cliente aceitou a oferta na última campanha, 0 caso contrário 	|

## 2.X Exploratory Data Analysis

>**[Nota]:** 
A fim de adquirir uma macrovisão do contexto apresentado no case, foi elaborada uma análise exploratória dos dados. O código utilizado pode ser verificado em `src/eda.ipynb`, que foi utilizado como um ambiente de prototipagem e visualização. Algumas das funções utilizadas durante o processo de EDA constam no script `eda.py`. Este script contém uma série de métodos e propriedades básicos e foi programado com o intuito de reduzir a verbosidade e repetição de operações no ambiente Jupyter.

