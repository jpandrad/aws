## Route53
O `Route53` e basicamente o servico de DNS (Domain Name System), fazendo o servico de traducao dominio para enderecamento IP

## Route53 Policies
A vantagem em utilizar o `Route53` e uma politica de roteamento, chamado de `Policies`, abaixo a lista necessarias para o exame:

* `Simple route`: Roteamento simples no qual o cliente faz a requisicao para o Route53 e ele retorna para o cliente o enderecamento IP.

* `Failover routing policy`: A politica e baseado em caso de falha ou indisponibilidade, comutando para outra conexao. Por Exemplo, o `Route53` possui visibilidade de 3 instancias. Caso a principal venha a ficar indisponivel, ele envia as requisicoes para as demais instancias. Configurando um Heath Check.

* `Latency routing policy`: Politica de rota baseado na latencia, possibilitando que o usuario se comunique as instancias mais proximas, por exemplo, temos um usuario nos estados unidos, a empresa possui possui instancias no Reino Unido, Brasil e Mexico. O Route53 verifica dentre os ambientes, direcionando as conexoes do usuario para a instancia com o menor tempo de latencia.

* `Weighted routing policy`: O Roteamento e feito baseado em peso, ou seja, e feito um balanceamento nas requisoces a fim de mandar cada um para um endereco, por exemplo, O cliente 1 faz a consulta do endereco, o Route53 retorna o endereco da instancia 1, o segundo cliente, solicita a resolucao do nome para a mesma aplicacao, em vez do route53 responder com o IP da instancia 1, ele responde o endereco IP da instancia 2. Podendo tambem ser criado um balanceamento de requisicoes para os servicos de Ec2.

Existem outras policies, para consultar, acesse o link da documentacao abaixo:

Documentacao: https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html


## Sobre AWS CloudFront
O Amazon CloudFront é um serviço de rede de entrega de conteúdo (CDN) rápido e altamente seguro oferecido pela Amazon Web Services (AWS). Ele distribui dados, vídeos, aplicativos e APIs para os espectadores dos usuários com baixa latência e altas velocidades de transferência.

Algumas características do Amazon CloudFront:
1. `Desempenho melhorado`: O CloudFront melhora o desempenho dos aplicativos, acelerando a entrega de conteúdo para os usuários finais. Isso é feito através do uso de uma rede global de pontos de presença (PoPs) que roteiam o conteúdo para o usuário a partir do local mais próximo.
2. `Segurança robusta`: O CloudFront oferece uma segurança robusta com integração ao AWS Shield, AWS Web Application Firewall (WAF) e Route 53 para ajudar a proteger seu aplicativo contra vários tipos de ataques. Ele também suporta a entrega segura de conteúdo através de HTTPS e integra-se ao AWS Certificate Manager para facilitar o gerenciamento de certificados SSL/TLS.
3. `Escalabilidade`: Como parte da AWS, o CloudFront pode escalar automaticamente para lidar com tráfego alto sem necessidade de intervenção manual.
4. `Personalização`: Com o CloudFront, você pode personalizar e otimizar o desempenho da entrega de conteúdo com base nas necessidades específicas do seu aplicativo.
5. `Integração com a AWS`: O CloudFront está profundamente integrado com outros serviços da AWS, como o S3, EC2, Elastic Load Balancer (ELB) e Route 53, o que facilita a entrega de conteúdo de várias fontes.
6. `Custo Efetivo`: O CloudFront usa um modelo de preços pay-as-you-go, onde você paga apenas pelo que usa. Além disso, há opções para economizar dinheiro ao se comprometer com um determinado nível de uso.


## S3 Transfer Acceleration
O Amazon S3 Transfer Acceleration é um recurso do Amazon S3 que permite a transferência rápida e segura de arquivos por longas distâncias entre o cliente e um bucket do S3. Este serviço utiliza a rede global da Amazon CloudFront para acelerar as transferências de upload e download para o S3.

Algumas características do S3 Transfer Acceleration:
1. `Velocidade aprimorada`: Este serviço é especialmente útil quando se precisa transferir grandes quantidades de dados de forma rápida e eficiente de um lugar distante para um bucket do S3.
2. `Facilidade de uso`: Ativar a Transfer Acceleration é tão simples quanto marcar uma caixa na configuração do bucket do S3. Não é necessário alterar o código da aplicação.
3. `Utiliza a Rede da Amazon CloudFront`: O serviço usa a infraestrutura de borda otimizada para latência da Amazon CloudFront, que tem pontos de presença (PoPs) em todo o mundo para rotear dados pela rede da AWS.
4. `Custo Eficiente`: Com a Transfer Acceleration, você paga apenas pelo que usa. No entanto, é importante notar que este serviço é cobrado além das taxas padrão de solicitação e armazenamento do S3.
5. `Segurança`: Assim como o S3, a Transfer Acceleration suporta a transferência de dados por HTTPS, oferecendo o mesmo nível de segurança dos dados em trânsito.

O S3 Transfer Acceleration é uma solução eficiente quando se precisa transferir grandes volumes de dados por longas distâncias. Ele maximiza a velocidade de transferência de dados, melhorando o desempenho e a eficiência das operações de negócios que envolvem o S3.

## AWS Global Accelerator
O AWS Global Accelerator é um serviço que melhora a disponibilidade e o desempenho de suas aplicações para usuários em todo o mundo. Ele faz isso usando a rede global altamente disponível da AWS e redirecionando o tráfego de usuários para a aplicação mais próxima em termos de latência. Isso resulta em uma melhoria significativa na experiência do usuário.

Algumas características do AWS Global Accelerator:
1. `Desempenho aprimorado`: O Global Accelerator melhora a velocidade de conexão e a latência para as aplicações da AWS, tornando-as mais rápidas e responsivas para os usuários, não importa onde eles estejam localizados.
2. `Alta Disponibilidade`: Utilizando a rede global da AWS, o Global Accelerator oferece uma alta disponibilidade, direcionando os usuários para a instância mais saudável da aplicação.
3. `Fácil de configurar`: Basta escolher os recursos da AWS que deseja acelerar, e o AWS Global Accelerator cuida do restante.
4. `Segurança aprimorada`: Com o Global Accelerator, você cria um único ponto de entrada para as suas aplicações, o que pode ser útil para configurações de segurança e firewall.
5. `Escalabilidade`: O serviço se adapta automaticamente às mudanças no tráfego de aplicação, o que o torna útil para cenários de alto tráfego ou para aplicações com padrões de tráfego imprevisíveis.

O AWS Global Accelerator é uma solução útil para melhorar a velocidade, a disponibilidade e a segurança de aplicações na AWS, proporcionando uma experiência de usuário mais suave e agradável.