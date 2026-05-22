Integridade:

* Conceito fundamental: Correção, consistência e segurança dos dados. Estão associadas aos conceitos de chave de acesso. Garantem o acesso individualizado a todas as ocorrências de uma tabela. Garantem que os relacionamentos estejam válidos e condizentes com a realidade.



* PK (Chave-Primária): Faz com que a tabela seja ordenada por ela automaticamente e não permite duplicidade em seu valor. Mantem a unicidade dos dados. Deve-se eleger um campo que nunca se repete.



* UK (Unique-Key): Além da PK uma tabela pode possuir quantas UK's forem necessárias. Garante que não serão inseridos dados duplicados em colunas que não são PK.



* SK (Secondary-keys): Chave auxiliar de acesso a uma tabela. Também possuem índices relacionados utilizados em campos onde se efetuam muitas pesquisas ou acesso. Não precisam necessariamente ser UK's.



* FK (Foreign-keys): Permite acesso e validação de outras tabelas. Deve ser compatível em tipo e tamanho com sua PK correspondente na tabela de origem.







Normalização:

Organizar as tabelas de modo que sua estrutura seja simples, relacional e estável. O Objetivo é evitar perdas e a repetição de informação, apresentando e armazenando os dados adequadamente. Melhora a estrutura dos dados e evita problemas de redundância e avarias de atualização. É um processo sistemático de aplicação de regras que vão da 1ª FN(Forma normal) à 5ª FN, mas na grande maioria dos casos a aplicação da 3ª FN já é o suficiente.



* 1ªFN: Exige que uma tabela não tenha aninhamentos (Atributos repetitivos).



* Nivelamento: A PK da tabela é formada pelas PK's de cada tabela adjacente. Caso existam atributos multivalorados, estes devem se tornar componentes da PK. Se existir aninhamento, provavelmente este 1ªFN não é o estado final do Schema. Uma tabela esta na 1ª FN se nenhum de seus atributos possui domínio multivalorado, ou seja, devemos eliminar itens repetitivos.



* EX:

|NOTA\_FISCAL|
|-|
|NR\_NOTA<br />NM\_CLIENTE<br />NM\_VENDEDOR<br />PRODUTO\_A<br />PRODUTO\_B<br />PRODUTO\_C|

|NOTA\_FISCAL|ITEM\_NOTA||
|-|-|-|
|NR\_NOTA<br />NM\_CLIENTE<br />NM\_VENDEDOR|NR\_NOTA<br />CD\_PRODUTO<br />DESC\_PRODUTO<br />VALOR||



* 2ª FN: Exige o entendimento do conceito de DF (Dependência Funcional). Existe DF em uma tabela que sempre tem um conjunto de um ou mais atributos determinando o valor de outro conjunto  de um ou mais atributos. É possível perceber isto analisando dados de arquivos e relatórios de uma organização. Uma tabela está na 2ª FN se e somente se estiver na primeira forma normal e todo atributo não chave depende funcionalmente de toda a PK e não apenas de parte dela. Deve existir DF da PK por completo. Cada atributo não chave deve ser analisado e se identificado DF de parte da PK, gera-se uma tabela que tenha o atributo não chave e parte da PK (que agora é uma PK completa). A 2ª FN é o caso da tabela de produtos onde o atributo determinante mais os outros que dependem apenas dele (Nome) foram movidos de NOTA e depois de ITEM\_NOTA para PRODUTO compondo a PK composta em ITEM\_NOTA.





* 3ª FN: Cada tabela esta na 3FN se e somente se todo atributo não-chave depende funcional e diretamente da PK, e não de um conjunto de um ou mais atributos não-chave. Desta forma todo atributo não chave deve ser analisado em relação a outros atributos não chave. Apenas tabelas com mais de um atributo não chave são consideradas, para efeito de analise da 3FN. Caso perceba-se uma DF (Dependência funcional) indireta, uma nova tabela é gerada, onde os atributos não-chave que determinam outros tornam-se PK e os atributos com DF indireta dele migram para ela como atributos não-chave. Na tabela antiga os atributos determinantes tornam-se FK's. Desta forma, uma tabela esta na 3FN quando esta na 2FN e não há dependência funcional transitiva entre seus atributos. O objetivo é separar subconjuntos incertos em um super-conjunto e evitar redundância nas informações. Além da repetição dos dados, a possibilidade da deterioração da qualidade das informações amenta muito.



* EX:

|NOTA\_FISCAL|CLIENTE|VENDEDOR|ITEM\_NOTA|PRODUTO|
|-|-|-|-|-|
|NR\_NOTA<br />COD\_CLIENTE<br />COD\_VENDEDOR<br />DR\_EMISSAO<br />VAL\_TOTAL|COD\_CLIENTE<br />NM\_CLIENTE<br />END\_CLIENTE|COD\_VENDEDOR<br />NM\_VENDEDOR|NR\_NOTA<br />COD\_PRODUTO<br />QTD\_PRODUTO<br />VL\_PRECO<br />VL\_TOTAL|COD\_PRODUTO<br />DESC\_PRODUTO<br />UND\_MED<br />VL\_PRODUTO|





.

