## Elastic Compute Cloud
O Elastic Compute Cloud (EC2) e um dos servicos mais utilizados na AWS, sendo um servico de infratratura (IAAS) para maquinas virtuais.

Algumas pontos chaves sobre a Amazon EC2

`Máquinas Virtuais`: EC2 fornece instâncias, que são máquinas virtuais executando os sistemas operacionais que você escolher.

`Escalabilidade`: Você pode dimensionar a capacidade de computação facilmente, criando e lançando novas instâncias conforme necessário, o que é útil para lidar com picos de demanda e escala.

`Controle Completo`: Os usuários têm controle total sobre as instâncias do EC2. Eles têm acesso de root, e podem interagir com elas como fariam com qualquer máquina.

`Várias Regiões e Zonas de Disponibilidade`: As instâncias do EC2 podem ser implantadas em várias regiões geográficas e zonas de disponibilidade. Isso ajuda a reduzir latência, aumentar a tolerância a falhas e cumprir os requisitos de residência de dados.

`Modelos de Instância`: O EC2 fornece uma variedade de tipos de instâncias otimizadas para diferentes casos de uso, garantindo que você tenha os recursos de que precisa para o aplicativo que está executando.

`Preços Flexíveis`: O EC2 oferece várias opções de preços, incluindo On-Demand (pague pelo que usar), Reservado (reserve uma instância por um período e obtenha um desconto) e Spot (licitação por capacidade não utilizada a preços mais baixos).

`Armazenamento Integrado`: As instâncias do EC2 podem ser integradas com outros serviços da AWS para fornecer armazenamento (por exemplo, Amazon EBS), bancos de dados (por exemplo, Amazon RDS), e redes (por exemplo, Amazon VPC).

`Segurança`: O EC2 trabalha com o Amazon VPC para fornecer segurança e robustez por meio de grupos de segurança e redes isoladas.


## Tipos de EC2
O Amazon EC2 oferece uma variedade de tipos de instâncias otimizados para atender diferentes casos de uso. Os tipos de instâncias compreendem combinações variadas de capacidade de CPU, memória, armazenamento e rede e proporcionam a flexibilidade para escolher a combinação apropriada de recursos para seus aplicativos. Os principais tipos de instâncias do Amazon EC2 incluem:


Abaixo algumas informacoes para analise durante a escolha do instance type:

`Instance Size`: Tipo de instancia, Cada instance type possui sua configuracao e otimizacao, levando a propositos gerais ou especificos, variando o tipo de tecnologia, CPU e otimizacao em que a maquina virtual sera alocada. Podendo pode estar disponivel ou nao em determinadas regions;

`vCPU `: Quantidade de Virtual CPU;

`Memory (GiB)`: Quantidade de memoria em Gigas;

`Instance Storage (GB)`: Tamanho do espaco de armazenamento, quando identificado como `EBS-Only`, significa que precisa se adicionado um disco EBS (Elastic Block Store) na instancia para obter um armazenamento;

`Network Bandwidth (Gbps)`: Taxa de transferencia da rede (throughput);

`EBS Bandwidth (Gbps)`: Taxa de transferencia para comunicacao da instancia com o disco EBS;

Link: https://aws.amazon.com/ec2/instance-types/

1. `Instâncias de Uso Geral (A, T, M)`: Essas instâncias proporcionam um bom equilíbrio de computação, memória e rede e são uma boa escolha para muitas cargas de trabalho que não requerem especificações de hardware específicas.

2. `Instâncias Otimizadas para Computação (C)`: Essas instâncias são otimizadas para cargas de trabalho que exigem alta performance de CPU, como computação científica, modelagem e análise financeira, e renderização de mídia.

3. `Instâncias Otimizadas para Memória (R, X, Z)`: Essas instâncias são projetadas para cargas de trabalho que processam grandes conjuntos de dados na memória, como bancos de dados em memória, caches distribuídos, análise em memória e aplicações de big data.

4. `Instâncias Otimizadas para Armazenamento (D, I, H)`: Essas instâncias são projetadas para cargas de trabalho que requerem alto desempenho de armazenamento local, como bancos de dados escalonáveis, processamento de dados em escala de petabytes e aplicações de data warehousing.

5. `Instâncias Otimizadas para GPU (P, G, F, Inf)`: Essas instâncias são projetadas para cargas de trabalho de computação gráfica, como aprendizado de máquina, mineração de criptomoedas, renderização 3D, e aplicações de streaming de jogos.

6. `Instâncias Arm (A1, M6g, C6g, R6g)`: Essas instâncias são baseadas na arquitetura Arm e são uma opção de baixo custo para cargas de trabalho que requerem um bom desempenho de CPU e suportam a arquitetura Arm.


## Modelos de Preco
Cada Instance Type possui um valor, sendo que quanto mais recursos de vCPU, memoria, disco e rede, mais caro vai ser para utilizar.

A AWS possui alguns modelos de aquisicao:
1. On Demand
2. Saving Plans
3. Spot Instances
4. Host Dedicated
5. Capacidade por Demanda

