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
O `Amazon AppFlow` e uma solucao 