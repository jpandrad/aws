## Amazon Cognito
O `AWS Cognito` e um servico que oforece uma 

Por exemplo, voce tem uma aplicacao Web ou Mobile e ela requer algum tipo de login. O `AWS Cognito` tem uma base de dados propria que armazena os usuarios e senhas. Uma grande e que podemos utilizar o Social Identity Provider (SIP), autenticacao baseada em servicos como Google, Facebook, Icloud e etc. Perfeito para gerenciamento de usuarios e senhas em uma grande quantidade.


## Amazon STS
O `Amazon STS` (Security Token Service) e um servico para gerar e gerenciar tokens de acesso.

Por exemplo, temos uma instancia EC2 e esta EC2, precisa acessar o S3. Normalmente criamos uma `IAM Role`, por baixo esta `IAM Role` cria um token que define um acesso temporario. Este Token e gerado pelo `STS`.

O S3 tambem faz o uso do `STS`, por exemplo, se tentarmos abrir uma imagem direto no S3, ele nao deixar, ao clicar no botao `Abrir`, voce conseguira ver a imagem na tela, se reparar na URL da imagem, existe uma informacao `Amz-Security-Token`, ou seja, o S3 solicitou ao servico do `STS` gerar um Token, o `STS` gerou um token temporario para poder ter acesso a imagem.


## AWS Device Farm
O `AWS Device Farm` e um servico especifico para desenvolvedor, que precisam testar uma aplicacao Web ou mobile no qual precisa ser testado em varios dispositivos.


## AWS AppSync
O `AWS AppSync` e um servico que faca uma syncronizacao entre uma aplicacao Web e uma aplicacao Mobile. O `AWS AppSync` utiliza uma tecnologia desenvolvida pelo Facebook chamada `GRAPHQL`, ela e utilizada para gerar codigos automaticamente vinda do cliente, garantindo tudo o que e digitado no APP, ele sincroniza com o portal Web. Fazendo integracao com banco de dados como `DynamoDB`.


## AWS Amplify
O `AWS Amplify` ajuda contruir aplicacoes Mobile.


## AWS IoT Core
O `AWS IoT` significa Internet of Things, este servico e utilizado para conectar devices a cloud, por exemplo, dispositivos com telefone, geladeira, carro ou qualquer outra coisa que seja "smart" e precisa se conectar aos servicos da AWS por exemplo, S3, Sage Maker, Lambda. Ele vai ser a ponte de conexao entre os dispositivos com a Cloud. Este servico e serverless e pode processar (fazer a conexao) de bilhoes de dispositivos e trilhoes de mensagens.


## AWS Step Functions
O `AWS Step Functions` e uma solucao que possibilita ordenar e coordenar funcoes que devem seguir em uma sequencia. Muito utilizado com interversao humana ou nao, por exemplo um Web Site de vendas e estoque, criando workflows.

- `Parallel State`: Dois estagios que vao ser executado no mesmo ponto

- `Sequence`: Sequencia de iniciar > Executar.


## Amazon AppFlow
O `Amazon AppFlow` e uma solucao para transferencia segura entre aplicacoes `software-as-a-service (SaaS)`, voce cria APIs que recebe de sources como SalesForce, CRM, ZenDesk, Slack e etc, e envia para destinos como S3, RedShift, Google Analytics, SalesForce e etc. Podendo ser criado por demanda, eventos, Schedules e etc. Possibilitando criar filtros, organizar e validar os dados dentro do `AppFlow`. Toda a transferencia e feito de modo seguro e toda a comunicacao passa ser encrypted.


## AWS Backup
O `Amazon AWS Backup` é um serviço centralizado para fazer backup e restaurar dados em toda a AWS. Com o AWS Backup, os usuários podem configurar políticas de backup de acordo com seus requisitos de negócios e garantir a conformidade regulatória e de políticas.

Principais características e funcionalidades do Amazon AWS Backup:
1. `Centralizado e Automatizado`: O AWS Backup permite que você centralize e automatize a proteção de dados em vários serviços da AWS, incluindo Amazon EBS, Amazon RDS, Amazon DynamoDB, Amazon EFS, Amazon EC2, AWS Storage Gateway e AWS Fargate.

2. `Políticas de Backup`: O serviço permite definir políticas de backup personalizadas, como frequência e retenção de backup, de acordo com suas necessidades e regulamentos de conformidade.

3. `Recuperação`: O AWS Backup oferece recuperação de ponto no tempo, o que significa que você pode restaurar seus dados para um ponto específico no tempo.

4. `Segurança e Conformidade`: Com o AWS Backup, você pode proteger seus backups com criptografia, gerenciar o acesso de backup com políticas do IAM e auditar suas atividades de backup com AWS CloudTrail.

5. `Monitoramento e Alerta`: O AWS Backup se integra com o AWS CloudWatch, oferecendo a capacidade de monitorar métricas de backup e receber alertas.

7. `Gerenciamento de Custo`: Com AWS Backup, você paga apenas pelo armazenamento que usa, ajudando a otimizar os custos de armazenamento de backup.

8. `Escalabilidade`: O AWS Backup é capaz de lidar com demandas crescentes de backup sem a necessidade de provisionar, configurar e gerenciar infraestrutura adicional.

O `Amazon AWS Backup` é uma solução eficiente e segura para gerenciar backups e restaurações de vários serviços AWS, proporcionando flexibilidade, automatização e conformidade com políticas.


## AWS Disaster Recovery Strategy
O `AWS Disaster Recovery (DR)` refere-se ao conjunto de estratégias e procedimentos implementados na plataforma AWS para proteger os dados e os sistemas de TI de uma organização contra desastres. Esses desastres podem ser naturais ou causados pelo homem e podem resultar em perda de dados, interrupção do serviço ou falha do sistema.

