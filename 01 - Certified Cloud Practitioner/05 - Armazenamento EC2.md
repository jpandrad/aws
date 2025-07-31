## Sobre o EBS
O Elastic Block Store (EBS) sao discos alocados em Storages fisicos em clusters e ligados via rede (NAS), proporcionando alta disponibilidade dos volumes alocados nas instancias e tambem a possibilidade de expansao ou criacao de novos discos nas instancias como tambem subir as instancias em outro host fisico.

Importante saber que o EBS esta disponivel apenas na mesma Availability Zone (AZ) na qual foi criada, para que seja possivel utilizar o volume em outra AZ, e necessario migrar o disco utilizando um `Snapshot`, ou seja, cria uma copia do volume EBS, migra a copia do volume para outra AZ e so entao pode fazer a criacao de um novo volume para que os dados possam ser utilizados em outra instancia.

Abaixo um Diagrama de como funciona o Elastic Block Store

![Diagram EBS](Images/Diagram_Amazon-Elastic-Block-Store.png)

Caso caia na prova sobre isso, o disco/volume so pode ser feito o attachment na mesma AZ, a migracao parte de uma copia e a utilizacao de um novo volume criado em uma outra AZ.

Link da Documentacao: https://aws.amazon.com/pt/ebs/

Principais caracteristicas do EBS:
1. `Desempenho de Armazenamento`: EBS fornece armazenamento em bloco de alto desempenho que pode ser anexado a uma instância EC2. Os volumes EBS são otimizados para cargas de trabalho que exigem operações de E/S de baixa latência, como bancos de dados e aplicativos que exigem muita E/S.

2. `Durabilidade`: O EBS é projetado para durabilidade. Os volumes EBS são automaticamente replicados em sua zona de disponibilidade para proteger contra falhas de componentes, proporcionando alta disponibilidade e durabilidade.

3. `Tipos de Volume`: EBS oferece vários tipos de volume para atender às necessidades de armazenamento e desempenho. Isso inclui os volumes SSD-backed para cargas de trabalho transacionais de uso geral (gp2 e gp3) e de alto desempenho (io1 e io2), e os volumes HDD-backed para cargas de trabalho throughput intensivas (st1 e sc1).

4. `Backup com Snapshots`: O EBS oferece a capacidade de criar snapshots (cópias) dos seus volumes, que são armazenados no Amazon S3 para durabilidade. Esses snapshots podem ser usados para criar novos volumes EBS ou para aumentar o tamanho do volume.

5. `Criptografia`: O EBS oferece a opção de criar volumes criptografados e controlar as chaves de criptografia usando o AWS Key Management Service (KMS). Isso ajuda a atender aos requisitos de conformidade e segurança.

6. `Integração com a AWS`: EBS é profundamente integrado com outros serviços da AWS, como Amazon CloudWatch para monitoramento, AWS Identity and Access Management (IAM) para controle de acesso, e AWS Snapshot Scheduler para automação de backup.


## Tipos de EBS
A AWS possui varios tipos de discos EBS, cada tipo possui uma caracteristica, performance, tecnologia e valores diferentes, proprocionando escolhas baseado na necessidade da aplicacao que seja hospedada. Basicamente existem dois tipos de EBS mais utilizados:
1. `HDD - Hard Disc Drive`
2. `SSD - Solid State Drive`

### HDD - Hard Disc Drive
Este tipo de dico e mais lento, porem entrega um espaco de armazenamento maior, sendo utilizado em aplicacoes que nao requer uma performance na entrega porem exige um alto consumo no armazenamento de dados como por exemplo um Backup.

### SSD - Solid State Drive
Este tipo de disco e mais rapido, porem entrega um espaco de armazenamento menor, sendo utilizado em aplicacoes que requer velocidade e performance no acesso aos dados no disco como por exemplo um Banco de Dados ou sistema de Cache.

Recomendado que antes de iniciar o deploy do ambiente, verifique as caracteristicas dos discos e defina baseado nas necessidades da aplicacao que sera hospedada.

Para maiores informacoes: https://aws.amazon.com/pt/ebs/volume-types/


## Valores de EBS
A cobranca do EBS sao valor mensal e por giga que for alocado, ou seja, se criar um disco EBS de 50 GB para uma instancia EC2 e nesta instancia estiver utilizando apenas 5 GB de espaco, o valor cobrado sera em cima da alocacao do recurso de 50 GB do servico EBS e nao do espaco que esta sendo utilizado dentro da instancia.


## Criando um Volume EBS
No painel da AWS, acesse o servico `EC2` > `Elastic Block Store` > `Volumes`. Clique no botao em `Create Volume`.

Em Volume settings, selecione as configuracoes que deseja para o volume

* `Volume type`: Tipo do volume que deseja criar

