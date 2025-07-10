# Banco de Dados
Existem dois tipos de Banco de Dados:
1. `Relacionais // Relational DB (SQL)`
2. `Nao Relacionais // Non Relational DB (NonSQL)`

### Relacionais
Os Bancos de Dados `Relacionais`, criam tabelas e voce cria uma relacao de tabelas uma com a outra.

### Nao Relacionais
Os Bancos de Dados `Nao Relacionais`, criam entradas em diferentes colunas.

Quando precisamos de dados estruturados, precisamos de um Banco de Dados `Relacionais`, por exemplo, se eu tenho um cliente com um ID, este ID do cliente pode ser utilizado em outros lugares.

No caso do `Nao Relacionais`, ele e utilizado mais para sistemas de `Big Data`, ou quando precisamos de informacoes em `real time`. Sendo otima para aplicacoes de rapido acesso.


### Sobre o RDS
O `Relational Database Service (RDS)`, possui uma lista de Database proprietaria (Aurora) entre outras Databases na voce pode criar. Este servico e gerenciado pela AWS, ela gerencia, provisionamento, patch de atualizacao, garante disastre recovery e escabilidade do ambiente.

No Caso do Aurora, nao e necessario nem escolher o espaco de armazenamento, pois tudo e gerenciado pela propria AWS.

Bancos disponiveis no RDS:
1. Postgres
2. MySQL
3. MariaDB
4. Oracle
5. Microsoft SQL Server (MSSQL)
6. Aurora

O Aurora possui uma compatibilidade para MySQL e Postgres, nao possuindo disponibilidade para free tier, ela garante que o Aurora possui 5x mais performance do que um MySQL e 3x mais performance do que o Postgres.

### Criando um banco de dados com o RDS
Dentro do painel da AWS, localize o servico `RDS` (Aurora and RDS -Managed Relational Database Service). Clique em `Create database`.

> [!CAUTION]  
> Cuidado para criar um servico de RDS, pois ele sera cobrado. Mesmo provisionando um ambiente pequeno com uma unica instancia, e criado uma maquian db.t4g.micro, podendo este custo chegar a U$86,51 (Dolares). Recomendo que apenas visualize as opcoes e entenda as configuracoes.

* `Choose a database creation method`: Selecione a opcao `Standard create` para que possamos ter varias opcoes de configuracoes como seguranca, backup, manutencao e etc.

* `Engine options`: Selecione o banco de dados que deseja utilizar, neste caso, vou utilizar o MySQL para utilizar a opcao de Free Tier.

* `Edition`: Selecione qual a edicao deseja utilizar. Essas configuracoes podem variar de acordo com o Banco de Dados selecionado. 

* `Engine version`: Selecione qual a versao da engine deseja utilizar. Essas configuracoes podem variar de acordo com o Banco de Dados selecionado.

* `Templates`: Voce seleciona de acordo com o ambiente, neste exemplo estarei utilizando o `Free tier`, pois nao iremos utilizar em ambiente de teste ou producao.

* `Availability and durability`: Como estamos utilizando no `Free tier`, so teremos a opcao de 1 instancia em uma AZ, para ambientes de producao, e recomendado utilizar ambientes de Cluster em Multi AZ de acordo com necessidade da aplicacao. Cada escolha sera um valor final no ambiente.

* `Settings > DB instance identifier`: Nome de identificacao do banco de dados.

* `Credentials Settings`: Credenciais de acesso ao banco de dados.

* `Instance configuration`: Instance Type que deseja utilizar.

* `Storage`: Configuracoes do volume EBS como o Storage type e tamanho do volume.

* `Connectivity`: Configuracoes de rede como VPC, acesso publico, Subnet entre outras configuracoes.

* `Tags - optional`: Tags para identificacao do banco.

* `Database authentication`: Metodo de autenticacao no banco de dados.

* `Monitoring`: Modelo de monitoramento do banco de dados.

* `Additional configuration`: Parametros de configuracoes adicionais.

> [!CAUTION]  
> Cuidado para criar um servico de RDS, pois ele sera cobrado. Mesmo provisionando um ambiente pequeno com uma unica instancia, e criado uma maquian db.t4g.micro, podendo este custo chegar a U$86,51 (Dolares). Recomendo que apenas visualize as opcoes e entenda as configuracoes.

Caso esteja tudo certo, clique em `Create Database`


## Elasticache
Como percebemos na criacao de um RDS, o servico provisiona instancias para o banco de dados, ou seja, um numero de instancias, com volumes EBS que pode ser `HDD` ou `SSD`. Este tipo ainda caba sendo um pouco mais lento, pois o banco fica armazenado em um volume, e temos o tempo de latencia de acesso ao volume. O `Elasticache` nada mais do que um banco de dados em memoria. Ele e em `In-Memory`, tornando um cache, por um curto espaco de tempo.

Quando utilizado o `Elasticache`, apontamos os servidores de aplicacao para o servico do `Elasticache` e entao o `Elasticache` consulta o banco de dados. Esta arquitetura reduz evita carga ao banco de dados, pois ele faz a consulta e ao fazer a proxima requisicao, o proprio `Elasticache` nao vai ate o banco de dados solicitar o processamento. Aumentando a performance da aplicacao e reduzindo o load no banco de dados.

Ele utiliza um de dois tipos de armazenamento (data store):
1. Redis
2. Memcache

Sao Open Sources, a diferenca e que o `Memcache` e bem mais simples e o `Redis` possui mais features ou caracteristicas que podemos alterar.


## DynamoDB
A AWS possui como proprietario um banco de dados `Non SQL`, chamado `DynamoDB`, existem outros, porem este e da AWS, ele possui uma disponibilidade e escabilidade muito grande. Armazernando por padrao em 3 AZs. O `DynamoDB` ao contrario dos demais, ele e `Servless`, ou seja, nao precisa de servidores ou instancias para utilizar.

### Criando um DynamoDB
Na console da AWS, procure pelo servico `DynamoDB` - Managed NoSQL Database. Ele por nao ser `SQL`, ele funciona como tablelas. Clique em `Create table`.

* `Table name`: Nome da tabela que deseja criar.

* `Partition key`: Seria uma chave primaria da tabela. Um valor de hash para recuperar itens da tabela e alocar os dados.

* `Table settings`: Pode manter o padrao `Default settings`.

* `Tags`: Tags para identificacao.

Clique em `Create table` para provisionar o DynamoDB.


## Amazon Neptune
O `Amazon Neptune` e um tipo de banco de dados para uma funcao, ele e fantastico para quando utilizado Social Network ou quando a aplicacao possui uma grande quantidade de links de artigos por exemplo Wiki Pedia.

Quando implementado, ele e disponivel em 3 AZs no minimo, e pode criar no maximo 15 Read replicas, podendo armazenar bilhoes de mensagens ou informacoes no `Amazon Neptune`. A latencia e na casa de milisegundos e pode ser utilzia com pesquisas complexas. O grande ponto do `Amazon Neptune`, ele pode criar `Graph Dataset`, ou seja, visualizar de forma grafica os dados dentro do banco.


## AWS Glue
O `AWS Glue` faz `ETL (Extract Transform Load)`, ou seja, extrai, transforma e carrega, sendo utilizado para a parte de analytics, fazer analises e entender o que os dados podem nos passar.

Basicamente o `AWS Glue` faz:

`Extract`: Extrai dados de um `Bucket S3` ou `banco de Dados / RDS`.

`Transform`: Transforma dentro do `Glue`.

`Load`: Carrega estes dados para um `Redshift`, possibilitando que voce faca analise dos dados.