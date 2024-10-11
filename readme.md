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
- Silhouette score -> KMeans;
- Score de distorção -> KMeans;
- Validação com especialistas da área de marketing.

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

### 2.1.1 Análise de variáveis demográficas
Esta seção descreve os passos realizados na análise demográfica dos dados de clientes.

**Tratamento da Variável 'Year_Birth':**
Preliminarmente, foram retirados outliers, que apontavam para idades muito avançadas.

1. Conversão de Ano de Nascimento para Idade
    - A coluna 'Year_Birth' foi convertida para idade atual dos clientes.
    - Foi calculada a diferença entre o ano da análise (2014) e o ano de nascimento.

2. Criação de Faixas Etárias
    - Foram criadas três faixas etárias, cada uma contendo aproximadamente 33% dos dados.
    - Nova coluna: 'Age_Range' (categórica)

**Análise preliminar da Variável Marital_Status:**
- Avaliação das entradas de 'Marital_Status': foram identificadas entradas similares ('Single', 'Alone'), que foram alocadas em uma única categoria.
- Entradas contendo valores de difícil interpretação e baixa frequência, como 'Absurd' e 'YOLO', foram descartadas.
- Criação de gráfico de barras (countplot) representando a frequência de clientes por faixa etária e nível educacional.

**Análise preliminar da Data de Aquisição do Cliente:**
1. Conversão de Formato
    - A coluna 'Dt_Customer' foi convertida de 'object' para 'datetime'.
2. Extração do Ano
    - O ano foi extraído da data de aquisição do cliente.
3. Criação de Lotes de Clientes
    - Foi criada uma nova coluna chamada 'Batch'.
    - Cada ano foi mapeado para um lote correspondente de clientes.

**Observações e Insights Preliminares**
1. Distribuição Educacional:
   - Graduação é o nível educacional mais comum em todas as faixas etárias.
   - PhDs e Mestrados são mais prevalentes nas faixas etárias mais velhas (39-50 e 50-78).
   - Educação básica é mais comum na faixa etária mais jovem (18-39).

2. Padrões por Faixa Etária:
   - A faixa etária de 18-39 anos mostra maior diversidade nos níveis educacionais.
   - A faixa de 50-78 anos tem uma proporção maior de graus avançados (PhD e Mestrado).

3. Potenciais Correlações:
   - Pode haver uma correlação entre idade e nível educacional, com clientes mais velhos tendendo a ter níveis educacionais mais altos.

## 2.2 Análise Exploratória dos Dados

>**[Nota]:** 
A fim de adquirir uma macrovisão do contexto apresentado no case, foi elaborada uma análise exploratória dos dados. O código utilizado pode ser verificado em `src/eda.ipynb`, que foi utilizado como um ambiente de prototipagem e visualização. Optou-se por realizar todo o processo de EDA e data cleaning neste Jupyter Notebook, sem a utilização de módulos. Neste sentido, indica-se a possibilidade de se elaborar, futuramente, um script que contenha funções capazes de executar o pré-processamento deste conjunto de dados, a fim de reduzir a verbosidade do código e melhorar sua organização.

### 2.2.1 Valor Gasto vs. Renda vs. Categorias de Produtos vs. Níveis Educacionais

#### Principais Descobertas
- A maior parte da receita da MIW vem de Vinhos e Produtos de Carne.
- Há uma grande oportunidade para melhorar o desempenho das demais categorias.
- Os níveis educacionais não parecem afetar significativamente os padrões de consumo.
- Pessoas com renda superior a $40.000,00 tendem a gastar mais em Vinhos e Produtos de Carne.
- Na faixa de renda entre $40.000,00 e $80.000,00, os gastos com Vinhos se distribuem uniformemente, sugerindo que maior renda não necessariamente implica em maiores gastos com Vinhos.
- Após atingir certa estabilidade financeira, as pessoas tendem a consumir mais álcool.

#### Implicações
- Potencial para estratégias de marketing focadas em aumentar as vendas nas categorias de produtos menos populares.
- Oportunidade para segmentação de clientes baseada em níveis de renda, especialmente para produtos de maior valor.

### 2.2.2 Valor Gasto por Categoria de Produto vs. Estado Civil

#### Principais Descobertas
- O estado civil não parece afetar significativamente o valor gasto nas categorias de produtos mapeadas.
- Esta observação é contra-intuitiva e merece uma investigação mais aprofundada.

#### Implicações
- Pode ser necessário reconsiderar estratégias de marketing baseadas em estado civil.
- Oportunidade para investigar outros fatores que possam influenciar os padrões de gasto.

### 2.2.3 Número de Compras vs. Renda vs. Canal de Venda

#### Principais Descobertas
- Há uma tendência geral de que pessoas com rendas mais altas realizam mais compras.
- A relação entre renda e número de compras varia de acordo com o canal de venda.

#### Implicações
- Potencial para estratégias de marketing personalizadas por canal de venda, considerando os níveis de renda dos clientes.
- Oportunidade para otimizar a experiência de compra nos canais preferidos pelos clientes de alta renda.