* `Size (GiB)`: Tamanho do volume que sera criado

* `IOPS`: Numero de operacoes de Input/Output por segundos que deseja obter com o Volume

* `Throughput (MiB/s)`: Performance de Throughput suportado pelo volume.

* `Availability Zone`: AZ em que sera criado o Volume.

* `Encryption`: Criar um volume criptografado. Caso habilite esta configuracao, voce precisa informar uma `KMS key` para criptografia.

* `Tags - optional`: Voce pode criar tags para identificacao dos discos como tambem filtrar para obter informacoes sobre custos.

Recomendado criar um disco criptografado, aumentando o nivel de seguranca dos recursos que estao sendo utilizados na AWS.

Clique em `Create Volume`.

Apos o volume esteja criado, ele ficara com status de `Available`, sera necessario fazer um `Attachment` para utiliza-lo em uma instancia.

Para colocar em uso, selecione o volume > `Actions` > `Attach Volume`.

Na tela de `Attach Volume`, selecione a qual instancia o volume sera associado, devera ser localizado via Instance Id. e informe qual o nome do dispositivo como path. Apos isso, clique no botao `Attach Volume`. Uma vez que ele esta associado, o status do volume ficara como `In-use`.


## Snapshot
O `Snapshot` e utilizado para criar uma copia do volume e dados contido neste volume. Pode ser utilizado tanto para Backup, quanto para migrar o volume para outra AZ. O Snapshot nao e cobrado, o que sera cobrado e o valor alocado do Snapshot.

Para fazer um `Snapshot`, selecione o `Volume EBS` que queria criar, clique em `Actions` > `Create snapshot`.

Insira um nome para ele, caso queira, adicione uma tag e clique no botao `Create snapshot` para criar uma copia do volume. Este processo deve levar algum tempo, dependendo do tamanho do volume como tambem da quantidade de informacoes continas nele. Um ponto importante e que o snapshot nao afeta diretamente o servidor, nao sendo necessario reiniciar ou desligar o servidor. Apenas com sistemas mais sensiveis por exemplo um banco de dados, e bom fazer em uma janela de manutencao a fim de evitar problemas ou perda de dados em tabelas.

Para consultar os Snapshots, acesse no menu do lado esquerdo a opcao `Elastic Block Store` > `Snapshots`.

Voce pode criar um volume a partir do Snapshot, selecionando o snapshot, clique em `Actions` > `Create volume from snapshot`. Caso queira criar uma imagem, selecione a opcao `Create image from snapshot` e subir uma imagem a partir desta imagem.


## Criando uma imagem AMI customizada
AMI siginifica `Amazon Machine Image`, sao imagens de sistema operacional pre configurados para serem utilizados no provisionamento de instancias EC2. Podemos utilizar tanto imagens publicas como oferecidas pela AWS e outras empresas, AMIs de comunidade ou voce pode criar imagens privadas e totalmente customizadas para utilizar em sua empresa.

Por fins de seguranca, nao e recomendado utilizar imagens da comunidade em ambientes de producao, uma vez que estas imagens podem conter falhas de seguranca e vulnerabilidades muitas vezes ja confioguradas para a finalidade de ataque.

Para criarmos uma imagem a partir de um Snapshot de um volume ou uma outra forma, seria criar uma instancia base com todos os softwares e configuracoes necessarias, em seguida selecionar ela no painel da AWS no servico `EC2`, clicar no botao `Actions` > `Image and Templates` > `Create Image`.

* `Image name`: Informe um nome para a imagem.

* `Image description`: Esta informacao e opcional, porem fornece uma descricao da imagem para uma identificacao futura.

* `Reboot Instance`: A instancia sera reiniciada a fim de criar uma imagem com ela desligada, caso habilitado, ela causara uma indisponibilidade momentanea, porem reduzira uma inconsistencia dos dados.

* `Instance volumes`: Configuracao de volumes contidos na AMI.

* `Tags`: Tags opcionais, voce pode criar as Tags da imagem e Snapshot juntas ou separadamente.

Apos inserido as informacoes, clique em `Create image`.

Para visualizar a imagem criada, acesse no meu lateral esquerdo `Images` > `AMIs`.


Para criar uma instancia a partir da AMI customizada, faca o processo de criacao normal de uma instancia EC2, na secao de `Application and OS Images (Amazon Machine Image)`, selecione a aba `My AMIs` e localize a imagem criada.

Tambem e possivel compartilhar esta imagem entre contas para poder obter um padrao basico de imagens.


## Sobre o EFS
Existe uma outra forma de armazenar os dados na AWS, ele e chamado de `Elastic File System (EFS)`, resolvendo um problema de compartilhamento em multiplos hosts no qual o `EBS` nao possibilita. O `EFS` e utilizado para compartilhamento de arquivos em sistema Linux.

