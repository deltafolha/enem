# Material e métodos da reportagem ["Questões inadequadas compõem 2% do Enem e não contam para nota"](https://www1.folha.uol.com.br/educacao/2021/11/questoes-inadequadas-compoem-2-do-enem-e-nao-contam-para-nota.shtml)

A reportagem, feita a partir dos microdados do Enem, se baseia em um modelo estatístico que estima a chance de um candidato acertar uma questão dada a sua proficiência na prova.

Para isso, foram calculados três parâmetros. São eles: parâmetro de discriminação (mede se a questão consegue diferenciar os candidatos de acordo com o nível de conhecimento naquele tema), parâmetro de dificuldade (indica o nível de dificuldade daquela questão) e parâmetro de acerto casual (estima a chance do candidato acertar porque chutou). 

Eles fazem parte da TRI (Teoria da Resposta ao Item) de três parâmetros, metodologia que o Inep utiliza para corrigir e dar nota aos candidatos. O órgão, contudo, não forneceu o valor dos parâmetros que são utilizados, e foi feito um cálculo próprio.


## Dados:

* As respostas e notas dos alunos foram obtidas a partir dos [microdados do Enem disponibilizados pelo Inep](https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados/enem)\*; 

* Foram analisadas somente as primeiras aplicações das provas de cada ano\*\*;

* A correspondência entre as questões e as respostas dos alunos presentes nos microdados foram feitas utilizando os arquivos  “itens_prova” de cada ano\*\*\*.

\* Dois alunos foram removidos porque apresentavam menos respostas do que seria o esperado (aluno com ID 400000364244 de 2012 apresentava 40 respostas válidas na prova de LC e aluno com ID 100000703699 apresentava 44 respostas válidas na prova de LC em 2009. Em ambos casos eram esperadas 45 respostas válidas)

\*\* Apesar de essa observação não estar presente no dicionário de dados, as provas com ID de 101 a 116 de 2010 são reaplicações;

\*\*\* A prova rosa de 2014 de linguagens e códigos (ID 198) apresenta ordenação errada no arquivo “itens_prova”, por isso para esse caso específico foi utilizada a ordem  [disponinilizada pelo curso Objetivo](https://www.curso-objetivo.br/vestibular/resolucao_comentada/enem/enem2014_2dia.asp?img=01). Foi confirmada que essa ordem está correta, pois a ordenação das respotas corretas dela bate com a do gabarito presente nos microdados. 




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

\* No caso da correlação bisserial, além da amostra homogênea citada acima também se usou um modelo com representação aleatória, com sorteio de 500 mil alunos de cada prova. Essa análise só foi utilizada para testar itens que não tiveram seus acertos ponderados. Isso foi feito pois se considerou que o Enem pode usar essa amostragem em uma calibragem após a prova. 

Itens que apresentaram correlação bisserial menor que 0.3,  raiz quadrada média do erro de aproximação da estatística de ajuste de Bocks maior que 0.05, coeficiente Crit maior que 80 ou parâmetro de discriminação menor que 0.34 foram selecionados como "suspeitos de serem inadequados".


### Classificação de item como inadequados 

Na literatura sobre o assunto é recomendado que os limiares que classificam os ítens sejam interpretados com cautela e que se faça uma análise das curvas de funções de respostas observada (com porcentagem de acerto no eixo Y e a proficiência no eixo X), junto com o enunciado e opções da questão para compreender se de fato há uma inadequação do item. Logo, essas questões tiveram suas curvas de funções de resposta ao item comparadas visualmente com o padrão de respostas empírico dos alunos,  agrupados em percentiles segundo suas notas para diagnosticar comportamentos claramente anormais que fogem do que seria esperado de uma questão com um padrão sigmóide monotônico (essas são as curvas dos gráficos presentes na reportagem). 

Dos 185 itens suspeitos de serem inadequados (que não passaram em algum filtro citado acima), somente 30 foram considerados claramente inadequados após essa inspeção. 

### Itens em que há forte evidências de terem tido peso zerado para quem acertou mais de uma resposta


Para cada item suspeito de ser inadequado se:

* Selecionou a matriz dicotômica de resposta da prova que o item pertence;
* Excluiu o item da matriz dicotômica de resposta;
* Se selecionou alunos que acertaram pelo menos um item (sem contar o item em questão);
* Agrupou os alunos que tinham o mesmo padrão de respostas nos itens restantes;
* Verificou se dentro de cada grupo acima os alunos que acertaram ou erraram o item em questão tinham a mesma nota final.
 
Ou seja, para os mesmos padrões de respostas (excetuando o item em questão) se verificou que acertar ou errar o item não levava a nenhum acréscimo da nota final.

A quantidade de padrões idênticos analisados variou de 1.341 a 58.210 (depedendo do item em questão). Esses padrões abrangem diferentes quantidades de acertos, logo de habilidades. 

Dos 30 itens considerados claramente inadequados, identificamos que 21 não tiveram o acerto considerado (70%). Isso demonstra que houve a identificação pelo modelo do INEP que estes itens tinham baixíssima capacidade de discriminação. Também se observou que outros 11 itens que eram "suspeitos de serem inadequados” não haviam sido considerados na pontuação. Esses foram também classificados como inadequados, totalizando 41 itens inadequados. Foi considerado que esses itens inadequados, uma vez que aparentemente o próprio modelo do Enem identificou que eles não estariam fornecendo informação sobre a proficiência do aluno. 


# Resultados

(Link para a tabela com os parâmetrosd e classificações dos itens.)[https://github.com/deltafolha/enem/blob/main/metodologias/indices_fits.csv]

Descrição das colunas:

* *id*: Identificador do item utilizado nos microdados do Enem

* *ano:* Ano da prova

* *area*: Área da prova

* *posicao_provaAzul*: Ordem da questão na área na prova azul

* *RMSEA.X2*: resultado da raiz quadrada média do erro de aproximação da estatística de ajuste de Bocks

* *crit*: Coeficiente Crit

* *a*: Parâmetro de Discriminação

* *bc_homogenea*: Correlação bisserial considerando o modelo com distribuição homogênea

* *bc_aleatoria*: Correlação bisserial considerando o modelo com distribuição aleatória

* *flag_<indice>*: Se o item não passou no teste em questão (1 = não passou)

* *flag_polemica*: Se o item foi identificado como polêmico (análise da matéria anterior)

* *flag_suspeito_1*: Se o item não passou em nos critérios, com exceção do _bc_aleatoria_

* *flag_suspeito_2*: Se o item não passou em nenhum critério

* *flag_inadequado_1*: Se após inspeção da curva empírica de função do item se identificou que o item era inadequado

* *flag_nao_contou*: Se em nenhuma combinação de respostas foi verificado um acréscimo de nota;

* *flag_inadequado_1*: Itens _flag_inadequado_1_ + _flag_nao_contou_


(Link para pasta com todos os gráficos da análise dos itens "suspeitos de serem inadequados".)[https://github.com/deltafolha/enem/tree/main/metodologias/graficos_fit_itens]

