## Normalização de Dados
Conforme vimos anteriormente, é muito melhor adotarmos uma estratégia em que se utilizem várias tabelas relacionadas em vez de uma única tabela. Basicamente, dois fatores nos levam a essa conclusão: redundância e espaço. Outros fatores também influenciam essa escolha, como a possibilidade de melhorarmos a qualidade da informação, seja fornecendo uma informação mais segura, seja pelo aumento da quantidade de dados no futuro. 

A forma apresentada com o uso do !(Modelo de Entidade X Relacionamento)[https://github.com/eduardowgmendes/mysql-studies/blob/master/chapter/00-conceitos-e-modelagem-de-dados.md#abordagem-relacional-o-modelo-de-entidade-x-relacionamento] é muito prática e usual, mas poderá deixar várias dúvidas quanto ao modelo adotado. Uma forma mais "científica" de realizar esse trabalho é utilizar a normalização de dados. 

A normalização de dados é uma sequência de etapas sucessivas que, ao final, apresentará um modelo de dados estável com um mínimo de redundância. 

Quanto à utilização de um ou outro modelo, não há escolha preferencial. Afinal, o modelo de dados pode ser extraído de uma outra forma. O resultado final deverá ser igual para ambas as formas. Quando se utilizam os dois, é muito mais difícil esquecer alguma informação importante. 

Devemos observar que quando desenvolvemos um sistema, dificilmente temos todas as informações estruturadas da forma como precisamos. Sempre achamos que sabemos o que fazer no sistema, seja por experiência anterior ou por arrogância, estamos destinando nosso sistema a um modelo muitas vezes pobre, incompleto e inadequado. Por isso, é importante utilizar as duas formas para modelarmos os dados. Um modelo deve corresponder ao outro. Se não corresponder, é uma boa oportunidade de voltar e conversar com o(s) usuário(s) e entender melhor o funcionamento da estrutura do sistema.

Há cinco regras que se aplicam a banco de dados: 

* a. Primeira Forma Normal (1FN).
* b. Segunda Forma Normal (2FN).
* c. Terceira Forma Normal (3FN).
* d. Quarta Forma Normal (4FN).
* e. Quinta Forma Normal (5FN).

Ao aplicarmos as regras anteriores já é possível atingirmos o objetivo ao qual se propõe a normalização de dados. Um modelo estável pode ser garantido quando atingimo a terceira forma normal. As demais formas serão utilizadas em casos específicos, desde que sejam absolutamente necessárias. 

O processo de trabalhar informações para criar estruturas de entidades em formas normais é chamado de normalização de dados. 

Antes de iniciarmos a análise de cada uma das etapas de normalização, verificaremos a terminologia utilizada, que envolve basicamente a teoria de conjuntos (que na realidade foi a base para a construção da teoria da normalização), o conceito de banco de dados relacional e a aplicação convencional em ambiente de processamento de dados. Observe na tabela a seguir o que um mesmo termo significa em cada uma das visões: 

| Conjunto | Banco de Dados | Processamento de Dados | 
|----------|----------------|------------------------|
| Relação  | Tabela         | Arquivo                |
| Domínio  | Possíveis valores para coluna | Possíveis valores para o campo | 
| Tupla    | Linha          | Registro |

Como preparação para a normalização, devemos ter a relação de todos os atributos necessários e uma chave primária para a entidade.

## Primeira Forma Normal (1FN)
### Definição 
Diz-se que uma entidade está na primeira forma normal quando nenhum de seus atributos (na estrutura) possuir repetições. 

Isso significa que os atributos são indivisíveis ou que possuem apenas um valor por célula. Deve-se, portanto, validar cada um dos atributos de forma a identificar se este possui um único valor para cada occorência da entidade. Veja que o valor (conteúdo) do atributo pode, e normalmente é, ser diferente em cada ocorrência da entidade (registro). O que se deve evitar é a ocorrência de mais de um atributo com a mesma característica emummesmo registro. Por exemplo, há várias ocorrências do atributo Produto emuma Nota Fiscal. Não é possível determinar se será comprado um ou mais produtos em uma única Nota Fiscal. Portanto, Produto é um atributo repetitivo na entidade Nota Fiscal e deve ser aplicado a primeira regra de normalização.

### Solução 
Neste caso, devemos separar a informação que se repete emuma nova entidade. Devemos ainda levar a chave primária da entidade original para a nova entidade gerada (caso contrário, não haveria como relacionar as informações das duas entidades). Feito isso, criaremos a nova chave para a nova entidade. Normalmente podemos localizar um campo que, unido à chave da entidade. Normalmente podemos localizar um campo que, unido à chave da entidade original, formará a chave da nova tabela (nesse caso, chave concatenada), ou podemos criar um campo para esse fim, caso não exista. Há a possibilidade de criarmos simplesmente uma nova chave não concatenada e independente da entidade original. É uma questão preferência.    

## Segunda Forma Normal (2FN)
### Definição 
Diz-se que uma entidade está na segunda forma normal quando todos os seus atributos **não chave** dependem unicamente da chave. 

Assim, deve-se perguntar a cada atributo, que não seja chave da entidade, se ele depende apenas da chave da entidade. O que se procura com isso é medir o grau de dependência entre os atributos. Apenas coisas semelhantes podem ser unidas em grupos semelhantes (veja que entidade nada mais é do que um grupo ou conjunto).

### Solução
Ao identificarmos uma situação como a descrita anteriormente, devemos separar os atributos independentes e criar ou identificar dentre os atributos separados uma nova chave para esta nova entidade. Essa chave deve ser mantida na entidade original como o atributo de relacionamento entre ambas as entidades. Dessa forma, não se perde qualquer informação no modelo.      

### Anomalias dos Dados 
Geralmente ao tratarmos da Normalização de Dados compreendemos o porque ela existe e quais situações controvérsas ela previne quando pensamos em sistemas de banco de dados. Vamos então entender o que são anomalias de dados e os problemas que geram essas anomalias. 

### Tabelas "Fazem Tudo" geram anomalias.     