#### Conclusões Gerais
1. A renda é um fator significativo nos padrões de gasto e frequência de compra.

2. As categorias de Vinhos e Produtos de Carne são as mais lucrativas e merecem atenção especial.

3. O estado civil pode ser menos importante do que se pensava inicialmente na determinação dos padrões de compra.

4. Há oportunidades significativas para melhorar o desempenho em categorias de produtos menos populares.

5. A segmentação de clientes baseada em renda e preferências de canal de venda pode ser eficaz para estratégias de marketing futuras.

### 2.2.4 Análise Multivariada

#### Principais Observações

1. Correlação Negativa entre Número de Crianças e Gastos
   - Existe uma correlação negativa entre o número de crianças em casa e o valor gasto em Vinhos e outros produtos mapeados neste conjunto de dados.
   - Este fato é particularmente curioso, pois se poderia esperar que ter mais pessoas em casa implicaria em maiores gastos com produtos domésticos.
   - Recomendação: Aplicar técnicas de inferência causal para investigar mais a fundo este fenômeno.

2. Ausência de Correlação com Adolescentes
   - Não há correlação relevante - nem positiva nem negativa - entre o número de adolescentes e o mix de produtos mapeados neste conjunto de dados.

3. Impacto de Crianças nas Compras
   - Ter crianças em casa tem uma correlação negativa significativa com o número de compras feitas no site, no catálogo e na loja.
   - Isto pode indicar que o mix de produtos da MIW pode não atender às necessidades de famílias com crianças pequenas.

4. Correlações entre Canais de Compra e Produtos
   - Existem correlações relevantes entre Compras por Catálogo e Compras em Loja com o valor gasto em vinhos, frutas, produtos de carne, produtos doces e produtos de ouro.
   - Isto pode ser uma evidência de que a marca MIW está posicionada como uma loja de departamentos.

5. Compras com Desconto
   - Há uma correlação ligeiramente negativa entre o número de Compras com Desconto e o valor gasto em Frutas, Peixes, Produtos de Carne e Produtos Doces.
   - Este fato é curioso, pois se esperaria que oferecer descontos aumentasse a receita do negócio.

#### Implicações e Recomendações

1. Segmentação de Clientes
   - Desenvolver estratégias de marketing específicas para famílias com crianças, possivelmente expandindo o mix de produtos para atender melhor suas necessidades.

2. Análise de Canais de Venda
   - Investigar por que as compras por catálogo e em loja têm correlações mais fortes com certos produtos. Isso pode informar estratégias de merchandising e layout de loja.

3. Política de Descontos
   - Revisar a estratégia de descontos, especialmente para as categorias de produtos que mostram correlação negativa com compras com desconto.

4. Pesquisa de Mercado
   - Conduzir pesquisas qualitativas para entender melhor por que famílias com crianças tendem a gastar menos em todas as categorias.

5. Análise de Compras
   - Realizar uma análise detalhada de compras para identificar padrões de compra conjunta entre diferentes categorias de produtos.

# 3. Agrupamento de Clientes
A fim de identificar os segmentos de clientes atedidos pela MIW, foi elaborada uma análise de *clusters*.

Para tal, foram utilizadas 22 variáveis originalmente numéricas e 2 categóricas, que, por sua vez, passaram por um processo de *enconding*, utilizando o método One Hot Enconder.

Na sequência, foi aplicada a técnica de padronização dos dados Standard Scaler. Aqui, vale a ressalva de que talvez a utilização de outro método de padronização mostre-se mais adequado, visto que algumas de nossas variáveis não possuem distribuição normal. Sugere-se o teste de métodos como MinMaxScaler or RobustScaler. Testes preliminares com MinMaxScaler se mostraram promissores, contudo, necessitam de avaliação.

Na sequência, foi aplicada uma técnica de redução de dimensionalidade, a partir de Análise de componentes principais. Foi avaliada a métrica de variância explicada para diversos valores de componentes, e, por fim, foram selecionadas 3 componentes.

Finalmente, foi realizado o agrupamento do conjunto de dados, avaliando-se as métricas de distorção e silhueta. Há espaço para a melhoria destas métricas, contudo, considerando-se o contexto deste projeto, entende-se que o processo de agrupamento foi capaz de gerar *clusters* suficientemente bem definidos e que podem atender aos objetivos propostos.

>[NOTA]: os resultados e desenvolvimento específicos desta etapa podem ser conferidos no arquivo `clustering.ipynb`.

# 4 Resultados 
A partir da elaboração deste projeto, foi possível descrever o conjunto de clientes em 4 grupos de características demográficas e comportamentos comerciais distintos.

