# Material e métodos do artigo "Na mira de Bolsonaro, questões 'ideológicas' e sobre ditadura do Enem são eficientes"

A reportagem, feita a partir dos microdados do Enem, se baseia em um modelo estatístico que estima a chance de um candidato acertar uma questão dada a sua proficiência na prova.

Para isso, foram calculados três parâmetros. São eles: parâmetro de discriminação (mede se a questão consegue diferenciar os candidatos de acordo com o nível de conhecimento naquele tema), parâmetro de dificuldade (indica o nível de dificuldade daquela questão) e parâmetro de acerto casual (estima a chance do candidato acertar porque chutou). 

Eles fazem parte da TRI (Teoria da Resposta ao Item) de 3 parâmetros, metodologia que o Inep utiliza para corrigir e dar nota aos candidatos. O órgão, contudo, não forneceu o valor dos parâmetros que são utilizados, e foi feito um cálculo próprio.

Foram consideradas na análise 24 questões que abordam temas como ditadura militar ou questões LGBTQIA+ e que foram alvo de críticas de grupos conservadores.

## Dados:

* As respostas e notas dos alunos foram obtidas a partir dos [microdados do Enem disponibilizados pelo Inep](https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados/enem)\*; 

* Foram analisadas somente as primeiras aplicações das provas de cada ano\*\*;

* A correspondência entre as questões e as respostas dos alunos presentes nos microdados foram feitas utilizando os arquivos  “itens_prova” de cada ano\*\*\*.

* Como os itens supostamente polêmicos estavam todos nas provas de linguagem e códigos (LC) e de ciências humanas (CH), somente essas provas analisadas. No caso de linguagens foram removidos os itens de inglês e espanhol

\* Dois alunos foram removidos porque apresentavam menos respostas do que seria o esperado (aluno com ID 400000364244 de 2012 apresentava 40 respostas válidas na prova de LC e aluno com ID 100000703699 apresentava 44 respostas válidas na prova de LC em 2009. Em ambos casos eram esperadas 45 respostas válidas)

\*\* Apesar de essa observação não estar presente no dicionário de dados, as provas com ID de 101 a 116 de 2010 são reaplicações;

