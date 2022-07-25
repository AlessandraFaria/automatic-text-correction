# automatic-text-correction
Recognition of frequent patterns in a textual database

**Neste repositório pretende-se apresentar uma solução autocorreção utilizando a linguagem de programação python, com o objetivo de analisar a eficiência do reconhecimento de padrões ortográficos dentro das tecnologias propostas pela linguagem.**

Comumentemente usuários de smartphones utilizam o recurso de correção automática do texto digitado. Atualmente quase todas as marcas ,fornecedoras de smartphones, fornecem um ou mais recursos de correção automática em seus teclados.
Dentro do contexto do aprendizado de máquina, a  correção automática do texto (auto correção) é baseada no processamento natural da linguagem em que  é programado para corrigir ortografias e erros durante a digitação do usuário.


## Base de dados
Atualmente os algoritmos de autocorreção presentes nos smartphones utilizam o contexto histórico das palavras digitadas pelo usuário ou seja, palavras e jargões comumentemente utilizados possuem maior peso quando o algoritmo busca a correção. Visando simular tal situação, a base de dados escolhida encontra-se no mesmo contexto.

A base é composta por pelo primeiro capítulo do livro Moby Dick; or The Whale na versão lançada dia vinte e cinco de dezembro de 2008 em inglês, esse capítulo possui: 1238242 caracteres, 222666 palavras e 22333 linhas. 

A base de dados não possui dados nulos, os dados são completos de modo que nenhuma palavra está escrita em parte ou fora de um contexto maior. Todas as palavras fazem parte do mesmo contexto e foram elaboradas pelo mesmo autor. Deste modo, todas as palavras levantadas na amostra serão utilizadas juntamente com as suas respectivas frequências.

## Metodologia
![image](https://user-images.githubusercontent.com/14276167/180791958-ed3be6b7-3d2d-4fc0-a10b-6bd4b2cbf79a.png)

A exploração dos dados brutos foi realizada utilizando a linguagem de programação python com as bibliotecas Pandas e Nump. Primeiramente, com o objetivo de analisar a frequência, identificou-se a quantidade de vezes em que cada palavra aparece na base de dados, ordenando de forma crescente a frequência identificada. Pode-se observar como amostra do resultado a seguinte sequência: 

('this', 1439), ('at', 1335), ('whale', 1230), ('by', 1222), ('not',    1173), ('from', 1104), ('on', 1073) 

O levantamento da frequencia relativa de palavras permite obter a probabilidade de cada palavra. Este levantamento foi realizado dividindo cada palavra, distinta, pelo número de palavras distintas na base.

O algoritmo de mineração de padrões frequentes foi aplicado buscando palavras semelhantes na base de dados usando como método a distância de jaccard. Como parâmetro do método foi utilizado o valor de 2 QVal. Além disso, a palavra a ser buscada foi pesquisada seguindo a ordem de frequência, ou seja  começando pelas palavras de maior probabilidade. 

Como modelo resultado o método exibe de forma ordenada, por semelhança e probabilidade, as cinco palavras que podem corresponder a palavra que deseja ser escrita pelo usuário. A figura abaixo exemplifica o resultado obtido ao escrever de forma errada a palavra Moby. é possível visualizar as palavras que possuem o mesmo padrão que a palavra digitada. 

![image](https://user-images.githubusercontent.com/14276167/180792201-ae8aa915-b6a3-4978-bf6a-f35db56989b8.png)

## Avaliação dos resultados
Com o objetivo de avaliar a eficiência de pesquisa da palavra correta pelo coeﬁcientes de Jaccard estendidos, um conjunto de experimentos foi realizado. Seis palavras com frequências distintas na base foram separadas e manipuladas para serem utilizadas como dado de entrada. As manipulações realizadas foram: extrair as duas primeiras palavras; substituir uma letra por outra e substituir duas letras por outras duas. O critério de avaliação é a quantidade de vezes que a palavra alvo foi corrigida corretamente.

O  resultado da execução do modelo com as palavras manipuladas pode ser visualizado na Figura Abaixo.
![image](https://user-images.githubusercontent.com/14276167/180792385-87ef3754-a244-43db-8c93-926cee99d3dd.png)

A figura abaixo demarca, em verde, todas as vezes que a palavra alvo foi corrigida automaticamente, é possível deduzir o grande impacto no resultado, de pequenas alterações na palavra.

![image](https://user-images.githubusercontent.com/14276167/180792475-bcee533e-24ea-4adf-a5f3-1d8226d91f58.png)

## Resultados
O processo de mineração de dados utilizado foi o de reconhecimento de padrões frequentes para autocorreção da ortografia de palavras nele a frequência das palavras na base de dados foi levantada é utilizada como parâmetro em um método que utilizava o índice de jaccard para retornar a palavra correta a ser escrita. O trabalho foi executado na linguagem de programação Python de forma otimizada.

Ao obter-se os resultados algumas falhas foram evidenciadas. O primeiro teste consistiu em buscar a correção da palavra utilizando somente as duas primeiras letras dela na busca, como resultado somente a palavra que era composta por três letras foi encontrada, tendo assim 16% de acerto. No segundo teste a palavra correta foi buscada alterando, somente, uma letra, observou-se que quando a palavra THE foi buscada alterando-a para THER o método entendeu que por ter um número de letras maior, se tratava de outra palavra, no caso THERE, nos outros casos de teste as palavras foram encontradas, tendo assim 83% de acerto na busca. O terceiro e último teste consistiu em modificar mais a estrutura da palavra, alterando  duas letras da sua ortografia, nessa situação três casos não foram identificados corretamente na busca pois o método encontrou palavras semelhantes que consideram a alteração como original da palavra, tendo assim 50% de acerto no objetivo do teste.

Conclui-se com os testes realizados que o método é eficiente na busca das palavras semelhantes mas deve-se ressaltar que dependendo do erro ortográfico digitado o método pode presumir que a palavra a ser buscada é outra.  


