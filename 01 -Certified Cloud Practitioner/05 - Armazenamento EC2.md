## Sobre o EBS
O Elastic Block Store (EBS) sao discos alocados em Storages fisicos em clusters e ligados via rede (NAS), proporcionando alta disponibilidade dos volumes alocados nas instancias e tambem a possibilidade de expansao ou criacao de novos discos nas instancias como tambem subir as instancias em outro host fisico.

Importante saber que o EBS esta disponivel apenas na mesma Availability Zone (AZ) na qual foi criada, para que seja possivel utilizar o volume em outra AZ, e necessario migrar o disco utilizando um `Snapshot`, ou seja, cria uma copia do volume EBS, migra a copia do volume para outra AZ e so entao pode fazer a criacao de um novo volume para que os dados possam ser utilizados em outra instancia.

Abaixo um Diagrama de como funciona o Elastic Block Store
![Diagram EBS](Images/Diagram_Amazon-Elastic-Block-Store.png)

Caso caia na prova sobre isso, o disco/volume so pode ser feito o attachment na mesma AZ, a migracao parte de uma copia e a utilizacao de um novo volume criado em uma outra AZ.

Link da Documentacao: https://aws.amazon.com/pt/ebs/


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
