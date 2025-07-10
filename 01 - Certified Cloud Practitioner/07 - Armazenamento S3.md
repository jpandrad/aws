# Sobre S3
O `Simple Storage Service (S3)` e um servico com acesso ilimitado de espaco, quando voce cria um bucket (pasta), voce pode colocar objetos que podem ser arquivos, fotos, videos e etc. Voce paga por utilizacao de espaco, por isso a AWS nao limita a quantidade de acesso.

Voce pode utilizar o S3 como backup de arquivos da sua empresa, archive, armazenar arquivos para instalacao de softwares nas instancias, imagens estaticas para sites. Ele pode ser barato como tambem muito caro, depende de quao rapido os objetos precisam ser acessados ou nao.

Quando criado uma Bucket, precisamos criar ela com um nome e ela precisa ser um nome unico (mundialmente), pois sera criado uma URL de acesso ao objeto mundialmente.

Existe uma particularidade no tamanho maximo de um objeto que pode ser hospedado na AWS e de 5 Tera em um arquivo. E se tiver um arquivo maior do que 5GB de tamanho, o upload devera ser feito via `Multi-Part Upload`.

Link: https://aws.amazon.com/pt/s3/


## Classes e valores do S3
A AWS possiu uma lista de classes de armazenamento, variando de acordo com as necessidades para armazenamento de objetos e tambem cada classe possui um valor a ser pago pelo armazenamento dos objetos.

Por exemplo, queremos armazenar arquivos de video, este arquivo de video sera acessado com uma frequencia muito alta, desta forma, seria necessario colocar em uma classe na qual os arquivos vao estar acessiveis o tempo inteiro, pagando um pouco mais por isso.

Outra finalidade, o armazenamento de Backup da empresa, na qual so sera utilizado em caso de extrema necessidade. Ficando 2-3 anos de arquivos sem acesso, desta forma nao precisamos colocar na classe mais rapida para acesso rapido, podemos colocar em uma classe mais barata chamada de `Glacier (deep archive)`

Documentacao: https://aws.amazon.com/pt/s3/storage-classes/?nc=sn&loc=3


## Criando um Bucket
Para criar um `Bucket` no servico do `S3`, acesse o painel da AWS e procure pelo servico `S3` (Scalable Storage in the Cloud). A criacao do S3 e global, porem no momento da criacao de do `Bucket`, este `Bucket` sera criado em uma `Region`, pois o acesso ao S3 e global, porem, os arquivos ficam hospedados em uma determinada `Region`.

Antes de criar o `Bucket`, certifique-se que voce esta na `Region` que deseja criar e Clique em `Create bucket`

* `Bucket name`: Nome do Bucket, este nome devera ser unico em toda a AWS.

As demais configuracoes, podemos deixar default, caso queira alterar e testar algo. Por padrao, a AWS ja criptografa os arquivos armazenados no servico S3.

Clique em `Create Bucket` para criar o bucket.

Para fazer upload de arquivos, clique no link do bucket, voce sera direcionado para o bucket em si. Clique no botao `Upload`. Na tela de upload, clique no botao `Add files` ou `Add folder` ou arraste o arquivo para a tela. clique no botao `Upload` para realizar o upload dos arquivos.

Apos finalizar o upload, voce podera ver os arquivos contidos no bucket. se clicarmos em um objeto, podemos acessar as propriedades dele.

Em `Object overview` dentro do objeto clicado, podemos ver o tipo, tamanho, data de modificacao a Region que ele se encontra, versao, o `Amazon Resource Name (ARN)`, a `S3 URI` e `Object URL`. O `Object URL` e um link para acesso externo do arquivo, se colocarmos no Brownser a URL, podemos acessar de qualquer lugar da internet, porem como nao permitimos o acesso externo, ao colocar URL, iremos ver uma mensagem de erro `AccessDenied`.


## Hospedando um site em S3
Uma vantagem que temos trabalhando com o S3 e um site estatico, ou seja, um site que nao tenha nenhuma inteligencia ou backend por tras, somente paginas estaticas sem atualizacao dinamica.

Vamos criar um `Bucket`,

* `Bucket name`: Coloque um nome unico para o bucket

* `Block Public Access settings for this bucket`: Como teremos acesso externo, precisamos alterar algumas permissoes de acesso ao `bucket`. desabilite a opcao `Block all public access` para que a bucket possua permissao publica. a AWs vai colocar um aviso `Turning off block all public access might result in this bucket and the objects within becoming public`, informe que voce reconhece que este bucket se tornara publico com acesso externo.

Clique em `Create Bucket`.

Vou fazer o upload do arquivo `index.html` que esta localizado dentro do diretorio `files` aqui no repositorio, este arquivo e apenas uma pagina html para testes.

