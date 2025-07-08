# Escalabilidade, Elasticidade e Disponibilidade
Existem 3 palavras que a AWS gosta de testar o conhecimento:
1. Escalabilidade
2. Elasticidade
3. Disponibilidade

Sao palavras basicas na qual toda a infraestrutura da AWS se baseia em seus servicos. Pois nao existe um motivo de um cliente tentar acessar um servico no qual nao esteja indisponivel, este problema vai afetar qualquer servico de qualquer empresa de qualquer porte.

### Escalabilidade
1. `Vertial`: Estamos falando em alterar o tipo da instancia (Instance Type), a fim de aumentar os recursos computacionais (Memoria, disco, CPU) no ambiente.
2. `Horizontal`: Quando estamos inserido novas instancias no ambiente para poder aumenta a quantidade de recursos computacionais no ambiente. Existe um servico que controla este tipo de acao, ele e chamado de `AutoScaling`, ele sempre funciona com outro servico chamado `Elastic Load Balancer (ELB)`.

### Elasticidade
A `elasticidade` nada mais a capacidade do sistema (aplicacao) se adapatar automaticamente as mudancas no ambiente que o `AutoScaling` proporciona. Estas mudancas podem ser tanto de `load/carga`. O `AutoScaling` pode aumentar ou reduzir a quantidade de servidores de acordo com a carga pre configurada para upgrade ou downgrade do ambiente.

### Disponibilidade
Ambiente sempre disponivel, ou seja, mesmo se houver algum problema em uma Availability Zone por exemplo, se tiver servidores em outras AZs ou Region (dependendo do nivel de criticidade da aplicacao), a aplicacao continua disponivel para o cliente mesmo que nao esteja em nosso alcance a correcao da comunicacao.


## AutoScaling
O sistema de `AutoScaling` e bem simples de ser utilizado, basicamente temos uma quantidade de usuarios que deseja acessar a aplicacao da empresa, ele acessa com o computador dele e acessa uma URL (endereco do site), do lado nosso, precisamos de 1 servidor, no qual ele hospeda a aplicacao e quer adicionar uma escabilidade maior, em vez de apenas um unico servidor, precisamos criar um `Grupo de AutoScaling`. Para isso precisamos das seguintes etapas:

1. `Criar um modelo de Instancia`: Este modelo devera conter todas as informacoes sobre a configuracao do Instance Type e script de userdata para instalacao e configuracao da aplicacao.
2. `Criar o AutoScaling`: Definir as configuracoes e metricas de quantidade de servidores e tresholds para aumentar/diminuir a escabilidade Horizontal no ambiente, sendo possivel subir em outra AZ de disponibilidade. Ele tambem foi criado para que caso os servidores nao estejam devidamente sendo utilizados, ele destroi ate manter o numero minimo de servidores configurados, este processo e chamado de `Scaling Out` e `Scaling In`

* `Scaling Out`: Quando o servico do `AutoScaling` insere novas instancias no ambiente.

* `Scaling In`: Quando o servico do `AutoScaling` remove instancias do ambiente.

Documentacao: https://docs.aws.amazon.com/autoscaling/plans/userguide/how-it-works.html

Aqui estão algumas características principais do Amazon Auto Scaling:
1. `Dimensionamento Automático`: O Auto Scaling permite que você defina políticas de dimensionamento que ajustam automaticamente a capacidade de recursos com base nas condições definidas. Por exemplo, você pode dimensionar automaticamente o número de instâncias do Amazon EC2 para atender à demanda de tráfego.

2. `Otimização de Custo e Performance`: Ao ajustar continuamente a capacidade, o Auto Scaling ajuda a melhorar a disponibilidade e minimizar os custos. Quando a demanda aumenta, o Auto Scaling adiciona automaticamente mais recursos. Quando a demanda diminui, ele remove os recursos desnecessários para economizar dinheiro.

4. `Balanceamento de Carga`: O Auto Scaling pode ser usado junto com o Elastic Load Balancing (ELB) para distribuir o tráfego de aplicações entre várias instâncias EC2 para melhorar a disponibilidade e a tolerância a falhas.

5. `Saúde da Aplicação`: O Auto Scaling realiza verificações de saúde em suas instâncias EC2 e substitui automaticamente as instâncias que não estão saudáveis.

