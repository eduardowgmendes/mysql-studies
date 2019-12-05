## Definição de Dados
Antes de criar as tabelas no nosso banco de dados, temos que definir quais as características de cada um dos campos. As características que o SQL exige são o tipo de dado e o tamanho de cada campo. Apresentaremos o padrão utilizado pela maioria dos bancos de dados SQL e você deverá consultar as eventuais mudanças do banco de dados em que estiver trabalhando.

Tipo de Dado | Descrição 
-------------|----------
`INTEGER` ou `INT` | Número positivo ou negativo inteiro. 
`SMALLINT` | Mesma função do `INTEGER`, mas ocupa cerca da metade do espaço.
`NUMERIC` | Número positivo ou negativo de ponto flutuante.
`DECIMAL` | Semelhante ao `NUMERIC`. 
`REAL` | Número de ponto flutuante de simples precisão.
`DOUBLE PRECISION` | Número de ponto flutuante de dupla precisão.
`FLOAT` | Número de ponto flutuante em que você define o nível de precisão (Número de dígitos significativos)
`BIT` | Armazenamento de um número fixo de Bits. O número de bits deve ser indicado, do contrário o padrão será 1.
`BIT VARYING` | Igual ao `BIT`, permitindo armazenar valores maiores. Utiliza-se para armazenamento de imagens. 
`DATE` | Permite armazenar datas.
`TIME` | Permite armazenar horários. 
`TIMESTAMP` | Permite armazenar uma combinação de data e hora. 
`CHARACTER` ou `CHAR` | Permite armazenar uma cadeia de caracteres (letras, símbolos e números). O tamanho deve ser informado e será fixo, ou seja, mesmo que não utilizado totalmente, será ocupado o espaço fisicamente. O Valor definido será o tamanho máximo da cadeia armazenada. 
`CHARACTER VARYING` ou `VARCHAR` | Permite armazenar cadeia de caracteres, mas com tamanho variável.
`INTERVAL` | Intervalo de data ou hora. 