## Cluster 0:
- Tamanho do Cluster: 957 de 2208
- Renda Média ~ 33.537,5
- 82% têm filhos em casa;
- 40% têm adolescentes em casa;
- Eles gastam baixos valores em qualquer categoria de produto mapeada pelo conjunto de dados (Vinhos, Frutas, Produtos de Carne, Produtos de Peixe, Produtos Doces, Produtos de Ouro);
- 2 compras em promoção durante o período analisado;
- 2 compras pela internet durante o período analisado;
- 0,51 compras por catálogo durante o período analisado;
- 3 compras em loja durante o período analisado;
- 6,5 visitas à web por mês;
- 41,2 anos de idade;
- 50% deles têm graduação;
- 25% deles são solteiros;
- 64% são casados ou estão com alguém.

### Ações Recomendadas
**Promoções voltadas para a família**: Crie uma campanha de marketing que se concentre em produtos voltados para a família e ofertas econômicas, enfatizando as compras em grandes quantidades para famílias com crianças. Ofereça descontos em itens essenciais que atraiam famílias com crianças, como lanches, bebidas e soluções para refeições rápidas.

**Programa de fidelidade "Budget-Friendly"**: Desenvolva um programa de fidelidade que recompense os clientes por suas compras cumulativas. Ofereça pontos para compras em grandes quantidades ou para categorias específicas de produtos que são populares entre as famílias, como carnes e doces, e permita que os pontos sejam trocados por prêmios ou descontos voltados para a família.

***

## Cluster 1:
- Tamanho do Cluster: 175 de 2208
- Renda Média ~81.152,66;
- 3% têm filhos em casa;
- 10% têm adolescentes em casa;
- Compram a cada 45 dias (em média);
- Gastaram ~885 em vinhos durante o período analisado;
- Gastaram ~485 em produtos de carne durante o período analisado;
- 1 compra em promoção durante o período analisado;
- 5,65 compras pela internet durante o período analisado;
- 6,24 compras por catálogo durante o período analisado;
- 8,10 compras em loja durante o período analisado;
- 3,24 visitas à web por mês;
- 75% deles aceitaram a campanha número 5;
- 50% deles aceitaram a campanha número 1;
- 42% deles têm graduação;
- 33% deles têm doutorado (PhD);
- ~60% deles são casados ou estão com alguém.

### Ações Recomendadas
**Eventos de desgustação e harmização:** recomenda-se o a execução de eventos de degustação para este público. Eles apresentam grande tendência de gastos elevados em produtos de valor agregado e, por possuírem maior renda, podem estar propensos a apreciar experiências personalizadas.

**Programa de membros premium:** a partir da introdução de um programa de membros premium, será possível coletar ainda mais dados e compreender melhor as tendências de consumo deste público. A partir disso, poderemos selecionar produtos para ofertar periodicamente, com condições especiais.

***
## Cluster 2:
- Tamanho do Cluster: 483 de 2208
- Renda Média ~71.800,00
- 6% deles têm um filho em casa;
- 31% deles têm um adolescente em casa;
- Compram a cada 51 dias;
- Gastaram ~488 em vinhos durante o período analisado;
- Gastaram ~402,65 em produtos de carne durante o período analisado;
- Gastaram ~100 em produtos de peixe durante o período analisado;
- 1,68 compras em promoção durante o período analisado;
- 5,3 compras pela internet durante o período analisado;
- 5,5 compras por catálogo durante o período analisado;
- 8,65 compras em loja durante o período analisado;
- 3 visitas à web por mês;
- Baixo impacto geral das campanhas de marketing;
- Idade média de 46 anos;
- 67% deles têm graduação;
- 64% são casados ou estão com alguém.

### Ações Recomendadas
**Campanhas de saúde e bem-estar:** este público apresenta uma certa propensão ao consumo de frutos do mar, que são produtos mais leves. O compartilhamento de receitas que levem este tipo de ingrediente, juntamente com ofertas em loja e catálogo pode aumentar o faturamento desta categoria de produto.

**Assinatura de produtos selecionados**: embora ainda tenha receita média elevada, este grupo tende a ter uma média de gastos menor, porém, pode-se aumentar sua fidelização através do fornecimento de ofertas periódicas de carnes, vinhos e peixes.

****
***
## Cluster 3:
- Tamanho do Cluster: 593 de 2208
- Renda Média ~55.991,00
- 26% têm filhos;
- 94% deles têm um adolescente em casa;
- Compram a cada 48 dias;
- Gastaram ~420 em vinhos durante o período analisado;
- Gastaram ~114,4 em produtos de carne durante o período analisado;
- 3,76 compras em promoção durante o período analisado;
- 6 compras pela internet durante o período analisado;
- 2,77 compras por catálogo durante o período analisado;
- 7,15 compras em loja durante o período analisado;
- 5,86 visitas à web por mês;
- 13% deles aceitaram a campanha 4;
- Idade média de 51 anos;
- 39% deles têm graduação;
- 22% deles têm mestrado;
- 33% deles têm doutorado (PhD);
- 67% são casados ou estão com alguém;
- 14% deles são divorciados.

### Ações Recomendadas
**"Noite da família":** grande parte deste grupo possui adolescentes em casa, o que pode ser uma excelente oportunidade para se ofertar produtos que possam compor uma experiência de programa familiar, como doces, sucos e refeições convenientes.

***