### On Demand
E o modelo que voce vai no portal da AWS, escolhe o tipo e modelo e pode utilizar, esta modalidade acaba sendo um pouco mais caro pois voce consegue subir maquinas e desliga-las a qualquer momento, pagando somente o que e consumido. O Valor e cobrado por segundo.

### Saving Plans
E o modelo de plano para se economizar, havendo 3 tipos: um para EC2, outro para Sagemaker e um outro para o Fargate. Sendo necessario fechar um contrato com a AWS de 1 a 3 anos.

### Spot Instances
Este modelo, voce paga muito mais barato, podendo chegar ate 90% a menos do que o On Demand, porem a AWS aloca em instancias na qual nao esta sendo utilizada e futuramente a AWS pode alocar o recurso quando necessario. Terminando o servidor. Nao sendo recomendado para utilizacao em producao. Este tipo de modelo e recomendado para ambientes e aplicacoes que poder ser tolerante a falhas, como por exemplo um ambiente de testes para desenvolvimento, teste de aplicacoes, POC interna que nao requer alta disponibilidade para testes entre outros cenarios que nao precisam de alta disponibilidade ou um UP time consideravel.

### Host Dedicated
Como o proprio nome diz, a AWS fornece um host totalmente dedicado, ele e extramente caro devido a alocacao de recurso fisicos. Muito utilizado em empresas do ramo financeiro e governos. Em geral, sao modalidade para empresas e setores que requer que uma parte dos dados nao podem ser compartilhados em rede publica devido compliance de seguranca e normas.

### Capacidade por Demanda
Nao sendo o mais importante, este modelo e um pouco mais barato do que o On Demand, voce solicita a locacao de quantidade de recursos computacionais em um determinado periodo e a AWS sabe quando voce vai alocar o recurso e deixar de utilizar apos o periodo informado.

Para maiores informacoes, consulte o link: https://aws.amazon.com/ec2/pricing/


## Valores do EC2
A AWS cobra por segundos, o valor varia de acordo com cada region, vamos pegar como exemplo uma instance type `t4g.nano`, o valor de `On-Demand hourly rate` e de `$0.0042`, ou seja, se utilizarmos esta instancia no periodo de 1 dia, ela custara `$0.1008`, e em 1 mes, ela custara aproximadamente `$3.1248`.

Lembrando que estes valores sao em dolares, no caso de trabalharmos no Brasil, precisamos converter o valor de dolar em real, ou seja, iriamos pagar R$16.90.

Este valor e apenas para pagar a alocacao da instancia, existem outros valores que precisam ser considerados pois no final, nao iremos pagar apenas este valor de R$16.90.

* Transferencia de dados DENTRO: da Internet para o Amazon EC2: 0,00 USD por GB.

* Transferencia de dados para FORA: do Amazon EC2 para a Internet: 100GB de transferencia de dados gratuitos por mes.

* Primeiro 10 TB/Mes: Contabilizado apos a cota de 100GB sera feito uma cobranca de 0,09 USD por GB.

* Proximos 40 TB/mes: 0,085 USD por GB.

Existem outros custos para transferencia de dados entre outros servicos como CloudFront, outras regions e etc. Sempre consulte a documentacao para obter informacoes mais precisas da cobranca de transferencia e recursos que sera utilizado.

Para maiores informacoes: https://aws.amazon.com/ec2/pricing/on-demand/

### AWS Calculator
A AWS oferece uma calculadora para fazer uma estimativa de custos, acesse o link: https://calculator.aws/.

Como mencionado, esta calculadora e para uma estimativa de custos, pois pode variar de acordo com a utilizacao do ambiente como tambem pelo comportamento da aplicacao. Quanto mais informacoes sobre o ambiente e utilizacao da aplicacao como tambem as transferencias, mais preciso as informacoes da calculadora chegara perto do que sera pago, porem nunca sera o mesmo valor, pois tudo pode variar de acordo com o comportamento da aplicacao no ambiente.


## Iniciando uma Instancia EC2
Para subir uma instancia EC2, acesse o console da AWS, primeiro passo, identifique em qual region voce se encontra, para isso, olhe no canto superior direito, ao lado do seu usuario, voce vera o nome da region. No meu caso, estou em `United State (N. Virginia)`. Apos esta localizacao, acess o servico `EC2` > `Instances`. Clique em `Launch instances`.

`Name`: Insira o nome da Instancia que vai ser exibido na console da AWS.

`Application and OS Images (Amazon Machine Image)`: Selecione uma AMI (Imagem) com o sistema operacional e versao, selecione tambem a arquitetura que deseja fazer o deploy.

`Instance type`: Selecione o tipo de instancia.

`Key pair (login)`: Chave de criptografia que sera utilizada para acesso ao servidor. Importante criar uma chave, pois sem esta chave, voce nao consegue acesso ao servidor.

`Network settings`: Configure a parte de Network como VPC, Subnet, Auto-Assign de Public IP, Security Group em que a instancia fara parte.

