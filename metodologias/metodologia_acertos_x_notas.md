# Material e métodos utilizados para a reportagem "No Enem, comece pelas mais fáceis"

A [reportagem](https://www1.folha.uol.com.br/educacao/2021/11/candidato-do-enem-comece-sempre-pelas-perguntas-faceis.shtml), feita a partir dos microdados do Enem, se baseia em um modelo estatístico que estima a chance de um candidato acertar uma questão dada a sua proficiência na prova. 

Para isso, foram calculados três parâmetros. São eles: parâmetro de discriminação (mede se a questão consegue diferenciar os candidatos de acordo com o nível de conhecimento naquele tema), parâmetro de dificuldade (indica o nível de dificuldade daquela questão) e parâmetro de acerto casual (estima a chance do candidato acertar porque chutou). 

Eles fazem parte da TRI (Teoria da Resposta ao Item) de 3 parâmetros, metodologia que o Inep utiliza para corrigir e dar nota aos candidatos. O órgão, contudo, não forneceu o valor dos parâmetros que são utilizados, e foi feito um cálculo próprio.

## Dados:

* As respostas e notas dos alunos foram obtidas a partir dos [microdados do Enem disponibilizados pelo Inep](https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados/enem)\*; 

* Foram analisadas somente as primeiras aplicações das provas de cada ano\*\*;

* A correspondência entre as questões e as respostas dos alunos presentes nos microdados foram feitas utilizando os arquivos  “itens_prova” de cada ano\*\*\*.

\* Dois alunos foram removidos porque apresentavam menos respostas do que seria o esperado. Aluno com ID 400000364244 de 2012 apresentava 40 respostas válidas na prova de linguagems e códigos (LC) e aluno com ID 100000703699 apresentava 44 respostas válidas na prova de LC em 2009. Em ambos casos eram esperadas 45 respostas válidas

\*\* Apesar de essa observação não estar presente no dicionário de dados, as provas com ID de 101 a 116 de 2010 são reaplicações;

\*\*\* A prova rosa de 2014 de linguagens e códigos (ID 198) apresenta ordenação errada no arquivo “itens_prova”, por isso para esse caso específico foi utilizada a ordem  [disponinilizada pelo curso objetivo](https://www.curso-objetivo.br/vestibular/resolucao_comentada/enem/enem2014_2dia.asp?img=01). Foi confirmada que essa ordem está correta, pois a ordenação das respotas corretas dela bate com a do gabarito presente nos microdados. 

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

## Dificuldade das questões:

A dificuldade dos itens foi estimada de duas formas:

1. Porcentagem do total de alunos que acertaram o item;
2. Parâmetro de dificuldade obtido utilizando a função [coef](https://www.rdocumentation.org/packages/mirt/versions/1.6.1/topics/coef-method) do pacote mirt da linguagem de programação R, utilizando o modelo definido acima.

## Gráfico na reportagem:

Nos gráficos estão representados os parâmetros de dificuldade (b) dos itens. Como alguns itens tiveram suas dificuldades estimadas em valores muito além da média dos demais, para facilitar a visualização da escala os valores de b foram truncados nos percentiles 5 e 95.

## Relação entre ordem das questões e a dificuldade:

Para verificar se a dificuldade está relacionada com a ordem que a questão ocorre na prova foi feita a análise a seguir.

1. Para cada prova de cada cor:

    a. Estimou-se o modelo (conforme descrito acima, mas separadamente para alunos que fizeram a prova de determinada cor);
    
    b. Extraiu-se o parâmetro de dificuldade (b) de cada item do modelo;
    
    c. Foi calculada a porcentagem de acerto de cada item (p), considerando todos os alunos;
    
    d. Foi ponderada a posição dos itens subtraindo a menor posição que o item aparece entre todas as provas (posicao ponderada). Se o mesmo item aparece nas posições 10, 20, 25 e 45, a posição ponderada dele será calculada subtraindo-se 10 (menor posição) desses valores. Assim, as posições ponderadas serão  0, 10, 15, 25 para o item nas diferentes prova.

    d. Calculou-se para cada item a distância entre os parâmetros b e p do item em menor posição, ou seja, a distância da dificuldade da prova em relação a quando o item apareceu na menor posição; 
    
2. Foi feita uma regressão linear entre a posição ponderada (item 1.c) e a distância das dificuldades (item 1.d). 

O coeficiente da posição relativa em função da distância do parâmetro p foi de -0.083 (±0.006; p-valor: < 2.2e-16), ou seja, a cada posição mais avançada do item a chance de acerto cai 0.08 pontos percentuais, e do parâmetro b foi de + 0.006 (± 0.0.0002; p-valor:2.2e-16). Assim, em ambos os casos há uma correlação entre posição mais posterior do item e aumento da dificuldade do item para os alunos.









