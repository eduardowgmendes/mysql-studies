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
( nome-coluna-1 tipo-de-dado-coluna-1 coluna-1-constraint, 
nome-coluna-2 tipo-de-dado-coluna-2 coluna-2-constraint,
nome-coluna-n tipo-de-dado-coluna-n coluna-n-constraint,
constraint-de-tabela)

```

onde:

Argumento | Descrição 
----------|----------
nome-tabela | Nome da Tabela. Deve ser único para o usuário. Não pode coincidir com o nome de outros objetos do banco de dados de um mesmo usuário. 
nome-coluna | Nome da Coluna. Esse nome deve ser único e exclusivo na tabela. 
tipo-de-dado-coluna | Tipo de dado conforme tabela anterior.
coluna-constraint | Regras agregadas à coluna.
constraint-de-tabela | Regras agregadas à tabela inteira.

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
