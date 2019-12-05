## Conceitos e Modelagem de Dados

### Introdução 
Desde o início da utilização dos computadores, sabemos que um sistema é feito para aceitar entrada de dados, realizar processamentos e gerar saída das informações processadas. Com o tempo, verificou-se a necessidade de armazenar as informaçẽos geradas pelos programas de computadores. O armazenamento e a recuperação das informações passaram a desempenhar um papel fundamental na informática. 

Em junho de 1970, E. F. Codd, membro do Laboratório de Pesquisa da IBM em San Jose , na Califórnia, publicou um trabalho intitulado "*A Relational Model of Data for Large Shared Data Banks*" (Um Modelo Relacional de Dados para Grandes Bancos de Dados Compartilhados), no jornal *Association of Computer Machinery*. Nesse trabalho, Codd estabeleceu princípios sobre gerência de banco de dados, denominando-os com o termo relacional. Essa foi a base utilizada na criação de uma linguagem padrão para manipular informações em Banco de Dados Relacionais. E essa linguagem é a SQL (*Structured Query Language*).

Inicialmente chamada de SEQUEL (*Structured English Query Language*), a linguagem SQL foi concebida e desenvolvida pela IBM, utilizando os conceitos de Codd. Em 1979, a Relational Software Inc., hoje Oracle Corporation, lançou a primeira versão comercial da linguagem SQL. 

Atualmente a SQL pode ser considerada um padrão para manipulação de dados em banco de dados. Duas entidades, a ANSI (*American National Standards Institute*) e a ISO (*International Standards Organization*), vêm ao longo do tempo padronizando a linguagem SQL. O primeiro padrão (SQL-86) foi definido pela ANSI em 1986 e consistia basicamente na SQL da IBM, com poucas modificações. Em 1987, a ISO adotou o mesmo padrão. Em 1989, surge uma nova versão (SQL-89), com significativas modificações.

## O que é SQL? 
SQL (*Structured Query Language*) é um conjunto de comandos de manipulação de banco de dados utilizado para criar e manter a estrutura desse banco de dados, além de incluir, excluir, modificar e pesquisar informações nas tabelas dele. A linguagem SQL não é uma linguagem de programação autônoma; poderia ser chamada de "sublinguagem". 

## Divisão da Linguagem 

A linguagem SQL é dividida nos seguintes componentes: 

### Data Definition Language (DDL)
Permite a criação dos componentes do banco de dados, como tabelas, índices etc. 

Principais comandos DDL: 

* `CREATE TABLE` 
* `ALTER TABLE` 
* `DROP TABLE` 
* `CREATE INDEX`
* `ALTER INDEX`
* `DROP INDEX`  

### Data Manipulation Language (DML)
Permite a manipulação dos dados armazenados no banco de dados. 

Princpais comandos DML: 

* `INSERT`
* `DELETE`
* `UPDATE`

### Data Query Language (DQL)
Permite extrair dados do banco de dados. 

Comando: 

* `SELECT`

### Data Control Language (DCL)
Provê a segurança interna do banco de dados. 

Comandos DCL:

* `CREATE USER`
* `ALTER USER`
* `GRANT`
* `REVOKE`
* `CREATE SCHEMA`

## Banco de Dados 
Banco de Dados é um conjunto coerente e lógico de dados relacionados que possuem significância intrínseca. Esses dados representam aspectos do mundo real e devem ser mantidos para atender aos requisitos da empresa. 

## Tabela 
Uma tabela pode ser compreendida como um conjunto de linhas e colunas. As colunas de uma tabela qualificam cada elemento (no caso, a linha) com informações relacionadas ao objeto.
Utilizando esses conceitos, é possível armazenar dados em uma ou várias tabelas, dependendo do que e como desejamos as informações. 

## Entidade 
Entidade é um agrupamento lógico de informações inter-relacionadas necessárias para a execução das atividades do sistema. Uma entidade normalmente representa um objeto do mundo real, quando não é, contém informações relevantes às operações da empresa .

### Exemplos de entidades 
Entidade | Objetos 
---------------------|-------------------
Físicas ou Jurídicas | Pessoas, funcionários, clientes, fornecedores e empresa   
Documentos | Ordem de compra, pedido e nota fiscal
Local | Almoxarifado e departamento
Tabelas | Classificação fiscal, centro de custo e UF
Matéria | Produto e peça 

### Classificação de entidades
As entidades podem ser classificadas em dois tipos: 

### Fundamental 
Contém dados básicos que são resultados ou alimentadores das operações da empresa. 

### Associativa 
É formada pele Relacionamento de duas Entidades Fundamentais sempre que estas se relacionarem mais de uma vez. Exemplos: 

* Aluno x Matéria 
* CD x Autor 
* Pedido X Produto etc. 