As soluções de recuperação de desastres da AWS são projetadas para minimizar o tempo de inatividade e a perda de dados após um desastre, permitindo que as organizações recuperem rapidamente suas operações normais. A AWS oferece vários serviços e recursos que facilitam a implementação de estratégias eficazes de recuperação de desastres, incluindo:

1. `AWS Backup`: um serviço que ajuda a centralizar e automatizar backups em vários serviços da AWS.

3. `Amazon S3`: um serviço de armazenamento que pode ser usado para armazenar e recuperar qualquer quantidade de dados a qualquer momento.

4. `Amazon EBS Snapshots`: que pode ser usado para fornecer backups pontuais de seus volumes de dados.

5. `Amazon RDS`: que suporta backups automatizados de instâncias de banco de dados.

6. `AWS CloudFormation`: um serviço que ajuda a modelar e provisionar recursos da AWS.

7. `Amazon Route 53`: um serviço de DNS que pode ser usado para rotear o tráfego de usuários para diferentes regiões da AWS.

8. `AWS Direct Connect`: um serviço que proporciona uma conexão de rede dedicada do seu local para a AWS.

A escolha da estratégia de recuperação de desastres na AWS (por exemplo, backup e restauração, recuperação de área de trabalho quente, recuperação de área de trabalho fria, recuperação piloto de luz) depende das necessidades específicas de cada organização, incluindo seus objetivos de tempo de recuperação (RTO) e objetivos de ponto de recuperação (RPO).

A AWS oferece uma ampla variedade de ferramentas e serviços que podem ser usados para implementar uma estratégia de recuperação de desastres robusta, ajudando as organizações a proteger seus dados e sistemas críticos contra interrupções imprevistas.


## AWS WorkSpaces
`Amazon AWS WorkSpaces` é um serviço gerenciado de desktop como serviço (DaaS), que permite provisionar desktops na nuvem para os usuários acessarem a qualquer hora, de qualquer lugar, usando qualquer dispositivo suportado. Este serviço é uma solução virtual de substituição de desktop que ajuda a reduzir os custos operacionais e melhorar a segurança dos dados.

Principais características e benefícios do AWS WorkSpaces incluem:
1. `Escalabilidade e Flexibilidade`: O AWS WorkSpaces permite provisionar o número exato de desktops de que você precisa e escalar para cima ou para baixo conforme as necessidades da sua organização mudam.

2. `Acesso em Qualquer Lugar`: Os usuários podem acessar os desktops do WorkSpaces de qualquer lugar usando o cliente de desktop AWS WorkSpaces, que suporta vários tipos de dispositivos, incluindo Windows e MacOS, iPads, tablets Kindle Fire e dispositivos Android.

3. `Segurança`: O AWS WorkSpaces ajuda a melhorar a segurança dos dados, uma vez que todos os dados são armazenados na AWS, e não no dispositivo do usuário final. Ele também suporta criptografia de dados e integra-se ao AWS Key Management Service.

4. `Gerenciamento Simplificado`: O AWS WorkSpaces elimina a necessidade de provisionar, implantar e gerenciar hardware complexo, proporcionando um ambiente de desktop gerenciado.

6. `Integração`: O serviço se integra ao Active Directory, permitindo que os usuários mantenham suas credenciais existentes para acessar seus WorkSpaces.

7. `Custo Efetivo`: Com o AWS WorkSpaces, você paga apenas pelo número de WorkSpaces que usa. Não há custos iniciais ou compromissos de longo prazo.

O `AWS WorkSpaces` é uma solução eficaz e segura para fornecer desktops virtuais que podem ser acessados de qualquer lugar, ajudando as organizações a reduzir os custos operacionais e a melhorar a segurança dos dados.


## AWS AppStream 2.0
`Amazon AppStream 2.0` é um serviço gerenciado da Amazon Web Services (AWS) que permite o streaming seguro de aplicativos de desktop para usuários sem reescrever esses aplicativos para a nuvem. Basicamente, o AppStream 2.0 fornece aos usuários acesso instantâneo a aplicativos de desktop por meio de um navegador da web.

Principais características e benefícios do Amazon AppStream 2.0 incluem:
1. `Acesso de qualquer lugar`: Com o AppStream 2.0, os usuários podem acessar os aplicativos de que precisam a partir de qualquer computador compatível com HTML 5, incluindo Chromebooks, Macs e PCs.

2. `Escala com demanda`: O AppStream 2.0 escala automaticamente para acomodar qualquer número de usuários em todo o mundo, sem que você precise provisionar, implantar e gerenciar infraestruturas.

3. `Segurança aprimorada`: Como os aplicativos são transmitidos a partir da AWS, os dados sensíveis nunca saem do seu VPC na nuvem, aumentando a segurança e a conformidade.

4. `Economia de custos`: Você paga apenas pelo que usa, com tarifação por usuário por hora. Não há compromissos iniciais ou de longo prazo.

6. `Gerenciamento Simplificado`: Você pode gerenciar seus aplicativos centralmente na AWS sem a necessidade de se preocupar com o provisionamento de infraestrutura, atualizações de software, patches de segurança e outras tarefas de gerenciamento de TI.

7. `Performance otimizada`: O AppStream 2.0 utiliza a tecnologia de streaming de alta qualidade da AWS, o que proporciona aos usuários uma experiência de desktop interativa e responsiva.

O `Amazon AppStream 2.0` é uma solução poderosa e flexível que permite às organizações transmitir aplicativos de desktop de maneira segura e eficiente para qualquer usuário, em qualquer lugar, reduzindo os custos de TI e melhorando a segurança dos dados.