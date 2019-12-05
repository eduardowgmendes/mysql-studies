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

## Abordagem Relacional: O Modelo de Entidade X Relacionamento
A Abordagem Relacional é a utilização de conceitos de Entidade e Relacionamento para criar as estruturas que irão compor o banco de dados. Partindo sempre da necessidade do usuário ou grupo de usuários do sistema, iniciamos a pesquisa das necessidades de informação desses usuários. 

A definição do escopo do sistema é, portanto, importante para o início do trabalho de análise de dados. 

É comum no início do desenvolvimento de um sistema que não tenhamos a noção exata da tarefa a ser realizada. O maior error nessa fase é admitir que jpa sabemnmos o que deve ser feito, seja por experiência anterior, seja por falta de tempo para conversar com os usuários do sistema. 

Para minimizar esse problema, devemos criar uma estrutura gráfica que permita identificar as Entidades de um sistema e como estas se relacionam. 

Nessa fase é importante saber quais informações são importantes para o sistema e o que deve ser armazenado (note que não utilizamos o como deve ser armazenado; isso será discutido na fase posterior). A esta representação gráfica dá-se o nome de Modelo de Dados.

Devemos notar que o Modelo de Dados dará suporte a toda a empresa, incorporando as informações necessárias para o andamento dos negócios. Ele será composto de Entidades e Relacionamentos, daí ser conhecido por MOdelo e Entidade X Relacionamento (MER).

Vantagens na utilização do Modelo de Entidade X Relacionamento: 

* **Sintaxe robusta**: o modelo documenta as necessidades de informação da empresa de maneira precisa e clara 

* **Comunicação com usuário**: os usuários podem, com pouco de esforço, entender o modelo.

* **Facilidade de criação**: os analistas podem criar e manter um modelo facilmente.

* **Integração com várias aplicações**: diversos projetos podem ser inter-relacionados utilizando-se o modelo de dados de cada um deles.

* **Utilização universal**: o modelo não está vinculado a um banco de dados específico, mas sim ao modelo da empresa, o que garante sua independência de implementação.

## Objetivos da Modelagem de Dados

O principal objetivo da Modelagem de Dados é desenvolver um modelo que, contendo as entidades e relacionamentos, seja capaz de representar os requerimentos das informações do negócio.

Veja o que poderia ser um exemplo de catálogo de CDs: 

Cód | Nome do CD | Nome da Música | Nome do Autor |
----|------------|----------------|---------------|
01 | Mais do Mesmo | Será | Renato Russo e ...
02 | Mais do Mesmo | Será | Renato Russo e ...
03 | Mais do Mesmo | Será | Renato Russo e ...
04 | Bate-Boca | Meninos, Eu Vi | Tom Jobim e ...
05 | Bate-Boca | Eu te Amo | Tom Jobim e ...
  
Um dos principais problemas relacionados com banco de dados é a redundância (repetição) das informações. Sempre que houver duas informações, nunca se saberá em qual deals pode confiar.

Imagine que na tabela exemplo alguém altere o nome do CD **apenas** na linha 2 para **Mais ou Menos**. Qual dos nomes estaria correto, **Mais do Mesmo** ou **Mais ou Menos**? É por isso que devemos criar um banco de dados com um mínimo de redundância, evitando esse problema.

Exatamente para evitar redundância é que se cria uma série de tabelas no banco de dados, e não apenas uma. Naturalmente isso aumenta a complexidade da operação, mas traz uma enorme vantagem ao evitar redundância.

Um outro objetivo é a economia de espaço. Quando se admite a redundância, é muito comum ter que repetir nomes, descrições, datas e etc. Ao isolarmos essas informações em tabelas distintas e ao relacionarmos as tabelas por um código comum estamos economizando espaço de armazenamento. 

No exemplo anterior, identificamos que há diversos dados redundantes: código do CD, nome do CD, nome da Gravadadora, preço e autor. Além do mais, a simples repetição desses campos representa um espaço gasto sem necessidade. Podemos separar as informações em mais de uma tabela, armazenando apenas uma vez cada informação distinta e relacionando as tabelas. 

Exemplo: podemos criar uma tabela para armazenar os dados dos CDs (código do CD, nome do CD, nome da gravadora e preço) e outra para armazenar as músicas (Número da Faixa, Nome, Autor, e Tempo). Basta acrescentar o código do CD em Músicas e teríamos uma relação entre Música e CD. Contudo, somente isso não é suficiente. 

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

## Entidades Associativas 
Há um caso específico para as Entidades Associativas: sempre que, além do simples relacionamento entre as duas entidades fundamentais, houver outras informações específicas da nova entidade criada (como, por exemplo, a quantidade e o valor entre o pedido x produto ou bimestre, nota e faltas do aluno x matéria), ela será chamada de entidade associativa atributiva.

