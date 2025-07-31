# VPC
A `Virtual Private Cloud (VPC)` e a forma de criar uma rede isolada na AWS. Quando subimos a instancia Ec2, ele ganha um enderecamento IP que fica associada em uma `subnet`. Todas as instancias dentro desta `subnet` podem se comunicar entre si. A `subnet` fica dentro de uma `Availability Zone (AZ)`. Toda a segmentacao da rede, fica criada dentro de uma `VPC`, e a `VPC` fica criada dentro de uma `Region`.

Uma `Subnet` e uma `VPC` nao conseguem por si so, o acesso a Internet, precisamos adicionar um recurso chamado `Internet Gateway`. Sendo uma vantagem de escolher quais subnets podem ter acesso a Internet e quais nao podem ter acesso a internet. Por exemplo, temos uma aplicacao Web que precisa de acesso da Internet e um banco de dados que nao precisa de comunicacao externa, colocamos o Web Server em uma subnet que possua acesso ao `Internet Gateway` e o servidor do banco de dados, em uma subnet que nao possua acesso ao `Internet Gateway`.

* `Internet Gateway`: Permite o acesso a Internet como tambem o acesso da Internet para dentro da rede.

Abaixo um diagrama da Virtual Private Cloud (VPC):

![Diagram EBS](Images/VPC.png)

Documentacao: https://docs.aws.amazon.com/pt_br/vpc/latest/userguide/what-is-amazon-vpc.html


# Criando uma VPC
No painel da AWS, procure pelo servico `VPC` - Isolated Cloud Resources. A partir desta tela, podemos ver todas as `VPCs` e `Subnets` que temos. Podemos consultar em qual zona as `subnet` esta registrada.

Se clicarmos em `Route Tables`, selecionar a Rote table default e clicar em `Routes`, podemos ver a rota local e tambem uma rota default `0.0.0.0/0` para o `Transit Gateway`.

Para que uma VPC possua sucesso, precisamos das seguintes configuracoes:
1. Alocar um CIDR em uma `VPC`.
2. Configuracao de `Subnet`.
3. Configuracao de uma `Route Table`.
4. Configuracao de um `Transit Gateway` caso as instancias precisem de acesso da Internet.

Antes de criar a nossa VPC, precisamos saber qual o tamanho da rede (quantidade de IPs) e qual sera o enderecamento IP desta rede. Temos que levar em consideracao que a AWS reserva de 3 a 5 IPs para a rede.

1. VPC: `172.16.0.0/16`
2. SubnetA: `172.16.0.0/20`
3. SubnetB: `172.16.16.0/20`


### VPC
Com as informacoes da rede, clique em `Create VPC`.

* `Resources to create`: Selecione a opcao `VPC only` para criamos apenas a VPC.

* `Name tag - optional`: Coloque um nome de identificacao da VPC.

* `IPv4 CIDR`: informe o bloco de enderecamento IP que esta VPC tera.

* `Tenancy`: Vamos manter o `Default`.

* `Tags`: tags de idenficiacao sao opcionais.

Apos inserido as informacoes, clique em `Create VPC`.

Criado a nossa `VPC`, vamos criar as `subnetes`.


### Subnets
No menu a esquerda, acesse `Virtual private cloud` > `Subnets`. Clique em `Create subnet`.

* `VPC ID`: A subnet devera ser acossiada a VPC que foi criada.

* `Subnet name`: Nome de identificacao da Subnet.

* `Availability Zone`: Selecione em qual AZ ela sera utilizada.

* `IPv4 VPC CIDR block`: Bloco de CIDR que sera utilizado.

* `IPv4 subnet CIDR block`: Informe o bloco de rede da subnet.

* `Tags - optional`: Tags para identificacao do recurso.

Podemos ja aproveitar e adicionar uma outra subnet clicando em `Add new subnet` e inserir as informacoes de uma outra subnet.

Clique no botao `Create subnet` para criar.

Com as Subnets criadas, podemos criar a tabela de roteamento


### Route Tables
Acesse no meu do lado esquerdo `Virtual private cloud` > `Route tables`. Clique em `Create route table`.

* `Name - optional`: Adicione um nome de identificacao da tabela de roteamento.

* `VPC`: Selecione a VPC que deseja utilizar.

* `Tags`: Tags de identificacao do servico.

Inserido as informacoes, clique em `Create route table`.

Apos criado a nossa `Route table`, podemos ver em `Routes` que so existe as rotas para ela mesma e em `Subnet associations`, nao temos nenhuma subnet associada.

Clique em `Edit subnet associations`, marque as subnets criadas e clique em `Save associations`. Com esta associacao, podemos colocar um host na `SubnetA` e um host na `SubnetB` e ambos os hosts vao se comunicar.


