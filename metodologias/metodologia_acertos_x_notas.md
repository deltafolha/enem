# Material e métodos do artigo "No Enem, comece pelas mais fáceis"

A reportagem se baseia em um modelo estatístico que estima a chance de um candidato acertar uma questão dada a sua proficiência na prova. 

Para isso, foram calculados três parâmetros. São eles: parâmetro de discriminação (mede se a questão consegue diferenciar os candidatos de acordo com o nível de conhecimento naquele tema), parâmetro de dificuldade (indica o nível de dificuldade daquela questão) e parâmetro de acerto casual (estima a chance do candidato acertar porque chutou). 

Eles fazem parte da TRI (Teoria da Resposta ao Item) de 3 parâmetros, metodologia que o Inep utiliza para corrigir e dar nota aos candidatos. O órgão, contudo, não forneceu o valor dos parâmetros que são utilizados, mesmo quando solicitado pela reportagem via Lei de Acesso à Informação, sob a justificativa de que são dados sensíveis.

## Dados:

* As respostas e notas dos alunos foram obtidas a partir dos microdados do Enem disponibilizados pelo Inep\*; 
* Foram analisadas somente as primeiras aplicações das provas de cada ano\*\*;
* A correspondência entre as questões e as respostas dos alunos  presentes nos microdados foram feitas utilizando os arquivos  “itens_prova” de cada ano\*\*\*.

\* Dois alunos foram removidos porque apresentavam menos respostas do que seria o esperado (aluno com ID 400000364244 de 2012 apresentava 40 respostas válidas na prova de LC e aluno com ID 100000703699 apresentava 44 respostas válidas na prova de LC em 2009. Em ambos casos eram esperadas 45 respostas válidas)

\*\* Apesar dessa observação não estar presente no dicionário de dados, as provas com ID 101 até 116 de 2010 são reaplicaçõe;.

\*\*\* A prova rosa de 2014 de linguagens e códigos (ID 198) apresenta ordenação errada no arquivo “itens_prova”, por isso para esse caso específico foi utilizada a ordem disponível pelo curso objetivo aqui.

## Cálculo dos parâmetros das questões utilizando o modelo de 3 parâmetros da teoria da resposta ao ítem:

Em cada prova os alunos foram agrupados pela quantidade de acertos. Foram removidos grupos com menos de 50 alunos. Em grupos com menos de 500 alunos todos os alunos foram selecionados, nos demais grupos se sorteou 500 alunos. Essa seleção foi feita para que tenha uma representação mais homogênea de alunos de diferentes habilidades do que ocorreria se simplesmente se sorteassem os alunos.

Os itens foram calibrados com função mirt do pacote mirt da linguagem de programação R. Os parâmetros que não estão descritos aqui é porque foram utilizados os valores padrões da função.

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

## Dificuldade das questões:

A dificuldade dos itens foram estimadas de duas formas:

1. Porcentagem do total de alunos que acertaram o item;
2. Parâmetro de dificuldade obtido utilizando a função coef do pacote mirt da linguagem de programação R, utilizando o modelo definido acima.

## Gráfico na reportagem:

Nos gráficos estão representados os parâmetros de dificuldade (b) dos itens. Como alguns itens tiveram suas dificuldades estimadas em valores muito além da médias dos demais, para facilitar a visualização da escala os valores de b foram truncados nos percentiles 5 e 95.

## Relação entre ordem das questões e a dificuldade:

Para verificar se a dificuldade está relacionada com a ordem que a questão ocorre na prova se fez a seguinte análise:

1. para cada conjunto de cada prova de cada área em cada ano se:
* Estimou o modelo (conforme descrito acima, mas dessa vez considerando somente alunos que fizeram a prova de determinada cor);
* Extraiu o parâmetro de dificuldade (b) de cada item do modelo;
* Calculou a porcentagem de acerto de cada item (p), considerando todos os alunos;
Ponderou a posição dos itens subtraindo a menor posição que o item aparece entre todas as provas (posicao ponderada).. Assim, se o mesmo item aparece nas posições 10, 20, 25 e 45, a posição ponderada dele calculada será calculada subtraindo-se 10 (menor posição) e o ítem terá esses valores de 0, 10, 15, 25 para cada prova.
* Calculou para cada item a distância entre os parâmetros b e p  do item em menor posição, ou seja, a distância da dificuldade desta prova em relação a quando o item apareceu em outra posição; 
3. Se fez uma regressão entre a posição ponderada e a distância das dificuldades. 

O coeficiente da posição relativa em função da distância do parâmetro p em função foi de -0.083 (±0.006; p-valor: < 2.2e-16), ou seja a cada posição mais avançada do item a chance de acerto cai 0.08 pontos percentuais, e do parâmetro b foi de + 0.006 (± 0.0.0002; p-valor:2.2e-16). Assim, em ambos casos há uma correlação entre posição mais posterior do item e aumento da dificuldade do item para os alunos.







