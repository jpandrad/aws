# O que e Docker
Docker e uma solucao para criar containers de aplicacoes, criando um isolando das aplicacoes e ao mesmo tempo possibilitando o compartilhamento de recursos fisicos como CPU e memoria da maquina. Ele tambem possibilita que sistemas com bibliotecas em versoes diferentes rode no mesmo servidor.


## ECS
O `Elastic Container Service` e um servico de container da AWS, por baixo e utilizado Docker.

* `TASK` e o arquivo de configuracao (definicao) do container, ele e em formatacao .json;

* A imagem do container e chamada de `Registry` e fica dentro do Servico `Elastic Container Registry (ECR)`;

* A alta disponibilidade dos containers sao feitas a partir do `Auto Scaling Group`;


## Amazon Elastic Kubernetes Service (EKS)
O Amazon Elastic Kubernetes Service (EKS) é um serviço de gerenciamento de contêineres que facilita a execução, escalabilidade e monitoramento de aplicações baseadas em contêineres usando o Kubernetes, um sistema de orquestração de contêineres de código aberto, na plataforma AWS.

Algumas das principais características e funcionalidades do Amazon EKS:
1. `Gerenciamento de Kubernetes`: O EKS remove a complexidade de configurar e operar um ambiente de Kubernetes, permitindo que você se concentre na construção de aplicações.

2. `Compatibilidade com Kubernetes`: O EKS é totalmente compatível com aplicações que rodam em qualquer ambiente padrão do Kubernetes, o que significa que você pode migrar qualquer aplicação padrão Kubernetes para o EKS sem precisar de qualquer modificação.

3. `Integração com a AWS`: O Amazon EKS é profundamente integrado com serviços da AWS, como Amazon RDS, AWS Lambda, Amazon S3 e Elastic Load Balancers, fornecendo uma experiência de usuário consistente em todo o ecossistema AWS.

4. `Segurança`: O EKS executa automaticamente várias tarefas de segurança, como a rotação periódica das chaves de criptografia usadas para proteger os dados armazenados em seus clusters.

5. `Escalabilidade`: Com o EKS, você pode escalonar suas aplicações para lidar com demandas de tráfego pico e para baixo, dependendo das necessidades da aplicação.

6. `Monitoramento e Diagnóstico`: O EKS se integra com o AWS CloudTrail e Amazon CloudWatch, fornecendo monitoramento detalhado, log de eventos e diagnóstico de suas aplicações e clusters de Kubernetes.

7. `Serviço Gerenciado`: O Amazon EKS elimina a necessidade de instalar, operar e dimensionar a infraestrutura de gerenciamento do Kubernetes, simplificando a operação e manutenção de clusters de Kubernetes.

O Amazon EKS oferece uma maneira poderosa, segura e escalável de executar aplicações baseadas em contêineres na AWS, enquanto aproveita as vantagens do Kubernetes como um padrão de facto para a orquestração de contêineres.