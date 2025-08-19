# Os 6 pilares do AWS Well-Architected
O AWS `Well-Architected Framework` e o que faz com que o negocio da AWS e seus clientes sejam cada vez maior, e uma estrutura criada pela AWS para ajudar na criacao das Infraestruturas e aplicacoes cada vez mais seguras, eficientes e escalaveis. Sendo um manual no qual possui 6 pilares:
1. Exelencia Operacional
2. Seguranca
3. Confiabilidade
4. Eficiencia e Performance (Desempenho)
5. Otimizacao de custos
6. Sustentabilidade

### Exelencia Operacional
Para conseguirmos uma `Exelencia Operacional`, precisamos primeiramente de um monitoramento, monitorar o ambiente e a base de melhoria continua do ambiente e dos demais processos.

Por exemplo, temos uma automacao, essa automacao precisa fazer o deploy de uma infraestrutura. Neste deploy, utilizamos o Cloud Formation para esta finalidade. E ecenssial utilizar `CloudWatch` para monitorar o que o `Cloud Formation` esta provisionando, para ter uma visibilidade do que esta acontecendo durante o deploy.


### Seguranca
`Seguranca` e um dos principais pilares, pois se nao tiver um bom nivel de seguranca no ambiente, as aplicacoes podem estar expostas e sofrerem ataques, causando problemas financeiros e de imagens. Pensando nisso, de acordo com o `AWS Well-Architected Framework`, precisamos proteger todos os dados, sistemas e qualquer tipo de ativo que temos dentro da estrutura cloud.

* Habilitar `Security Groups` nas instancias.

* Permitir que acesso remoto seja feito apenas por `Bastion Host`

* Aplicar ACL para controlar a entrada e saida de comunicacao entre subnets.

* Habilitar o `AWS Key Management System (KMS)` para gerenciar todas as chaves.

* Gerenciar grupos de acessos, usuarios MFA no `AWS IAM`.


### Confiabilidade
Aumentar a `Confiabilidade` da sua topologia cloud, manter tudo funcionando, tendo certeza que se houver uma falha, o ambiente ainda possui recursos para manter a disponibilidade. Alguns Recursos 

* Estrutura com multiplas `Availability Zone`.

* `Route 53` apontando para servidores primarios e secundarios.

* `Escability` com `Placement Groups`.


### Eficiencia e Performance (Desempenho)
A `Eficiencia e Performance (Desempenho)` e voce nao gastar recursos desnecessarios, fazendo com que seja feito uma devido analise e estudo de desempenho no ambiente, necessidades e configurado para que este ambiente nao tenha tanto um recurso muito grande, quanto tambem o ambiente nao possua alocacao de recursos desnecessarios.

Por exemplo, temos um `auto scaling`, protegendo o ambiente em caso de alta utilizacao e ao mesmo tempo deixando com que o ambiente nao possua recursos alocados desnecessariamente.

Uma outra solucao, criar uma performance adicionando um cache com `Elastic Cache`.


### Otimizacao de custos
A `Otimizacao de custos` e feito com base na utilizacao do ambiente, um estudo para identificar possiveis reducoes de custos e ao mesmo tempo sem impactar na performance e disponibilidade do ambiente.

Por exemplo, visualizar se a instancia precisa ser adquirida como `on demand`, se nao pode ser um `Reserved Instance` pagando menos.

Outro exemplo seria estudar se a aplicacao hospedada no servidor, realmente precisa estar ligada 100% do tempo, se nao pode ser desligado fora do horario comercial ou nos finais de semana, por exemplo um ambiente de desenvolvimento, homologacao que nao requer 100% do tempo ligados.


### Sustentabilidade
Existem algumas empresas que possui como bench marketing a `Sustentabilidade`, focando na reducao do impacto ambiental. Como podemos reduzir um consumo em uma aplicacao. poder olhar para regiao da AWS que utilizam mais energia limpas.


## AWS Cloud Adoption Framework (AWS CAF)
O `AWS CAF` foi criado pela AWS junto com outras empresas e analistas e colocou em um documento. Este framework fala sobre capacidade, controle, compliance e como transformar para a nuvem.

Documentacao: https://aws.amazon.com/pt/cloud-adoption-framework/

Para a prova, nao precisa saber tudo, precisa apenas entender e saber os beneficios

* Reduzir os riscos comerciais

* Melhore a performance ambiental, social e de governanca

* Aumente a receita

* Aumente a eficiencia operacional


## AWS Ecosystem
O `AWS Ecosystem` e um eco sistema que a AWS criou em ao redor dela, para te ajudar como cliente.

Blog que possui tudo o que esta acontecendo na AWS como novidades e melhorias (https://aws.amazon.com/blogs/).

Forum da AWS para perguntas e contato e se comunicar com a comunidade (https://repost.aws/pt).

Existe um portal para whitepapers e guides de como fazer qualquer coisa dentro da AWS (https://aws.amazon.com/pt/whitepapers/)

Partner Solutions (antigamente chamado de Quick Start), sao empresas que criaram solucoes na AWS e podem ajudar outros clientes. (https://partners.amazonaws.com/partners)


## AWS IQ
O `AWS IQ` e um servico para concluir servicos na AWS, que precisam de uma ajuda de outros experts. Voce pode pedir uma ajuda e pagar na plataforma, bem parecido com free lancer, porem com um nivel de conhecimento alto e certificado pela AWS.

Portal: https://iq.aws.amazon.com/


## AWS Managed Services
O `AWS Managed Services` e um servico no qual a empresa quer que a AWS gerencia os servicos da sua empresa, sendo um servico com alto custo, todo o gerenciamento da cloud da sua empresa passa a ser pela AWS. Desde gerenciamento, migracao e implementacao da Cloud passa a ser AWS. Suporte 24/7 nao sendo necessario a preocupacao a equipe ou profissionais altamente qualificados.