### Internet Gateway
Acesse no menu a esquerda `Virtual private cloud` > `Internet gateways`. E clique em `Create internet gateway`.

* `Name tag`: Nome de identificacao do Internet Gateway.

* `Tags - optional`: Tags de identificacao do recurso.

Inserido as informacoes, clique em `Create internet gateway`.

Quando criamos o `Internet gateway`, ele fica com o estado de `Detached`, precisamos associar ele a uma `VPC` para podemos utilizar. Clique em `Actions` > `Attach to VPC`.

* `Available VPCs`: Selecione a VPC que deseja fazer o attach do Internet Gateway.

Clique em `Attach internet gateway` para associar o Internet gateway na VPC.

Temos o Internet Gateway na VPC, porem as intancias nao sabem o caminho para chegar ate o Internet Gateway pois esta faltando rotas. Precisamos criar na tabela de roteamento uma rota para que qualquer acesso a internet seja encaminhado para o Internet Gateway.

Acesse no meu a esquerda `Virtual private cloud` > `Route tables`. Selecione a tabela de roteamento da VPC que criamos e clique na aba `Routes` e clique em `Edit routes`.

Na tela de edicao das rotas, clique em `Add route`. 

* `Destination`: Insira o endereco IP 0.0.0.0/0

* `Target`: Selecione a opcao Internet Gateway, Apos selecionado, sera exibido um outro menu de selecao, no qual podemos ver o Internet Gateway que criamos.

Clique em `Save changes` para adicionar a rota.


## Sobre ACL
A `Network Access list (ACL)` proteje a subnet em si, temos uma protecao e controle de acesso pelo `Security Group` e a `ACL` adiciona uma camada de seguranca, permite tudo o que passa nas linhas superiores e na ultima linha ela proibe tudo, atuando como firewall na subnet.

A leitura da lista na ACL e feita de cima para baixo, sendo necessario ficar atento na numeracao `Rule number`, pois como a leitura e feita de cima para baixo, quando cair em uma condicao de bloqueio/liberacao, ela nao continua a leitura ate o final da lista, so executa o momento em que ela realizar o `Match` da regra.

Diferente do Security group, ela possibilita `Explicity Denny`, ou seja, permite negar o acesso. No caso do `Security Group`, ele apenas permite acessos na porta.

A partir do momento que criamos uma VPC, a AWS ja cria uma ACL.

Ao acessar uma ACL, teremos regras de `Inbound rules` e `Outbound rules`. Filtrando o que enta e sai em uma Subnet.

`Network ACLs` sao `stateless`, ou seja precisa ser explicito a regra tanto na entrada quanto na saida, diferente do `Security Groups` que sao `stateful`, nao sendo necessario criar as regras nas duas direcoes (Inbound e Outbound).

Basicamente utilizamos a `Network ACLs` quando queremos fazer o controle entre duas `subnets` e `Security Group` quando queremos fazer o controle por `hosts`.

Para acessar o painel de configuracoes, acesse o servico `VPC` > `Security` > `Network ACLs`.


## VPC Peering
Por padrao, uma maquina em uma subnet dentro de uma VPC, nao consegue se comunicar com outra maquina que esta dentro de outra subnet em uma outra VPC. Para conseguirmos este tipo de comunicacao, utilizamos o `VPC Peering`. Este tipo de comunicacao tambem e conhecida como `ClassicLink`.

Abaixo um Diagrama de como funciona o VPC Peering:

![Diagram VPC Peering](Images/peering-intro-diagram.png)

Documentacao: https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html

Para a configuracao de `VPC Peering`, acesse o painel de controle da AWS, procure pelo servico `VPC` - Isolated Cloud Resources.

No menu esquerdo, localize a secao `Virtual private cloud` > `Peering connections`.

Clique em `Create peering connection`.

* `Name - optional`: Nome da conexao de peering. Uma dica e sempre colocar um nome de referenca da conexao para que no futuro, seja facil de identificacao.

* `Select a local VPC to peer with - VPC ID (Requester)`: A VPC local na conta que sera a solicitante para acesso a VPC destino.

* `Select another VPC to peer with`: A outra VPC de destino, possibilitando o acesso entre VPC da mesma conta, em outra conta e ate mesmo em outra region.

* `Tags`: Tags opcionais para identificacao.

Apos inserido as informacoes, clique em `Create peering connection` para criar a solicitacao.

Apos criado a solicitacao, sera enviado uma requisicao para a VPC de destino, sendo necessario um aceite de comunicacao. Caso esteja utilizando na mesma conta, na tela da propria mensagem que existe a acao pendente, clique em `Actions` > `Accept Request` e clique em `Accept Request` para o aceite da requisicao.

Apos o aceite, sera necessario mudar as regras na tabela de roteamento para que uma VPC possa se comunicar com a outra.


