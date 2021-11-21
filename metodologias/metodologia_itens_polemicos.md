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

|     id|area |  ano| posicao_provaAzul|link_questao                                                                                                                                                                      |tipo     |link_critica                                                                                                                   |
|------:|:----|----:|-----------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------|:------------------------------------------------------------------------------------------------------------------------------|
|  68887|ch   | 2014|                33|[link](https://descomplica.com.br/gabarito-enem/questoes/2014/primeiro-dia/existe-uma-cultura-politica-que-domina-o-sistema-e-e-fundamental-para-entender-o-conservadorismo/)     |critica  |[link](https://oglobo.globo.com/brasil/educacao/academicos-atacam-doutrinacao-do-enem-14546063)                                |
|  14258|ch   | 2015|                29|[link](https://descomplica.com.br/gabarito-enem/questoes/2009/segundo-dia/considerando-se-os-textos-apresentados-e-o-contexto-politico-e-social-no-qual-foi-produzida-obra/)      |critica  |[link](https://oglobo.globo.com/brasil/educacao/especialistas-se-dividem-sobre-doutrinacao-em-prova-do-enem-17909168)          |
|  38029|ch   | 2015|                42|[link](https://descomplica.com.br/gabarito-enem/questoes/2015/primeiro-dia/ninguem-nasce-mulher-torna-se-mulher-nenhum-destino-biologico-psiquico-economico-define-a-forma/)      |critica  |[link](http://g1.globo.com/educacao/enem/2015/noticia/2015/10/deputados-bolsonaro-e-feliciano-acusam-enem-de-doutrinacao.html) |
| 112076|lc   | 2018|                20|[link](https://descomplica.com.br/gabarito-enem/questoes/2018/primeiro-dia/situacao-narrada-revela-uma-tensao-fundamentada-na-perspectiva/)                                       |critica  |[link](https://twitter.com/francischini_/status/1059265756339363840?lang=en)                                                   |
| 112113|lc   | 2018|                37|[link](https://descomplica.com.br/gabarito-enem/questoes/2018/primeiro-dia/da-perspectiva-usuario-o-pajuba-ganha-status-de-dialeto-caracterizando-se-como-elemento-de-patr/)      |critica  |NA                                                                                                                             |
|  60218|lc   | 2009|                43|[link](https://descomplica.com.br/gabarito-enem/questoes/2009/segundo-dia/considerando-se-os-textos-apresentados-e-o-contexto-politico-e-social-no-qual-foi-produzida-obra/)      |ditadura |NA                                                                                                                             |
|  60220|lc   | 2009|                42|[link](https://descomplica.com.br/gabarito-enem/questoes/2009/segundo-dia/texto-ja-foi-o-tempo-em-que-via-convivencia-como-viavel-exigindo-deste-bem/)                            |ditadura |NA                                                                                                                             |
|  70736|ch   | 2010|                35|[link](https://descomplica.com.br/gabarito-enem/questoes/2010/primeiro-dia/opiniao-podem-prender-podem-bater-podem-ate-deixar-sem-comer-que-eu-nao-mudo-de-opiniao/)              |ditadura |NA                                                                                                                             |
|  70778|ch   | 2010|                33|[link](https://descomplica.com.br/gabarito-enem/questoes/2010/primeiro-dia/nao-e-dificil-entender-o-que-ocorreu-no-brasil-nos-anos-imediatamente-anteriores-ao-golpe-militar-de/) |ditadura |NA                                                                                                                             |
|  75440|ch   | 2011|                42|[link](https://descomplica.com.br/gabarito-enem/questoes/2011/primeiro-dia/em-meio-turbulencias-vividas-na-primeira-metade-dos-anos-1960-tinha-se-impressao-de-que-ten/)          |ditadura |NA                                                                                                                             |
|   7589|ch   | 2012|                15|[link](https://descomplica.com.br/gabarito-enem/questoes/2012/primeiro-dia/diante-dessas-inconsistencias-e-de-outras-que-ainda-preocupam-opiniao-publica-nos-jornalistas/)        |ditadura |NA                                                                                                                             |
|  13273|lc   | 2012|                36|[link](https://descomplica.com.br/gabarito-enem/questoes/2012/segundo-dia/logia-e-mitologia-meu-coracao-de-mil-e-novecentos-e-setenta-e-dois-ja-nao-palpita-fagueiro-sabe-que/)   |ditadura |NA                                                                                                                             |
|   8604|ch   | 2013|                20|[link](https://descomplica.com.br/gabarito-enem/questoes/2013/primeiro-dia/a-imagem-foi-publicada-no-jornal-correio-da-manha-no-dia-de-finados-de-1965/)                          |ditadura |NA                                                                                                                             |
|  24456|ch   | 2014|                28|[link](https://descomplica.com.br/gabarito-enem/questoes/2014/primeiro-dia/a-comissao-nacional-da-verdade-cnv-reuniu-representantes-de-comissoes-estaduais-e-de-varias/)          |ditadura |NA                                                                                                                             |
|  68434|ch   | 2014|                42|[link](https://descomplica.com.br/gabarito-enem/questoes/2014/primeiro-dia/o-presidente-do-jornal-de-maior-circulacao-do-pais-destacava-tambem-os-avancos-economicos-obtidos/)    |ditadura |NA                                                                                                                             |
|  24576|ch   | 2015|                19|[link](https://descomplica.com.br/gabarito-enem/questoes/2015/primeiro-dia/no-periodo-de-1964-a-1985-a-estrategia-do-regime-militar-abordada-na-charge-foi-caracterizada-pela/)   |ditadura |NA                                                                                                                             |
|  82324|lc   | 2015|                39|[link](https://descomplica.com.br/gabarito-enem/questoes/2015/segundo-dia/situado-na-vigencia-do-regime-militar-que-governou-o-brasil-na-decada-de-1970/)                         |ditadura |NA                                                                                                                             |
|  86985|ch   | 2016|                 2|[link](https://descomplica.com.br/gabarito-enem/questoes/2016/primeiro-dia/batizado-por-tancredo-neves-de-nova-republica/)                                                        |ditadura |NA                                                                                                                             |
|  97744|ch   | 2016|                13|[link](https://descomplica.com.br/gabarito-enem/questoes/2016/primeiro-dia/a-operacao-condor-esta-diretamente-vinculada-as-experiencias-historicas/)                              |ditadura |NA                                                                                                                             |
|  24935|ch   | 2017|                38|[link](https://descomplica.com.br/gabarito-enem/questoes/2017/primeiro-dia/no-periodo-anterior-ao-golpe-militar-de-1964-os-documentos-episcopais-indicavam-para-os-bispos-que/)   |ditadura |NA                                                                                                                             |
|  77759|lc   | 2017|                25|[link](https://descomplica.com.br/gabarito-enem/questoes/2017/primeiro-dia/uma-noite-em-67-mas-foi-uma-noite-aquela-noite-de-sabado-21-de-outubro-de-1967/)                       |ditadura |NA                                                                                                                             |
|  82891|lc   | 2017|                24|[link](https://descomplica.com.br/gabarito-enem/questoes/2017/primeiro-dia/e-aqui-antes-de-continuar-este-espetaculo-e-necessario-que-facamos/)                                   |ditadura |NA                                                                                                                             |
|  98027|ch   | 2018|                24|[link](https://descomplica.com.br/gabarito-enem/questoes/2018/primeiro-dia/no-referido-texto-historico-manifestacao-cartunista-henfill-expressava-uma-critica-aoa/)               |ditadura |NA                                                                                                                             |
|  89028|lc   | 2018|                42|[link](https://descomplica.com.br/gabarito-enem/questoes/2018/primeiro-dia/publicado-em-1979-o-texto-compartilha-com-outras-obras-da-literatura-brasileira-escritas-no-periodo/)  |ditadura |NA                                                                                                                             |





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

Dos 43 itens suspeitos de serem inadequados (que não passaram em algum filtro citado acima), somente 17 foram considerados claramente inadequados após essa inspeção. O único supostamente polêmico dentre esses 43 suspeitos não foi considerado claramente inadequado, pois ainda que sua curva não seja claramente uma sigmóide, pois tem duas regiões de "subida" com um plateau entre elas, o que explica ela ter sido detectada pelo RMSE.X2 como inadequada, ela possui uma clara tendência de subida. 

Aqui a função de respostas observada (bolas) e a previsão do modelo na questão. 
![fig_1](https://user-images.githubusercontent.com/94707416/142745070-3672ad75-5892-4849-9c42-6f35639d1fd0.png)

Aqui a função de respostas observada de uma questão que foi diagnosticada como claramente inadequada. 
![fig_2](https://user-images.githubusercontent.com/94707416/142745075-cba680ec-cda2-4e6f-b24e-3bb032d3763c.png)