No catálogo de CD dado como exemplo, podemos identificar facilmente duas entidades: CD e Música. Observando com mais cuidado, vê-se que Gravadora e Autor também possuem uma estrutura independente. Isso porque há outras informações que, apesar de não estarem descritas na planilha, são fato apenas da Gravadora e do Autor. Exemplo: endereço, data de nascimento, telefone e etc. Para isso é importante entender o que são os atributos (catacterísticas) de uma Entidade.   

## Atributos 
Os atributos são as informações básicas que qualificam uma entidade e descrevem seus elementos ou características. 

Há uma tendência em confundir Entidade e Atributo. Tenha em mente que atributo é uma característica, logo não contém um grupo de informações. POr sua vez, uma entidade sempre é um grupo. No mínimo são necessários dois atributos para criar uma entidade.

Exemplos de atributos para as entidades: 

**Entidade Pessoa**: nome, endereço, documento, data de nascimento, telefone e e-mail.

**Entidade Nota Fiscal**: série, número, data de emissão e cliente.

## Tupla 
É uma estrutura de atributos intimamente relacionados e interdependentes que residem em uma entidade. Saindo um pouco da definição formal uma tupla a grosso modo seria um registro.

## Chave
É um atributo utilizado para indexar dados. 

Há três tipos de chave: 

* Primária 
* Estrangeira
* Secundária 

### Chave Primária
É o atributo que permite identificar uma única ocorrência de uma tupla em uma Entidade. 
Dessa forma, seu conteúdo deve ser único, exclusivo e imutável para cada linha dessa Entidade. Todos os demais atributos da entidade devem depender unicamente desse atributo. 
Nem todo campo é uma boa chave primária. Normalmente utilizamos campos numéricos por serem localizados mais rapidamente pelos bancos de dados. Valores alfanuméricos grandes têm acesso mais lento. Todas as tabelas devem conter uma chave primária. 

### Chave Estrangeira 
É o atributo que estabelece relação de uma Entidade com a Chave Primária de outra Entidade e permite uma relação entre entidades.

![Chave Estrangeira Exemplo](https://raw.githubusercontent.com/eduardowgmendes/mysql-studies/master/images/mdr_chave_estrangeira.jpg)

### Chave Secundária 
Esta chave é utilizada como meio de classificação e pesquisas em entidades.    

## Relacionamento 
Sempre que duas entidades apresentarem interdependência (por exemplo, autor da música ou música do CD), indica-se um relacionamento entre elas.

Assim podemos dizer que: 

1. Cada CD deve ser gravado por uma única gravadora. 
2. Cada gravadora pode ter gravado um ou mais CDs. 

1. Cada autor pode ter escrito uma ou mais músicas.
2. Cada música pode ser escrita por um ou mais autores.

1. Cada música pode estar gravada em um ou mais CD.
2. Cada CD deve conter uma ou mais músicas. 

1. Cada CD pode ser indicado por um ou mais CDs. 
2. Cada CD pode indicar um único CD. 

Conforme você pode notar, cada relacionamento contém um nome (normalmente um verbo como ser gravado, conter, ter escrito), a determinação de opcionalidade (deve ou pode) e um grau ou cardinalidade (uma única ou uma ou mais).

### Cardinalidade 
Há três tipos de relacionamentos: 

* Um para um (1:1)
* Um para muitos (1:n)
* Muitos para muitos (m:n)

### Relacionamento 1:1
Ocorre sempre que uma entidade tiver uma única ocorrência para cada ocorrência na outra entidade. Exemplos:

* Departamento e Gerente
	* Para cada departamento existe apenas um gerente 
* Placa Mãe e Computador
	* Cada computador possui apenas uma placa mãe  

### Relacionamento 1:n
Ocorre sempre que uma entidade se relacionar com uma ou mais tuplas da outra entidade e esta outra se relacionar apenas com uma tupla daquela entidade. 

* Gravadora e CD 
	* Uma gravadora possui vários CDs gravados por ela
* Cliente e Pedido
	* Um cliente possui vários pedidos
* Pedido e Item do Pedido
	* Um pedido possui vários itens 

### Relacionamento m:n
Ocorre sempre que uma entidade se relacionar com várias tuplas de outra entidade e esta, por sua vez, relacionar-se com várias tuplas daquela entidade.  

* Autor e Música 
	* Cada música é composta por vários autores e cada autor pode compor uma ou várias músicas 
* Aluno e Matéria 
	* Cada aluno é inscrito em uma ou várias matérias e cada matéria possui vários alunos 

