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

## Criação de Tabelas 
Tabelas são as estruturas mais importantes de um banco de dados. Nas tabelas estará o conteúdo que representa cada objeto do mundo real, cuja importância para o funcionamento do sistema justifica a sua criação. As próprias tabelas criadas no banco de dados ficam armazenadas em tabelas internas do gerenciador de banco de dados. É o chamado Dicionário de Dados. Com a utilização do Dicionário de Dados, as informações das tabelas ficam sempre à disposição do usuário e permitem um controle maior do que está sendo armazenado. 

O padrão SQL divide em três categorias as tabelas de um banco de dados: 

* **a. Tabelas permanentes**: ficam permanentemente armazenadas no banco de dados, a menos que sejam explicitamente excluídas. 

* **b. Tabelas temporárias globais**: utilizadas para armazenamento temporário de informaçoes durante algum processamento específico, são eliminadas assim que for encerrado o acesso ao banco de dados. Possuem visibilidade em todo o banco de dados. 

* **c. Tabelas temporárias locais**: semelhantes às globais, são visíveis apenas em um módulo específico em que foram criadas. 

Note que as tabelas temporárias possuem um conceito diferente das Visões de Banco de Dados (`Views`). 

As tabelas que criaremos para armazenar as informações do nosso sistemas serão tabelas permanentes. Para criá-las, utilizaremos o comando `CREATE TABLE`.

### Integridade Referencial - `Constraints`
Constraints são regras agregadas a colunas ou tabelas. Assim pode-se definir como obrigatório o preenchimento de uma coluna que tenha um valor-padrão quando uma linha for incluída na tabela ou quando aceitar apenas alguns valores predefinidos. NO caso de regras aplicadas a tabelas, tem-se a definição de chaves primárias e estrangeiras. Veremos adiante como colocar isso em prática. 

### `CREATE TABLE`
A sintaxe básica do comando é a seguinte: 

```sql

CREATE TABLE nome_tabela
( nome-coluna1 tipo-de-dado-coluna1 coluna1-constraint, 
nome-coluna2 tipo-de-dado-coluna2 coluna2-constraint,
nome-colunan tipo-de-dado-colunan colunan-constraint,
constraint-de-tabela)

```

onde:

Argumento | Descrição 
----------|----------
*nome-tabela* | Nome da Tabela. Deve ser único para o usuário. Não pode coincidir com o nome de outros objetos do banco de dados de um mesmo usuário. 
*nome-coluna* | Nome da Coluna. Esse nome deve ser único e exclusivo na tabela. 
*tipo-de-dado-coluna* | Tipo de dado conforme [tabela anterior](https://github.com/eduardowgmendes/mysql-studies/blob/master/chapter/01-fundamentos-e-definicoes-basicas.md#defini%C3%A7%C3%A3o-de-dados).
*coluna-constraint* | Regras agregadas à coluna.
*constraint-de-tabela* | Regras agregadas à tabela inteira.

Exemplo: 

```sql

CREATE TABLE CD (
Codigo_CD		INTEGER NOT NULL,
Codigo_Gravadora	INTEGER NULL,
Nome_CD			VARCHAR(60) NULL,
Preco_Venda		DECIMAL(16,2) NULL,
Data_Lancamento		DATE DEFAULT SYSDATE,
CD_Indicado		INTEGER NULL,
PRIMARY KEY(Codigo_CD),
FOREIGN KEY(Codigo_Gravadora)
REFERENCES Gravadora (Codigo_Gravadora),
CHECK (Preco_Venda > 0)
);

```
## Tipos de Constraints mais comuns

Serão analisados alguns tipos de constraints encontrados com mais frequência nos bancos de dados. As constraints variam muito de um banco de dados para outro. Pode ser que algumas delas não esteja presente no banco de dados que você estiver utilizando.

### Chave Primária 
Conforme discutimos anteriormente, chave primária é a coluna, ou grupo de colunas, que permite identificar um único registro na tabela. Para especificar que uma coluna ou grupo de colunas representa a chave primária de uma tabela, deve-se acrescentar a palavra-chave `PRIMARY KEY` seguida do nome da(s) colunas(s). Alguns bancos de dados permitem especificar a chave primária como constraint da coluna (quando a chave primária for apenas uma coluna) ou como constraint de tabela. Outros aceitam apenas como constraint de tabela. Para facilitar, aconselha-se utilizar a chave primária como constraint de tabela.

Digamos que haja uma tabela de cliente cuja chave primária seja o campo *CDCLIENTE*. A criação da chave primária ficaria assim: 

```sql

PRIMARY KEY (CDCLIENTE),

```

### Chave Estrangeira 
Chave estrangeira é o campo que estabele o relacionamento entre duas tabelas. Assim, uma coluna, ou grupo de colunas, de uma tabela corresponde à mesma coluna, ou grupo de colunas, que é a chave primária de outra tabela. Dessa forma, deve-se especificar na tabela que contém a chave estrangeira quais são essas colunas e à qual tabela está relacionada. Veja que o banco de dados irá verificar se todos os campos que fazem referência à tabela estão especificados. 

Ao determinar esse tipo de relacionamento, fica garantido a integridade  das informações. Os valores presente na(s) coluna(s) definida(s) como chave estrangeira devem ter um correspondente na outra tabela, caso contrário o banco de dados deve retornar uma mensagem de erro. É normal que, ao tentar excluir um registro de uma tabela, o banco de dados verifique se há chaves estrangeiras relacionados a esse registro. Se houver, também será retornado um erro impedindo essa operação. 

Infelizmente, muitos programadores não utilizam esses recursos dos bancos de dados. Se não forem definidas as chaves estrangeiras nas tabelas, apenas o programa controlará o que pode ou não ser excluído ou alterado, colocando em risco informações revelantes do sistema. Por exemplo, pode-se excluir uma peça de tabela, mesmo que haja pedidos ou notas fiscais relacionada a ela. Dessa forma, perde-se a informação. Muitos poderiam dizer que o programa não permitiria tal ocorrência. É verdade. Porém todos os bancos de dados possuem programas de manipulação direta dos dados. Não é apenas por meio do seu programa que alguém irá manipular as informações. Alías, se alguém estiver mal intencionado, não utilizará o seu programa para agir (...).

Para especificar uma chave estrangeira, utilize a seguinte sintaxe: 

```sql

FOREIGN KEY nome-chave-estrangeira ( lista-de-colunas )
REFERENCES nome-tabela ( lista-de-colunas )
ON UPDATE ação
ON DELETE ação

``` 
Onde: 

Opção | Descrição
------|----------
*nome-chave-estrangeira* | Nome opcional da constraint
*lista-de-colunas* | Lista de colunas de tabela que faz referência a outra referência a outra tabela.
*nome-tabela* | Nome da tabela em que está a chave primária
*ação* | Determina qual ação o banco de dados deve tomar quando for excluída ou alterada uma linha de tabela que contém referência a esta chave. Pode ser `SET NULL`(altera o conteúdo da coluna para Nulo, perdendo a referência, sem deixar valores inconsistentes), `SET DEFAULT` (altera o conteúdo da coluna para o valor especificado na cláusula `DEFAULT` se houver), `CASCADE` (exclui ou altera todos os registros que se relacionam a eles), `NO ACTION` (em caso de alteração, não modifica os valores que se relacionam a eles) ou `RESTRICT` (não permitem a exclusão da chave primária).

Como por exemplo, vamos fazer referência à tabela de cliente quando estamos criando a tabela de pedidos: 

```sql

FOREIGN KEY pedido_cliente_fk ( cdcliente )
REFERENCES cliente
ON UPDATE CASCADE
ON DELETE RESTRICT,

```

Veja que não houve a necessidade de iniciar a lista de colunas após o nome de tabela que contém a chave primária, pois esta foi definida na criação da tabela Cliente.

### `DEFAULT`
Serve para atribuir um conteúdo-padrão a uma coluna da tabela, sempre que for incluída uma nova linha na tabela. Deve-se especificar a palavra-chave `DEFAULT`, seguida do conteúdo-padrão. Imaginando uma coluna QUANTIDADE que deva ter o conteúdo-padrão 1, deveríamos criá-las desta forma: 

```sql 

QUANTIDADE INTEGER DEFAULT 1,

```

### `NOT NULL`
Indica que o conteúdo de uma coluna não poderá ser Nulo. Se cada coluna não tiver valor atribuído durante uma inclusão, terá seu valor Nulo. Alguns outros bancos de dados não SQL atribuíam conteúdo em função do tipo de dado: campos numéricos tinham valor zero, cadeias de caracteres conteúdo branco e assim por diante. 

Lembre-se: em bancos de dados SQL, colunas sem valor atribuído possuem conteúdo Nulo. 

Dessa forma, ao tentar incluir uma coluna com essa restrição, que não apresenta valor, o banco de dados retornará uma mensagem de erro e não incluirá a linha. Imagine um caso em que não se possa incluir um cliente sem que seja preenchido o nome. Essa coluna seria criada desta forma: 

```sql

NOME_CLIENTE VARCHAR(50) NOT NULL,

```

### `UNIQUE` 
Indica que não pode haver repetição no conteúdo da coluna. Isso é diferente do conceito de chave primária. A chave primária, além de não permitir repetição, não pode conter valores nulos. Ao especificarmos que uma coluna deve conter valores únicos, indicamos que todos os valores não nulos devem ser exclusivos. Devemos acrescentar a cláusula `UNIQUE`, após a definição da coluna, ou `UNIQUE`, seguida dos  campos que devam ter essa característica no final da criação da tabela. Ainda na tabela de clientes, vamos especificar o número do CPF como campo de valor único. 

```sql

CPF NUMERIC(11) UNIQUE,

``` 

### `CHECK` - Definição de domínio
Um domínio é uma expressão de valores possíveis pra o conteúdo de uma coluna. Podemos, ao criarmos uma coluna, especificar quais os valores que poderão ser utilizados para preencher a coluna. Para criar um domínio para uma coluna, utilizamos a palavra-chave `CHECK`, seguida da condição que validará o conteúdo. Imagine um campo de sexo. Esse campo só poderá aceitar M para masculino ou F para feminino. O domínio dessa coluna é (M, F) e seria criado desta forma: 

```sql

SEXO CHAR(1) CHECK ( UPPER(SEXO) = 'M' OR UPPER(SEXO) = 'F'),

``` 

### Assertivas 
Uma assertiva é utilizada para estabelecer restrição no banco de dados com base em dados de uma ou mais tabelas. Dessa forma, você pode estabelecer como regra que a tabela CD sempre tenha de uma linha.

```sql

CREATE ASSERTION nome 
	CHECK ( expressão_logica );

CREATE ASSERTION ha_cd 
	CHECK ( EXISTS select codigo_cd from CD );

``` 

### Alteração de estrutura de tabela 
Para alterar a estrutura de uma tabela, utilizamos o comando `ALTER TABLE`. Dependendo do banco de dados, podemos: 

### Acrescentar novas colunas 

O comando utilizado para acrescentar novas colunas é muito semelhante ao da criação de colunas em uma tabela: 

```sql

ALTER TABLE tabela
	ADD nome-coluna tipo-de-dado constraints [ nome-coluna tipo-de-dado constraints, ...]

```

Exemplo: 

```sql

ALTER TABLE cliente 
	ADD email varchar(80) UNIQUE

```

## Acrescentar novas constraints
O comando utilizado para acrescentar novas constraints é muito semelhante ao da criação de constraints em uma tabela: 

```sql

ALTER TABLE tabela 
	ADD PRIMARY KEY (CDCLIENTE)

```

Nesse caso, estamos alterando uma constraint de tabela. Note que a colocação do parênteses após a cláusula `ADD` é opcional. Uma constraint de coluna deve ser alterada utilizando o comando a seguir, relacionado à própria coluna. 

### Modificar colunas 
Podemos modificar qualquer característica de uma coluna, seja o tipo de dado (alguns bancos de dados requerem ausência de conteúdo na coluna para fazer essa alteração), o tamanho (alguns só aceitam alterações para valores maiores que o definido) e as constraints:

```sql

ALTER TABLE tabela 
	MODIFY (nome-coluna tipo-da-dado constraints)

```

Exemplo: 

```sql

ALTER TABLE cliente 
	MODIFY email varchar(100) NOT NULL

```

Podemos especificar apenas o que estamos modificando; não é necessário repetir o que não será alterado. Assim, se quisermos apenas modificar o tipo de dado e seu tamanho, não é necessário especificar a constraint e vice-versa. De qualquer forma, devemos sempre especificar qual coluna está sofrendo a modificação. 

### Excluindo elementos
Pelo padrão SQL, deveria ser possível excluir colunas ou constraints de uma tabela. Alguns bancos de dados não permitem a exclusão de colunas. No Oracle , a cláusula de exclusão é `DROP` e não `DELETE`, como definido desde a SQL-92.

```sql

ALTER TABLE tabela
DELETE elemento

```

Exemplo 1 - Exclusão de coluna: 

```sql

ALTER TABLE cliente 
	DELETE email

```

Exemplo 2 - Exclusão de constraint de tabela: 

```sql

ALTER TABLE cliente 
	DELETE primary key

```

Exemplo 3 - Exclusão de constraint de tabela: 

```sql

ALTER TABLE cliente 
	DELETE FOREIGN KEY pedido_cliente_fk

```

Note que a exclusão de constraint de coluna deve ser feita como uma alteração da coluna. Veja o exemplo anterior. 

### Trocar nome de elementos 

Podemos trocar o nome de tabelas ou colunas (alguns bancos de dados não permitem essa operação):

* a. Alteração de nome de tabela

```sql

ALTER TABLE tabela 
	RENAME nome-tabela

```

Exemplo: 

```sql

ALTER TABLE cliente 
	RENAME cli

```

* b. Alteração de nome de coluna 

```sql

ALTER TABLE tabela 
	RENAME coluna-velha TO coluna-nova

```
Exemplo: 

```sql

ALTER TABLE cliente
	RENAME nome_cliente TO nmcliente

```

## Eliminando uma tabela 
Para eliminar uma tabela do banco de dados, utilizamos o comando `DROP TABLE` seguido do nome da tabela. Alguns bancos de dados somente permitirão a exclusão da tabela desde que esta não esteja relacionada a outras. Alguns deles podem conter cláusulas específicas para excluir a tabela, independentemente das constraints definidas (no Oracle, você pode especificar `CASCADE` após o nome da tabela). Exemplo: 

```sql

DROP TABLE cliente

```   