6. `Integração AWS`: O Auto Scaling está integrado com uma série de serviços da AWS, incluindo Amazon CloudWatch, Amazon SNS, AWS CloudFormation, entre outros.

7. `Flexibilidade`: O Auto Scaling permite dimensionar vários recursos, não se limitando apenas às instâncias EC2. Você também pode dimensionar serviços como Amazon DynamoDB, Amazon Aurora, Amazon ECS, e Amazon RDS.


## ELB e ALB
Nao podemos falar de AutoScaling e alta disponibilidade sem falarmos de `Elastic Load balancer (ELB)`. O ELB e responsavel por fazer o balanceamento de carga entre os servidores que estao na AWS com o cliente. o ELB precisa saber quem sao os WebServers que estao dentro de um `AutoScaling Group (ASG)` para que quando o ASG crie novos servidores, ele notifique o ELB que existem novos servidores no pool.

Abaixo, os tipos que temos de Load Balancer na AWS:
1. `Aplication Load Balancer (ALB)`
2. `Network Load Balancer (NLB)`
3. `Gateway Load Balancer (GLB)`

Os mais utilizado e o ALB para balanceamento de carga em aplicacoes e o NLB que realiza o balanceamento de carga a nivel de servidor. O GLB e um tipo de load balancer para ser utilizado em Load Balancers de terceiros.

Aqui estão algumas características principais do ELB:
1. `Tipos de Balanceador de Carga`: O ELB oferece três tipos de balanceadores de carga que se adequam a diferentes necessidades de aplicação - o Balanceador de Carga de Aplicação (ALB) para tráfego HTTP e HTTPS, o Balanceador de Carga de Rede (NLB) para tráfego TCP, UDP e TLS, e o Classic Load Balancer para tráfego HTTP, HTTPS, TCP e SSL.

2. `Alta disponibilidade`: O ELB distribui automaticamente o tráfego em várias instâncias em várias zonas de disponibilidade para garantir a continuidade do serviço, mesmo se uma ou mais instâncias falharem.

3. `Escalabilidade`: O ELB escala automaticamente a sua capacidade de balanceamento de carga em resposta ao tráfego de entrada.

4. `Integração com o Auto Scaling`: O ELB trabalha em conjunto com o Auto Scaling da AWS para garantir que há capacidade suficiente para atender ao tráfego de entrada e para substituir as instâncias que falham.

5. `Segurança`: O ELB oferece recursos de segurança como a integração com o AWS Certificate Manager para SSL/TLS, e a integração com o AWS Identity Access Management (IAM) para controle de acesso.

6. `Monitoramento e Auditoria`: O ELB integra-se com o Amazon CloudWatch e o AWS CloudTrail para monitorar o desempenho de suas aplicações e registrar as ações realizadas no seu balanceador de carga.


## Criando um modelo de execucao
Primeiro precisamos criar um `AutoScaling` e dentro da criacao, iremos fazer a criacao de um ELB usando o tipo ALB (Aplication Load Balancer).

No Painel de EC2, acesse `Instances` > `Launch Templates`. Nesta opcao iremos criar um modelo para as instancias. Clique no botao `Create launch template`.

* `Launch template name - required`: Nome do Template.

* `Template version description`: Descricao para este template.

* `Application and OS Images (Amazon Machine Image)`: Selecione a imagem (AMI) na qual sera provisionada.

* `Instance type`: Tipo que as instancias seram criadas.

* `Key pair (login)`: Chave de criptografia que sera utilizada para acesso aos servidores.

* `Security groups`: Informe o grupo de seguranca que sera utilizado.

* `Storage (volumes)`: Configure o disco EBS conforme necessidade.

* `Advanced details` > `User data - optional`: Crie um script que fara toda a configuracao da instancia apos a criacao. Para exemplo, pode utilizar o script abaixo:
```shell
#!/bin/bash
# Update packages and install necessary software
yum update -y
yum install -y httpd
amazon-linux-extras install -y epel
yum install -y jq

# Enable and start Apache web server
systemctl enable httpd
systemctl start httpd

# Get a token for accessing instance metadata
TOKEN=$(curl -s -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")

# Get instance metadata including the availability zone
INSTANCE_ID=$(curl -s -H "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/latest/meta-data/instance-id)
AVAILABILITY_ZONE=$(curl -s -H "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/latest/meta-data/placement/availability-zone)

# Create an index.html file
cat > /var/www/html/index.html <<EOF
<!DOCTYPE html>
<html>
<head>
    <title>Instance Details</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f0f0f0;
        }
    </style>
</head>
<body>
    <h1>Instance Details</h1>
    <p><strong>Instance ID:</strong> ${INSTANCE_ID}</p>
    <p><strong>Availability Zone:</strong> ${AVAILABILITY_ZONE}</p>
</body>
</html>
EOF

# Set the appropriate permissions
chmod 644 /var/www/html/index.html
```

