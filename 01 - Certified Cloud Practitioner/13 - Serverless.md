## AWS Batch
`Batch` e um grupo de tarefas que devem ser executadas ao mesmo tempo ou em uma sequencia pre definida, processamento em lote, treinamento de modelo de ML analise em qualquer escala.


Link para maiores informacoes: https://aws.amazon.com/pt/batch/


## AWS LightSail
O `Amazon Lightsail` é um serviço de computação em nuvem da Amazon Web Services (AWS) que oferece servidores virtuais privados (VPS), armazenamento, bancos de dados e redes balanceamento de carga a um custo acessível. É projetado para simplificar o lançamento e gerenciamento de aplicações na AWS, especialmente para pequenas empresas, desenvolvedores e estudantes que estão começando a usar a nuvem.

Principais características e funcionalidades do Amazon Lightsail:
1. `Instâncias VPS Previsíveis e Acessíveis`: O Lightsail oferece uma variedade de planos de instâncias com preços fixos e previsíveis que incluem computação, armazenamento e transferência de dados, tornando-o uma opção atrativa para pequenos projetos, sites e aplicações.

2. `Bancos de Dados Gerenciados`: O Lightsail oferece bancos de dados gerenciados que facilitam a configuração, operação e escala de bancos de dados MySQL e PostgreSQL na nuvem.

3. `Gerenciamento Simples de DNS`: Com o Lightsail, você pode gerenciar facilmente os registros DNS do seu domínio diretamente da interface do Lightsail.

4. `Balanceamento de Carga`: O Lightsail oferece balanceadores de carga que distribuem o tráfego entre suas instâncias para melhorar a disponibilidade e a tolerância a falhas de suas aplicações.

5. `Snapshots Automatizados`: O Lightsail permite que você crie snapshots de suas instâncias e bancos de dados para backup, restauração e recuperação de desastres.

6. `Integração com AWS`: Embora o Lightsail seja projetado para ser um serviço simples e autônomo, ele também permite a integração com outros serviços AWS à medida que suas necessidades de aplicação se tornam mais complexas.

7. `Rede Privada Virtual (VPC)`: Cada instância Lightsail roda em uma VPC, oferecendo uma camada adicional de segurança e permitindo um controle granular sobre a visibilidade de suas instâncias.

8. `Scripts de inicialização e Blueprints`: O Lightsail permite que você utilize scripts de inicialização e blueprints para configurar rapidamente novas instâncias com aplicações pré-instaladas.

O Amazon Lightsail é um serviço ideal para quem está começando com a computação em nuvem, oferecendo um ponto de partida simples e de baixo custo para hospedar aplicações, sites, blogs, e outros projetos na AWS.


## AWS Lambda
O Amazon Web Services (AWS) `Lambda` é um serviço de computação que executa seu código em resposta a eventos e gerencia automaticamente os recursos computacionais para você, tornando mais fácil a implantação de aplicações que escalam individualmente em resposta a novas informações.

Algumas características notáveis do AWS Lambda:
1. `Execução de Código sem Servidor`: O AWS Lambda executa o código em um ambiente computacional de alta disponibilidade, o que significa que você não precisa se preocupar em provisionar, escalar, ou gerenciar quaisquer servidores.

2. `Resposta a Eventos em Tempo Real`: Você pode executar seu código em resposta a desencadeadores (triggers), como alterações em um bucket do Amazon S3, atualizações em uma tabela do DynamoDB, solicitações HTTP personalizadas ou até mesmo em novos fluxos de dados no Kinesis.

3. `Escalabilidade Automática`: Sua aplicação escala automaticamente com o AWS Lambda. Quando seu código não está sendo executado, você não paga nada. O serviço gerencia toda a capacidade, patching de segurança, monitoramento e registro de logs.

4. `Personalização de Recursos Computacionais`: Você pode ajustar a quantidade de memória alocada para sua função e o AWS Lambda alocará proporcionalmente a CPU, o disco de E/S e a largura de banda da rede.

5. `Programação em Múltiplas Linguagens`: O AWS Lambda suporta código escrito em JavaScript (Node.js), Python, Java (Java 8 & 11), .NET (C#), Go, Ruby e PowerShell. Também oferece um Runtime API que permite o uso de qualquer linguagem de programação adicional para a criação de funções.

6. `Integração Profunda com a AWS`: O AWS Lambda está integrado ao ecossistema da AWS, o que significa que ele pode ser acionado diretamente por outros serviços da AWS.

7. `Modelo de Preço Baseado em Uso`: Você paga apenas pelo tempo de computação que consome - não há cobrança quando seu código não está sendo executado.

O AWS Lambda é uma ferramenta de computação eficiente e flexível que permite a execução de código sem a necessidade de gerenciar servidores, proporcionando um modelo de desenvolvimento focado em responder a eventos e construir aplicações orientadas a microserviços.


## AWS Fargate
O `AWS Fargate` é um serviço de computação sem servidor para contêineres que permite executar aplicações sem ter que gerenciar a infraestrutura subjacente. Ele funciona com o Amazon Elastic Container Service (ECS) e o Amazon Elastic Kubernetes Service (EKS), simplificando a tarefa de executar contêineres em escala.

Algumas das principais características e funcionalidades do AWS Fargate:
1. `Computação sem Servidor para Contêineres`: Com o AWS Fargate, você não precisa se preocupar com o provisionamento, a configuração e a escalabilidade da infraestrutura de execução dos contêineres. O serviço cuida de todos esses aspectos, liberando você para se concentrar em projetar e construir suas aplicações.

2. `Integração com ECS e EKS`: O Fargate se integra facilmente com o ECS e o EKS, permitindo que você execute tarefas e trabalhos em contêineres de forma eficiente e escalável.

3. `Segurança Isolada`: Cada tarefa ou pod que você executa no Fargate tem seu próprio ambiente isolado de computação, rede e armazenamento, o que aumenta a segurança.

4. `Dimensionamento Flexível`: O Fargate dimensiona automaticamente em resposta à carga de trabalho. Ele pode executar tudo, desde pequenas aplicações de micro-serviços até grandes aplicações de back-end que precisam de muitos recursos.

5. `Preços Pay-as-you-go`: Você paga apenas pelos recursos de computação e memória que seus contêineres precisam quando estão rodando, tornando o Fargate uma opção econômica.

7. `Observabilidade`: O Fargate se integra ao AWS CloudWatch e ao AWS X-Ray, proporcionando insights detalhados sobre o desempenho e a saúde de suas aplicações.

O AWS Fargate é uma opção poderosa e flexível para a execução de aplicações baseadas em contêineres na AWS, eliminando a necessidade de gerenciar a infraestrutura subjacente e permitindo que os desenvolvedores se concentrem em construir aplicações eficazes e eficientes.