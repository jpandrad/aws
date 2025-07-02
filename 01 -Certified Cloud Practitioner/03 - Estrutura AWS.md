## Infraestrutura Global da AWS
A AWS possui uma infraestrutura global com varios datacenters espalhados pelo mundo.

Atualmente ela possui

* 37 Regions;

* 117 Availability Zones;

* 700+ CloudFront POP e 13 regional edge caches;

* 43 Local Zones;

Para maiores informacoes, acesse o endereco: https://aws.amazon.com/about-aws/global-infrastructure/

### Regions
Uma `Region` sao regioes localizadas em uma determinada area do mundo, a `Availability Zone` sao datacenters proximos dentro de uma `Region`, estes datacenter sao utilizados como mecanismos de backup em caso de falhas.

Um `Local Zone` sao datacenters menores que estao conectados diretamente com as `Availability Zones`.

Por exemplo, a AWS possui uma Region chamada `us-east`, localizado em North Virginia na america do norte (Estados Unidos), esta region possui um codigo de `us-east-1`, sendo que o `us-east` siginifica a regiao e o codigo `1`, o numero do datacenter, se consultado Ohio, podemos ver que o codigo e `us-east-2`. Dentro de North Virginia (us-east-1), ela possui 3 `Availability Zone`. Podemos dizer que North Virginia, possui 3 Datacenters.

### Local Zones
Uma `Local Zone` e uma especie de implantacao de infraestrutura proxima ao cliente, permitindo que alguns servicos de armazenamento, banco de dados e alguns outros produtos da AWS, reduzindo a latencia de entrega das informacoes. Essas zonas podem ser locacao de datacenters de terceiros.

### AWS Wavelenght
O `AWS Wavelenght` e uma oferta de infraestrutura otimizada para aplicacoes moveis de computacao de borda. As zonas sao implantacoes de infraestrutura da AWS com servico de computacao e armazenamento da AWS incorporados nas redes 5G dos provedores de servicos de comunicacao (CSP), para que o trafego de aplicacoes de dispositivos 5G acesse os servidores de aplicacoes em execucao nas zonas Wavelenght sem sair da rede de telecomunicacao. Evitando a latencia que resultaria do trafego de aplicacoes atravesse varios saltos na internet para chegar ao seu destino.

### AWS Outposts
O `AWS Outposts` leva os produtos, em qualquer datacenter ou espaco.


## AWS Share Responsability Model
A AWS e sua empresa compartilham alguams responsabilidades, voce como empresa (conta pessoal), tem a responsabilidade da estrutura Cloud e a AWS possui uma outra responsabilidade.

Basicamente a AWS e responsavel pela parte de:

`Software`
1. Compute
3. Storage
4. Database
5. Networking

`Hardware/AWS Global Infrastructure`
1. Regions
2. Availability Zones
3. Edge Locations

Isso quer dizer que nao e necessario nenhuma preocupacao em suporte, seguranca que afetem estes itens.

As suas responsabilidades como "Customer" sao:
1. Customer Data
2. Plataform, application, Identity & Access Management
3. Operating System, Network & Firewall Configuration
4. Client Side Data Encryption & Data integrity Authentication
5. Server-side Encryption (File System and/or data)
6. Networking Traffic Protection (Encryption, Integrity, Identity) 


Para maiores informacoes, consulte o link: https://aws.amazon.com/compliance/shared-responsibility-model/