## VPC EndPoint
O `VPC EndPoint` e uma solucao que possibilita criar um endpoint de acesso aos recursos na AWS sem a necessidade de acesso a Internet, fazendo que todo o trafego de acesso aos servicos sejam internamente.

Por exemplo, voce tem um `Bucket do S3`, e tem um host dentro da AWS que precisa de acesso a este bucket, por padrao o trafego vai passar pela internet, pois todo o objeto do S3 ganha um URL exposta para a internet. A Instancia vai precisar sair para a internet para acesso a este bucket.

Em muitos cenarios corporativos, ocorre que devido a uma estrutura de seguranca, ambientes como banco de dados, backend, sistema legados entre outros, os servidores nao podem ter acesso a internet.

Existem dois tipos de EndPoint:
1. `Gateway`: Utilizado para os servicos de S3 e DynamoDB.
2. `Interface`: Utilizado para os outros servicos.

Documentacao: https://docs.aws.amazon.com/vpc/latest/privatelink/create-interface-endpoint.html

Para a configuracao de `VPC EndPoint`, acesse o painel de controle da AWS, procure pelo servico `VPC` - Isolated Cloud Resources.

Acesse no menu localizado a esquerda, `PrivateLink and Lattice` > `Endpoints`, clique em `Create endpoint`.

* `Name tag - optional`: Nome de identificacao do recurso que sera criado.

* `Type`: Selecione a categoria na qual queira criar, por exemplo, se quiser criar para um S3, selecione a opcao `AWS services`.

* `Services`: Selecione o servico, por exemplo, procure por `S3`.

Repare que na lista sera exibido varios tipos de servicos do S3, como ja mencionado a cima, o S3 utiliza o gateway, sendo necessario selecionar a opcao `com.amazonaws.us-east-1.s3 Type:Gateway`.
| Service Name | Owner | Type | Service Region |
| -------- | ------- | ------- | ------- |
| com.amazonaws.s3-global.accesspoint | amazon | amazon | Interface | us-east-1 |
| com.amazonaws.us-east-1.s3 | amazon | amazon | Gateway | us-east-1 |
| com.amazonaws.us-east-1.s3 | amazon | amazon | Interface | us-east-1 |
| com.amazonaws.us-east-1.s3-outposts | amazon | amazon | Interface | us-east-1 |
| com.amazonaws.us-east-1.s3express | amazon | amazon | Gateway | us-east-1 |
| com.amazonaws.us-east-1.s3tables | amazon | amazon | Interface | us-east-1 |


* `Network settings > VPC`: Selecione em qual VPC sera criado o endpoint.

* `Route tables`: Selecione a tabela de roteamento, isso significa que todo mundo que estiver na tabela de roteamento vai conseguir chegar direto no S3.

* `Policy`: Selecione a opcao `Full access` para acesso total ou caso queira customizar a policy, utilize a opcao `Custom`.

* `Tags`: Tags opcionais para identificacao do recurso criado.

Apos inserido as informacoes, clique no botao `Create endpoint`.


## VPC Flow Logs
O `VPC Flow Logs` e um tipo de monitoramento na VPC, muito utilizado para verificar o trafego dentro da VPC, Subent ou dentro de uma interface ENI (Elastic Network Interface).

Documentacao: https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html

Para habilitar o `VPC Flow Logs`, acesse o painel da AWS, procure pelo servico de `VPC` - Isolated Cloud Resources.

No menu localizado a esquerda, selecione a opcao `Virtual private cloud` > `Your VPCs`. Selecione a `VPC` que deseja habilitar o servico.

Clique na guia `Flow logs`. Clique em `Create flow log`.

* `Name - optional`: Nome para identificacao do recurso que sera criado.

* `Filter`: Filtro do que voce quer obter logs
1. `Accept`: Obtem logs de tudo o que e aceito.
2. `Reject`: Obtem logs de tudo o que e rejeitado.
3. `All`: Obtem todos os tipos de logs.

* `Maximum aggregation interval`: Intervalo de quanto tempo sera capturado os pacotes.

* `Destination`: Destino no qual os logs serao armazenados, por exemplo `Cloud Watch`, `Bucket S3`. Apos selecionado a opcao, sera exibido uma outra para determinar grupo ou bucket de destino como tambem a necessidade de uma service role.

* `Log record format`: Formatacao do log, possibilitando customizacoes.

* `Log file format`: Formatacao do arquivo de log.

* `Partition logs by time`: Logs de participacao de tempo, quanto maior o tempo, maior o tamanho do arquivo de log.

* `Tags`: Tags opcionais para identificacao do recurso criado.

Apos inserido as informacoes, clique em `Create flow log`.

Os logs podem demorar um pouco para ser criado.


## Client e Site to Site VPN