Apos feito o upload, acesse o bucket criado > `Properties`. va ate o final da pagina na secao `Static website hosting` e clique em `Edit`.

Ative a opcao de Web Site estatico marcando o box `Enable`.

* `Host a static website`: Deixe marcado a opcao Host a static website pois queremos hospedar um site estatico.

* `Index document`: vamos adicionar como arquivo default do site, o `iondex.html`. Caso esteja utilizando outro arquivo como pagina principal, voce deve informar aqui.

Clique em `Save changes` para salvar as configuracoes.

Em `Properties`, va ate a secao `Static website hosting`, voce vai encontrar o link `Bucket website endpoint`, ao tentar acessar o link, podemos notar que iremos conseguir acessar, porem iremos receber uma mensagem de erro `403 Forbidden - Access Denied`.

A bucket esta como publica, porem existe uma configuracao extra de permissoes de acesso. Na propria configuracao do bucket, clique na guia `Permissions`. Acesse a secao de configuracao `Bucket policy` e clique no botao `Edit`.

Em `Policy`, adicione as seguintes linhas, estas permissoes estao em formatacao JSON:
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::Bucket-Name/*"
            ]
        }
    ]
}
```
Altere o `arn:aws:s3:::Bucket-Name/*` para o nome do bucket, por exemplo, o nome do bucket que foi criado e `meu-site-com-br-9751265`, voce altera para `arn:aws:s3:::meu-site-com-br-9751265/*`

Apos inserido a policy, clique no botao `Save changes`.

Atualize a pagina e veja o acesso ao site.


## Habilitando versionamento
O `S3` proporciona versionamento de arquivos, podendo ser recuperado em caso de exlucao ou ate mesmo rollback em caso de necessidade.

Quando habilitado, ao fazer o upload de um arquivo, ele cria uma versao, ao fazer o upload do mesmo objeto, ele cria a versao 2. Quando falamos do mesmo objeto, precisa ser as mesmas caracteristicas de nome e tambem a mesma extensao do arquivo.

Ao remover o objeto, o S3 nao exclui o objeto direto, ele coloca uma "tag" informando que o arquivo foi excluido e nao exibe ele, porem ele ainda esta la e existe a possibilidade de recuperar.

Quando criamos versionamento, pagamos pelos objetos no S3 e tambem dos objetos versionados, por exemplo, temo um objeto na versao 3 com 105m, na versao 2 com 103m e na versao 1 com 100m, sera cobrado 308m ao total.

Existe a possibilidade de limitar a quantidade de versoes.

Para habilitar o versionamento, acesse o bucket, va na guia `Properties` e na secao `Bucket Versioning`, clique no botao `Edit`. Habilite a opcao `Bucket Versioning`.

Apos habilitado, podemos identificar que apareceu uma nova opcao para visualizacao das versoes na pagina do bucket em que exibe todos os arquivos no bucket chamado `Show versions`.


## Replicacao de buckets
O `S3` oferece a possibilidade de replicarmos os objetos sentre regions ou ate na mesma region.

Quando falamos de replicacao na mesma region, estamos falando em `Same Region Replication (SRR)`, utilizado em replicacao entre estagios de ambiente (desenvolvimento, homologacao e producao).

Quando falamos em replicacao de dados em outra region, estamos falando em `Cross Region Replication (CRR)`, utilizado para backup em outra region ou quando voce precisa disponibilizar as informacoes para consulta mais rapida nos clientes que estao em outro pais por exemplo.

Esta sincronizacao de dados e feito `Asynchronous`, ou seja, voce faz o upload para a bucket e ela replica automaticamente. Lembrando que e necessario ter as permissoes entre as buckets.

Para que a replicacao aconteca, e obrigatorio estar com a opcao de versionamento habilitado no bucket.

Vamos criar um novo bucket em outra region, para isso, altere a region na conta da AWS, crie um novo bucket, pode utilizar as configuracoes padroes durante a criacao deste bucket, ativando somente o versionamento deste bucket tambem.

Para exemplificar, temos os seguintes Buckets:
| Name | AWS Region |
| --- | --- |
| bucket-joao-production-1234 | US East (N. Virginia) us-east-1 |
| bucket-joao-backup-1234| US East (Ohio) us-east-2 |

Estarei configurando uma copia do bucket `bucket-joao-production-1234` para o bucket `bucket-joao-backup-1234`, entre regions.

Acesse a bucket principal, no meu caso a `bucket-joao-production-1234`, acesse a guia `Management` e encontre a secao `Replication rules`. Clique em `Create replication rule`.

* `Replication rule name`: Insira um nome de identificacao para a regra de replicacao.

* `Status`: Mantenha a regra habilitada.

* `Source bucket > Choose a rule scope`: Selecione a opcao `Apply to all objects in the bucket` para sincronizar todos os objetos ou caso queira criar um filtro de somente alguns objetos, deixe a opcao `Limit the scope of this rule using one or more filters` marcada e crie quais objetos queira sincronizar.

* `Destination`: Escolha o bucket de destino, neste exemplo, o bucket encontra-se na mesma conta, desta forma preciso deixar marcado a opcao `Choose a bucket in this account` e selecionar o bucket `bucket-joao-backup-1234` como destino. Caso o bucket esteja em outra conta, utilize a opcao `Specify a bucket in another account` e insira as informacoes da outra conta.

* `IAM role`: Selecione a opcao `Create new role` para ele criar uma role automaticamente com as permissoes necessarias, caso ja exista uma role com as devidas permissoes, voce pode selecionar atraves das opcoes `Choose from existing IAM roles` ou `Enter IAM role ARN`.

As demais opcoes sao de acordo com a necessidade do ambiente.

Clique no botao `Save`. Caso o bucket ja possua objetos, ele vai exibir uma mensagem perguntando se voce deseja replicar os objetos ja existentes.


## Sobre criptografia no S3
Criptografia e um ponto muito importante para a AWS, garantindo que todos os dados armazenados na AWS estao criptografados. Quando enviamos algum arquivo no S3, este arquivo nao esta criptografado, ao armazenar o arquivo no `S3`, o arquivo armazenado se torna criptografado, isso e chamado de `Server-Side-Encryption`, sendo o default da AWS. Este arquivo so podera ser lido com a chave de descriptografia.

Existe um outro cenario nao muito utilizado e que o `S3` sendo como servidor e existe o cliente, e o cliente por algum motivo, ele quem faz a criptografia. utilizando uma chave propria da empresa e ele faz a criptografia do arquivo antes de mandar para o servidor. Este processo se chama `Client-Side-Encryption`.

Para validar a configuracao de criptografia, acesse o bucket > `Properties`.

Na secao `Default encryption`, podemos identificar que a configuracao `Encryption type` esta como `Server-side encryption with Amazon S3 managed keys (SSE-S3)`, possuindo uma criptografia `Server-Side`. Ao clicar no botao `Edit`, temos 3 tipos de `Encryption type`:

1. `Server-side encryption with Amazon S3 managed keys (SSE-S3)`: Modo default no qual o servico do S3 utiliza uma chave da AWS gerada automaticamente para criptografia dos dados.

2. `Server-side encryption with AWS Key Management Service keys (SSE-KMS)`: Modo para utilizar uma outra chave de criptografia.

3. `Server-side encryption with AWS Key Management Service keys (SSE-KMS)`: Aplica duas camadas de criptografia na qual uma delas sera do lado do servidor e a outra a chave do lado do cliente.

Ou podemos desativar a chave da Bucket deixando como `Disable` na configuracao `Bucket Key`.

O proprio padrao da AWS ja aplica um chave de criptografia atualizada e mais segura para os clientes, sendo a recomendacao da propria AWS a utilizacao.


## Storage Gateway
O `Storage Gateway ` e utilizado para extender o armazenamento dos dados da empresa, quando uma empresa possui um `Array de Storage`, e a empresa precisa ou fazer um backup no S3, ou uma copia ate mesmo expandir os dados para serem utilizados na Cloud, o `Storage Gateway` quem fara esta conexao entre a AWS e o Storage da empresa. O `Storage Gateway` pode ser tanto um servidor `fisico` quanto uma `Maquina Virtual`.

Documentacao: https://docs.aws.amazon.com/filegateway/latest/files3/what-is-file-s3.html

A AWS utiliza no S3 seu proprio protocolo, nao utilizando protocolos de mercado como NFS ou SMB, basicamente o `Storage Gateway` faz uma "conversao" da conexao entre o storage local com a AWS.

O `Storage Gateway` tambem pode ser utilizado para `Amazon EBS` e `Amazon GLACIER`. Toda a comunicacao entre estes servicos sao totalmente seguras.


## AWS Snow Family
A AWS possui ate o momento, 3 tipos de `Snow`:
1. `SnowCone`
2. `SnowBall`
3. `SnowMobile`

Esses sao dispositivos no qual a AWS manda para a sua empresa, voce realiza a copia dos dados, envia novamente para a AWS e a AWS realiza o upload dos arquivos em um bucket S3. Utilizado em casos no qual a empresa possui varios teras de dados, a empresa pode possuir uma baixa conexao e a transferencia pode levar um tempo consideravel tanto para finalidade de migracao quando tambem tempo de projeto ou alguma outra necessidade de urgencia que leve a necessidade em copiar estes arquivos para um bucket S3.

Documentacao: https://docs.aws.amazon.com/pt_br/whitepapers/latest/how-aws-pricing-works/aws-snow-family.html