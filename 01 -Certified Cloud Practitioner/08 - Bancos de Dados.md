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

## Criando um banco de dados com o RDS
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


