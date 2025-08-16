## AWS Control Tower
O `AWS Control Tower` e um servico para empresas que utilizam servicos da AWS em grande escala, empresas que possuem multiplas contas.

Em estruturas muito grande, e normal segmentar ambientes de Billing, Security, Network, Workload (Aplicacao) em contas diferentes em vez de segmentar tudo em uma unica conta, facilitando o gerenciamento e acessos aos recursos da conta em especifico.

Em ambientes que possuem esta estrutura, exitem a necessidade de configurar servicos em uma conta
- AWS Config
- Cloud Trail (Auditoria)
- S3

O `AWS Control Tower` simplifica o processo de criacao de multiplas contas dentro de uma organizacao.


## AWS Resource Access Manager (AWS RAM)
O `AWS RAM` ele funciona dentro de uma estrutura com organization (organizacao), possibilitando o compartilhamento de recursos entre accounts.

Documentacao: https://docs.aws.amazon.com/ram/latest/userguide/what-is.html

Por exemplo, tenho uma `Organization` com contas para `dev` e `system` e uma instancia da conta de `system` precisa acessar a instancia na conta de `dev`. O RAM possibilita extender a subnet da conta `dev` para a conta `system` com restricoes.

A vantagem e habilitar a conectividade entre duas contas, nao alterando o privilegio e permissoes das contas configuradas.


## AWS Service Catalog
O `AWS Service Catalog` é um serviço de gerenciamento de serviços que permite que organizações criem e gerenciem catálogos de serviços de TI aprovados para uso na AWS.

Algumas das principais características e funcionalidades do AWS Service Catalog:
1. `Governança e Controle`: O AWS Service Catalog permite que administradores de TI mantenham um controle firme sobre os serviços da AWS utilizados dentro de suas organizações. Eles podem especificar quais serviços os usuários têm permissão para lançar, implementar controles de custos e garantir que todas as implementações estejam em conformidade com as políticas corporativas.

2. `Autoatendimento`: Usuários podem navegar pelos catálogos de serviços aprovados e lançar os serviços que precisam por conta própria, sem precisar de assistência direta da equipe de TI.

3. `Padronização de Serviços`: O AWS Service Catalog permite criar e gerenciar portfólios de produtos que são aprovados para uso na organização. Isso ajuda a garantir que os serviços lançados pelos usuários estejam de acordo com as melhores práticas e políticas da organização.

4. `Integração com Outros Serviços AWS`: O AWS Service Catalog se integra com outros serviços AWS, como AWS CloudFormation, AWS Identity and Access Management (IAM), AWS Config, entre outros.

5. `Controle de Custo e Orçamento`: Ao restringir quais serviços podem ser lançados e como eles são configurados, o AWS Service Catalog pode ajudar as organizações a manterem o controle dos custos e a garantirem que os recursos da AWS são usados de forma eficiente.

6. `Rastreamento e Auditoria`: O AWS Service Catalog rastreia o uso de serviços, o que facilita a auditoria e o cumprimento dos requisitos de conformidade.

O AWS Service Catalog é uma ferramenta para organizações que precisam manter um controle rigoroso sobre o uso dos serviços da AWS, enquanto permitem que os usuários acessem e lancem os serviços de que precisam de forma autônoma.


## AWS Trusted Advisor
O `AWS Trsuted Advisor` e um servico muito utilizado por empresas grandes, pode tambem ser adquirido por outras empresas. O `AWS Trsuted Advisor` e um especialista dentro da AWS que ajuda a reduzir custos dentro da empresa, melhorar a performance, seguranca e tolerancia a falha.