`Configure storage`: Configure o(s) disco(s) EBS (Elastic Block Store) para que a maquina possua disco de armazenamento.

`Advanced details`: Nao obrigatorio, porem existem uma serie de configuracoes que podem ser realizadas durante o provisionamento da instancia, como por exemplo um user data que fara uma serie de comandos como por exemplo a instalacao de um apache, NGINX apos o deploy da instancia.

`Number of instances`: Coloque o numero de instancias que deseja criar

Apos inserido todas as informacoes, clique no botao `Launch Instance` para que a instancia seja criada.


### Security Group
O Security group funciona como uma solucao de controle de acesso as portas da EC2, sendo um pouco diferente de um Firewall, pois ele so permite e nao nega acessos como tambem nao registra nenhuma informacao, ele e uma camada a mais na seguranca da rede antes da comunicacao com a EC2.

Aqui estão algumas características principais dos Security Groups na AWS:

1. `Regras de entrada e saída`: Cada security group consiste em um conjunto de regras de entrada e saída. As regras de entrada controlam o tráfego que é permitido chegar à instância associada ao security group, enquanto as regras de saída controlam o tráfego permitido para sair da instância.

2. `Estado de conexão`: Os security groups são "stateful", o que significa que se você enviar uma solicitação de uma instância, a resposta é permitida automaticamente, independentemente das regras de saída.

3. `Permissões por protocolo`: As regras em um security group permitem especificar protocolos permitidos, portas e origem (para tráfego de entrada) ou destino (para tráfego de saída). Isso permite que você restrinja o tráfego para um protocolo ou porta específicos e controle de onde o tráfego é originado ou para onde ele é direcionado.

4. `Flexibilidade e controle`: Você pode associar diferentes security groups a diferentes instâncias e também pode modificar as regras de um security group a qualquer momento. As novas regras são aplicadas automaticamente a todas as instâncias associadas ao security group.

5. `Isolamento de instâncias`: Os security groups ajudam a isolar suas instâncias de outras instâncias na mesma rede, uma vez que as regras são aplicadas por instância e não por sub-rede.

### Alterando um Security Group
Para alteracao de regras no Security Group, acesse o servico `EC2` no console web da AWS, localize no menu esquerdo a secao de `Network & Security` e clique em `Security Groups`, ou na instancia selecionada, clique na guia `Security`, localizando o nome do Security Group que esta vinculado.

Voce pode utilizar o mesmo security group em varias instancias como tambem uma instancia pode conter varios security groups.

Localize qual o security group deseja alterar e clique no respectivel `Security group ID`.

Ao acessar o security group, voce vai localizar o `Inbound rules` e `Outbound rules`. Selecione qual direcao de regra deseja criar a liberacao ou alteracao e clique em `Edit rules`.

Na tela de edicao, clique em `Add rule` para adicionar uma nova regra ou em `Delete` para deletar uma regra ja existente. Repare que ao criar, sera necessario informar algumas coisas basicas como:

`Type`: Tipo de protocolo como TCP, UDP, ICMP, SSH e etc;

`Protocol`: Protoclo de comunicacao TCP ou UDP, repare que ao selecionar um tipo SSH, o Protocol vai ser TCP;

`Port range`: Range ou porta de comunicacao que sera liberado

`Source/Destination`: Origem ou destino no qual sera feito a liberacao, este campo depende de qual direcao (Inbound rules/Outbound rules) voce vai criar. Para criar direcionamento. A liberacao deve ser feito via Network Mask, por exemplo de um para um, utilize o /32, voce pode fazer a permissao entre security group informando o nome do security group ou atraves de uma prfix List.

`Description - optional`: Descricao para identificacao da regra. Mesmo sendo opcional, e sempre bom colocar uma descricao para identificar a regra.

Importante saber que o `Security Group` trabalha com linhas, ou seja, cada linha e uma regra e a `quote` maxima padrao e de 1000. Pode parecer muito em um ambiente pequeno, porem ele cria vai criar uma linha para cada origem e porta, por exemplo:

Tenho que liberar a porta 80 e 443 para os destinos 192.168.10.10, 192.168.10.120 e 192.168.10.30. Em vez do security goup criar duas linhas (uma para o HTTP e outra para o HTTPS) conforme exemplo abaixo:
```
HTTP TCP 80 Custom 192.168.10.10/32, 192.168.10.120/32, 192.168.10.30/32
HTTPS TCP 443 Custom 192.168.10.10/32, 192.168.10.120/32, 192.168.10.30/32
```

Sera criado seis linhas:
```
HTTP TCP 80 Custom 192.168.10.10/32
HTTP TCP 80 Custom 192.168.10.120/32
HTTP TCP 80 Custom 192.168.10.30/32
HTTPS TCP 80 Custom 192.168.10.10/32
HTTPS TCP 80 Custom 192.168.10.120/32
HTTPS TCP 80 Custom 192.168.10.30/32
```