Principais caracteristicas do EFS:
1. `Escalabilidade`: O EFS é projetado para escalar automaticamente para acomodar o crescimento dos dados, de alguns gigabytes a petabytes, sem a necessidade de provisionar o armazenamento.

2. `Alta Disponibilidade e Durabilidade`: O EFS armazena automaticamente os arquivos em vários dispositivos dentro e entre várias zonas de disponibilidade para garantir a disponibilidade e durabilidade dos dados.

3. `Compartilhamento de Arquivos`: O EFS suporta o compartilhamento de arquivos entre várias instâncias do Amazon EC2, permitindo que múltiplos servidores acessem um sistema de arquivos simultaneamente.

4. `Integração com AWS`: O EFS pode ser integrado a outros serviços da AWS, como o AWS Backup para backups automatizados e o AWS IAM para controle de acesso.

5. `Tipos de armazenamento`: O EFS oferece várias classes de armazenamento, incluindo Standard e Infrequent Access (IA), permitindo que você otimize os custos com base em seus padrões de acesso aos arquivos.

6. `Segurança`: O EFS inclui suporte para criptografia de dados em repouso e em trânsito, bem como integração com o AWS Key Management Service (KMS) para gerenciamento de chaves de criptografia.

### Criando um Elastic File System (EFS)
Na console AWS, localize o servico `EFS`, servico de `Management File Storage for EC2`. A partir do servico, voce clica no botao `Create File System`. Fique atento a questao de valores, pois os valores sao diferentes do servico de `EBS`, como tambem pode variar de acordo com a utilizacao do servico em seu ambiente.

* `Name - optional`: Nome do File System

* `Virtual Private Cloud (VPC)`: VPC na qual o EFS estara disponivel.

Caso queria opcoes mais avancadas, clique no botao `Customize`.

Apos inserido as informacoes, clique no botao `Create file system` para criar o `EFS`. A partir deste momento, voce ja pode compartilhar os arquivos entre os servidores.

Para que seja possivel a visualizacao dos arquivos nos servidores, precisamos fazer um `EFS mount target` no sistema de arquivos do servidor. O Topico de realizar um `EFS mount target` dentro do servidor nao e cobrado na prova.

Para maiores informacoes, consulte a documentacao: https://docs.aws.amazon.com/efs/latest/ug/accessing-fs.html


## Sobre o FSx
O `File System x` tem a mesma finalidade do EFS, porem ao contrario, ele e utilizado em sistemas Windows e pode ser utilizando tambem em outras aplicacoes que necessitam alta desempenho. Sendo gerenciado pela AWS.

Para maiores informacoes, consulte o portal: https://aws.amazon.com/pt/fsx/.


### Criando um FSx
No painel da AWS, procure o servico `FSx` Fully managed third-party file systems optimized for a variety of workloads. em `Select file system type`, selecione qual tipo deseja e configure o servico conforme necessario ao ambiente.

O FSx possibilita controle por security group, autenticacao em um Active Directory para utilizar via SSO (Single-Sign ON).

Principais caracteristicas do EFS:
1. `FSx para Windows File Server`: Ele fornece um sistema de arquivos nativamente compatível com o Windows, permitindo que você mova com facilidade as aplicações baseadas em Windows que exigem o sistema de arquivos do Windows para a AWS. É construído sobre o Windows Server e oferece suporte a recursos como deduplicação de dados, criptografia de dados em repouso, e acesso via SMB (Server Message Block) e NFS (Network File System).

2. `FSx para Lustre`: O Lustre é um sistema de arquivos popular para cargas de trabalho de computação intensiva, como análise de big data, modelagem de machine learning e processamento de mídia. O FSx para Lustre é totalmente gerenciado pela AWS, simplificando o processo de criação e execução de um sistema de arquivos Lustre.

3. `Desempenho`: O Amazon FSx foi projetado para oferecer o desempenho rápido necessário para suportar aplicações exigentes. Ele fornece baixa latência e altas taxas de transferência de dados.

4. `Compatibilidade e Integração`: O Amazon FSx é totalmente compatível com os sistemas de arquivos que suporta, o que significa que você pode usar suas ferramentas e aplicações existentes sem modificação. Além disso, o FSx se integra com uma série de outros serviços AWS para coisas como backup, monitoramento e acesso seguro a arquivos.

5. `Segurança`: O Amazon FSx oferece várias funcionalidades de segurança, como a capacidade de armazenar dados em redes virtuais privadas da Amazon (VPCs), suporte a redes de acesso (ACLs) para o Windows File Server, criptografia de dados em repouso e em trânsito, e integração com AWS Key Management Service (KMS) para gerenciamento de chaves de criptografia.