> [!NOTE]  
> O Script fara a atualizacao do sistema operacional, instalacao e habilitar o servico WebServer Apache e em seguida, pegara algumas informacoes da instancia e colocara em uma pagina Web. Este exemplo seria uma base de configuracao do user data.

Apos inserido as informacoes, revive em `Summary` e se estiver tudo correto, clique no botao `Create launch template`.

Com o `Launch Template` criado, vamos criar um `AutoScaling Group`, para isso, no painel de EC2, acesse `AutoScaling` > `Auto Scaling Groups`. Clique no botao `Create Auto Scaling group`. Existem 7 etapas para a criacao do `AutoScaling Group`:

1. `Choose launch template or configuration`: Nesta etapa, precisamos informar o nome do `AutoScaling Group` e qual `Launch template` sera utilizado, voce tambem pode alterar a versao do modelo que sera utilizado.

2. `Choose instance launch options`: Nesta segunda etapa, iremos escolher as opcoes de execucao da instancia, selecione em qual `VPC` as instancias seram criadas e em `Availability Zones and subnets`, selecione quais subnetes elas seram criadas. Podemo utilizar apenas uma unica subnet, porem o recomendado e utilizar em mais de uma, pois se houver algum problema de indisponibilidade na AZ, o servico continuara disponivel para os clientes.

3. `Integrate with other services`: Nesta etapa iremos criar o nosso load balancer, podemos subir o `AutoScaling` sem o balanceador de carga, no qual nao faria muito sentido, pois queremos o `AutoScaling` para termos alta disponibilidade e elasticidade no ambiente, podemos selecionar um balanceador de carga ja existente ou criar um novo. Ao criar um novo, voce pode selecionar um `ALB` ou `NLB`. Configure o Loadbalancer conforme necessidade da aplicacao.

4. `Configure group size and scaling`: Nesta etapa iremos configurar o tamanho do grupo. Sendo extremamente importante, precisamos informar a quantidade desejada de instancias em `Desired capacity`, em `Scaling`, iremos informar a quantidade minima de instancias que queremos no ambiente `Min desired capacity` e a maxima de instancias em `Max desired capacity`. Em `Automatic scaling - optional`, podemos configurar uma politica com metricas para elasticidade do ambiente baseado em utilizacao de memoria/cpu e etc.

5. `Add notifications`: Nesta etapa, voce pode adicinar notificacoes.

6. `Add tags`: Nesta etapa, voce pode adicinar Tags.

7. `Review`: Etapa para revisao das configuracoes, caso esteja tudo certo, clique no botao `Create Auto Scaling group`.

Apos clicado no botao `Create Auto Scaling group`, eo ambiente sera provisionado automaticamente, voce pode acompanhar o andamento nas secoes de `Instances`, `Load balancers` e em `Auto Scaling groups`.


### Removendo os recursos
Para finalizar o ambiente, sera necessario excluir em uma ordem especifica, caso ao contrario, o servico de `AutoScaling` provisionara os recursos novamente. Para isso, siga a seguinte ordem:
1. `Auto Scaling Groups`: Acesse `Auto Scaling` > `Auto Scaling Groups`, selecione o Auto Scaling Groups e clique em `Actions` > `Delete`.

2. `Load Balancer`: Acesse `Load Balancing` > `Load Balancers`, selecione o Load Balancer e clique em `Actions` > `Delete load balancer`.

3. `Target Groups`: Acesse `Load Balancing` > `Target Groups`, selecione o Target Groups e clique em `Actions` > `Delete`.

4. `Instances`: Acesse `Instances` > `Instances`, selecione as Instancias e clique em `Instance state` > `Terminate (delete) instance`.

5. `Launch Templates`: Acesse `Instances` > `Launch Templates` , selecione o Launch Template e clique em `Actions` > `Delete template`.

Por seguranca, aguarde alguns minutos e faca uma nova revisao para confirmar que todos os recursos foram apagados corretamente.