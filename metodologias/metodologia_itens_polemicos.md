# Material e métodos do artigo "XXXXXXXXXXXXXXXXXXXX"

A reportagem se baseia em um modelo estatístico que estima a chance de um candidato acertar uma questão dada a sua proficiência na prova. 

Para isso, foram calculados três parâmetros. São eles: parâmetro de discriminação (mede se a questão consegue diferenciar os candidatos de acordo com o nível de conhecimento naquele tema), parâmetro de dificuldade (indica o nível de dificuldade daquela questão) e parâmetro de acerto casual (estima a chance do candidato acertar porque chutou). 

Eles fazem parte da TRI (Teoria da Resposta ao Item) de 3 parâmetros, metodologia que o Inep utiliza para corrigir e dar nota aos candidatos. O órgão, contudo, não forneceu o valor dos parâmetros que são utilizados, mesmo quando solicitado pela reportagem via Lei de Acesso à Informação, sob a justificativa de que são dados sensíveis.

## Dados:

* As respostas e notas dos alunos foram obtidas a partir dos [microdados do Enem disponibilizados pelo Inep](https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados/enem)\*; 

* Foram analisadas somente as primeiras aplicações das provas de cada ano\*\*;

* A correspondência entre as questões e as respostas dos alunos  presentes nos microdados foram feitas utilizando os arquivos  “itens_prova” de cada ano\*\*\*.

* Como os itens supostamente polêmicos estavam todos nas provas de linguagem e ciências humanas, somente essas provas analisadas. No caso de linguagens se removeu os ites de inglês e espanhol, já que são os mesmos para todos os alunos. 

\* Dois alunos foram removidos porque apresentavam menos respostas do que seria o esperado (aluno com ID 400000364244 de 2012 apresentava 40 respostas válidas na prova de LC e aluno com ID 100000703699 apresentava 44 respostas válidas na prova de LC em 2009. Em ambos casos eram esperadas 45 respostas válidas)

\*\* Apesar dessa observação não estar presente no dicionário de dados, as provas com ID 101 até 116 de 2010 são reaplicaçõe;.

\*\*\* A prova rosa de 2014 de linguagens e códigos (ID 198) apresenta ordenação errada no arquivo “itens_prova”, por isso para esse caso específico foi utilizada a ordem disponível pelo curso objetivo [aqui](https://www.curso-objetivo.br/vestibular/resolucao_comentada/enem/enem2014_2dia.asp?img=01). Foi confirmada que essa ordem está correta, pois a ordenação das respotas corretas dela bate com a do gabarito presente nos microdados. 

## Cálculo dos parâmetros das questões utilizando o modelo de 3 parâmetros da teoria da resposta ao ítem:

Em cada prova os alunos foram agrupados pela quantidade de acertos. Foram removidos grupos com menos de 50 alunos. Em grupos com menos de 500 alunos todos os alunos foram selecionados, nos demais grupos se sorteou 500 alunos. Essa seleção foi feita para que tenha uma representação mais homogênea de alunos de diferentes habilidades do que ocorreria se simplesmente se sorteassem os alunos.

Os itens foram calibrados com função [mirt](https://www.rdocumentation.org/packages/mirt/versions/1.34/topics/mirt) do pacote [mirt](https://www.rdocumentation.org/packages/mirt/versions/1.34) da linguagem de programação R. Os parâmetros que não estão descritos aqui é porque foram utilizados os valores padrões da função.

* Se utilizou o modelo de 3 parâmetros

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

* Média e desvio padrão da variável latente utilizada foram as mesmas observadas na prova após a conversão da escala Enem. Ou seja, para obter a média da variável latente se utilizou a média das notas dos alunos da prova e se subtraiu 500 e depois se dividiu o valor obtido por 100. Já para se obter o desvio padrão da variável latente se dividiu o desvio padrão das notas dos alunos da prova por 100.

## Identificando itens inadequados:


### Seleção de itens suspeitos a serem inadequados 

Para cada ítem se obteve os seguintes parâmetros a partir do modelo obtidos acima e da matriz dicotômica de resposta dos alunos:

* Correlação bisserial (utilizando a função [psych::biserial](https://search.r-project.org/CRAN/refmans/psych/html/tetrachor.html)) para se identificar itens que tenham seu padrão de respostas pouco correlacionado com o resto da prova, o que indicaria que o item em questão não tem sua resposta correta claramente determinada pela proficiência aferida na área\*;

* Raiz quadrada média do erro de aproximação da estatística de ajuste de Bocks (utilizando a função [mirt::itemfit](https://rdrr.io/cran/mirt/man/itemfit.html))\*\* para verificar se o modelo utilizado está prevendo de forma satisfatória a probabilidade de acertos no item segundo proficiência do candidato;

* Coeficiente Crit (utilizando a função [mokken::check.monotonicity](https://rdrr.io/cran/mokken/man/check.monotonicity.html)) para identificar se em algum ponto da escala a probabilidade de acerto no item decresce quando a proficiência do candidato aumenta; 

* Parâmetro de Discriminação (utilizando a função [mirt::coef](https://rdrr.io/cran/mirt/man/coef-method.html)) para detectar itens com pouca capacidade de distinguir alunos segundo sua proeficiência;

\* No caso da correlação bisserial para comparar com achados anteriores, além da amostra homogênea citada acima também se usou um modelo com representação aleatória, onde se sorteou 500 mil alunos de cada prova.

Itens que apresentaram: correlação bisserial menor que 0.3,  raiz quadrada média do erro de aproximação da estatística de ajuste de Bocks maior que 0.05, coeficiente Crit maior que 80 ou parâmetro de discriminação menor que 0.34 foram selecionados como "suspeitos de serem inadequados".

### Classificação de item como inadequados 

Na literatura da área é sempre recomendado que esses limiares que classificam os ítens sejam interpretados com cautela e que se faça uma análise de suas curvas de funções de respostas observada (onde se coloca porcentagem de acerto no eixo Y e a proficiência no eixo X) junto com o enunciado e opções da questão para compreender se de fato há uma inadequação do item. Logo, esses itens tiveram suas curvas de funções de resposta ao item comparadas visualmente com o padrão de respostas empírico dos alunos.  agrupados em percentiles segundo suas notas para diagnosticar comportamentos claramente anormais que fogem do que seria esperado de uma questão com um padrão sigmóide monotônico (essas são as curvas dos gráficos presentes na matéria). 

Dos 43 itens suspeitos de serem inadequados (que não passaram em algum filtro citado acima), somente 17 foram considerados claramente inadequados após essa inspeção, o único polêmico não foi considerado. 