\*\*\* A prova rosa de 2014 de linguagens e códigos (ID 198) apresenta ordenação errada no arquivo “itens_prova”, por isso para esse caso específico foi utilizada a ordem  [disponinilizada pelo curso objetivo](https://www.curso-objetivo.br/vestibular/resolucao_comentada/enem/enem2014_2dia.asp?img=01). Foi confirmada que essa ordem está correta, pois a ordenação das respotas corretas dela bate com a do gabarito presente nos microdados. 


## Questões supostamente polêmicas

Foram selecionados itens que tratam da ditatura ou que foram alvos de críticas por um suposto viés ideológico. Abaixo a tabela com os itens:

|     id|  ano|area |tipo     |link_critica                                                                                                                   |
|------:|----:|:----|:--------|:------------------------------------------------------------------------------------------------------------------------------|
|  68887| 2014|ch   |critica  |[link](https://oglobo.globo.com/brasil/educacao/academicos-atacam-doutrinacao-do-enem-14546063)                                |
|  14258| 2015|ch   |critica  |[link](https://oglobo.globo.com/brasil/educacao/especialistas-se-dividem-sobre-doutrinacao-em-prova-do-enem-17909168)          |
|  38029| 2015|ch   |critica  |[link](http://g1.globo.com/educacao/enem/2015/noticia/2015/10/deputados-bolsonaro-e-feliciano-acusam-enem-de-doutrinacao.html) |
| 112076| 2018|lc   |critica  |[link](https://twitter.com/francischini_/status/1059265756339363840?lang=en)                                                   |
| 112113| 2018|lc   |critica  |NA                                                                                                                             |
|  60218| 2009|lc   |ditadura |NA                                                                                                                             |
|  60220| 2009|lc   |ditadura |NA                                                                                                                             |
|  70736| 2010|ch   |ditadura |NA                                                                                                                             |
|  70778| 2010|ch   |ditadura |NA                                                                                                                             |
|  75440| 2011|ch   |ditadura |NA                                                                                                                             |
|   7589| 2012|ch   |ditadura |NA                                                                                                                             |
|  13273| 2012|lc   |ditadura |NA                                                                                                                             |
|   8604| 2013|ch   |ditadura |NA                                                                                                                             |
|  24456| 2014|ch   |ditadura |NA                                                                                                                             |
|  68434| 2014|ch   |ditadura |NA                                                                                                                             |
|  24576| 2015|ch   |ditadura |NA                                                                                                                             |
|  82324| 2015|lc   |ditadura |NA                                                                                                                             |
|  86985| 2016|ch   |ditadura |NA                                                                                                                             |
|  97744| 2016|ch   |ditadura |NA                                                                                                                             |
|  24935| 2017|ch   |ditadura |NA                                                                                                                             |
|  77759| 2017|lc   |ditadura |NA                                                                                                                             |
|  82891| 2017|lc   |ditadura |NA                                                                                                                             |
|  98027| 2018|ch   |ditadura |NA                                                                                                                             |
|  89028| 2018|lc   |ditadura |NA                                                                                                                             |





## Cálculo dos parâmetros das questões utilizando o modelo de 3 parâmetros da teoria da resposta ao ítem:

Em cada prova os alunos foram agrupados pela quantidade de acertos. Foram removidos grupos com menos de 50 alunos. Em grupos com menos de 500 candidatos, todos foram selecionados. Nos demais grupos, sortearam-se 500 alunos. Essa seleção foi feita para que se tivesse uma representação mais homogênea de alunos de diferentes habilidades do que ocorreria se simplesmente se sorteassem os candidatos.

Os itens foram calibrados com função [mirt](https://www.rdocumentation.org/packages/mirt/versions/1.34/topics/mirt) do pacote [mirt](https://www.rdocumentation.org/packages/mirt/versions/1.34) da linguagem de programação R. No caso de parâmetros não estão descritos aqui, foram utilizados os valores padrão da função.

* Utilizou-se o modelo de 3 parâmetros

    * As prioris de cada um dos parâmetros para todos os ítens foram:

        * parâmetro de discriminação

            * Distribuição: lnorm (log-normal)

            * Média log: 1,00

            * Desvio padrão log: 0.,5

        * parâmetro de dificuldade

            * Distribuição: norm (normal/Gaussiana)

            * Média: 0,00

            * Desvio Padrão: 1,00

        * parâmetro de acerto casual

            * Distribuição: expbeta (beta após aplicar a função plogis ao valor de entrada)

            * Alpha: 5

            * Beta: 17

* O limiar de convergência utilizado foi 0,001

* Média e desvio padrão da variável latente utilizados foram os mesmos observados na prova após a conversão da escala Enem. Ou seja, para obter a média da variável latente se utilizou a média das notas dos alunos da prova e se subtraiu 500. Depois, dividiu-se o valor obtido por 100. Já para obter o desvio padrão da variável latente se dividiu o desvio padrão das notas dos alunos da prova por 100.

## Identificando itens inadequados:


### Seleção de itens suspeitos de serem inadequados 

Para cada ítem se obteve os seguintes parâmetros a partir do modelo acima e da matriz dicotômica de resposta dos alunos:

* Correlação bisserial (utilizando a função [psych::biserial](https://search.r-project.org/CRAN/refmans/psych/html/tetrachor.html)) para identificar itens que tenham seu padrão de respostas pouco correlacionado com o resto da prova, o que indicaria que o item em questão não tem sua resposta correta claramente determinada pela proficiência aferida na área\*;

* Raiz quadrada média do erro de aproximação da estatística de ajuste de Bocks (utilizando a função [mirt::itemfit](https://rdrr.io/cran/mirt/man/itemfit.html))\*\* para verificar se o modelo utilizado está prevendo de forma satisfatória a probabilidade de acertos no item segundo proficiência do candidato;

* Coeficiente Crit (utilizando a função [mokken::check.monotonicity](https://rdrr.io/cran/mokken/man/check.monotonicity.html)) para identificar se em algum ponto da escala a probabilidade de acerto no item decresce quando a proficiência do candidato aumenta; 

* Parâmetro de Discriminação (utilizando a função [mirt::coef](https://rdrr.io/cran/mirt/man/coef-method.html)) para detectar itens com pouca capacidade de distinguir alunos segundo sua proeficiência;

\* No caso da correlação bisserial para comparar com achados anteriores, além da amostra homogênea citada acima também se usou um modelo com representação aleatória, com sorteio de 500 mil alunos de cada prova.

Itens que apresentaram correlação bisserial menor que 0.3,  raiz quadrada média do erro de aproximação da estatística de ajuste de Bocks maior que 0.05, coeficiente Crit maior que 80 ou parâmetro de discriminação menor que 0.34 foram selecionados como "suspeitos de serem inadequados".

### Classificação de item como inadequados 

Na literatura sobre o assunto é recomendado que os limiares que classificam os ítens sejam interpretados com cautela e que se faça uma análise das curvas de funções de respostas observada (com porcentagem de acerto no eixo Y e a proficiência no eixo X), junto com o enunciado e opções da questão para compreender se de fato há uma inadequação do item. Logo, essas questões tiveram suas curvas de funções de resposta ao item comparadas visualmente com o padrão de respostas empírico dos alunos,  agrupados em percentiles segundo suas notas para diagnosticar comportamentos claramente anormais que fogem do que seria esperado de uma questão com um padrão sigmóide monotônico (essas são as curvas dos gráficos presentes na reportagem). 

Dos 43 itens suspeitos de serem inadequados (que não passaram em algum filtro citado acima), somente 17 foram considerados claramente inadequados após essa inspeção. O único supostamente polêmico dentreesses 43 suspeitos não foi considerado inadequado. 
