# O que e IAM
Identity Access Manager (IAM) gerencia o acesso de usuarios, grupos, roles, policy e muito mais.

Basicamente ele possui 3 tipo de categorias:

1. `Users`: Usuarios para acesso a conta na AWS;
2. `Groups`: Grupos de permissionamento e que sao aplicados para um determinado numero de `Users`, estes usuarios herdam as permissoes de acesso do Grupo;
3. `Roles`: As roles (funcoes) sao atribuidas para politica a nivel de servico na AWS, por exemplo, voce permite que uma EC2 acesse um S3 a partir de uma role, sem a necessidade de um usuario se autenticando para tal finalidade;

Existe a possibilidade de aplicar permissoes especificas para os usuarios, porem e uma boa pratica criar `Groups` e gerenciar as permissoes, uma vez que facilita a propagacao das permissoes para outros usuarios como tambem o gerenciamento de acessos.

As `Policies` sao escritas em JSON podendo ser criada com cliques na plataforma da AWS.


## IAM Identity Center
O `IAM Identity Center` e o sucessor do `AWS Single Sing-ON`, funcionando basicamente igual o IAM, porem ele utiliza a tecnologia `Single Sing-On`, proporcionando uma base centralizada de usuario como o `Active Directory` que proporciona o gerenciamento de usuarios para ser utilizado tambem em aplicacoes.

Por padrao ele vem desabilitado e para habilitar, sera necessario criar organizacao.


## MFA
O `Multiple Factor Authentication` adiciona uma camada de seguranca que ao se autenticar na conta, ele pede um numero de 6 digitos que muda a cada 30 segundos. Aumentando o nivel de seguranca para acesso. O MFA nao vem habilitado por padrao e a configuracao e feita por usuario.

1. `Aplicacao Autenticadora`: Autenticacao via aplicativo em um celular como por exemplo o Google Authenticator;
2. `Chave de Seguranca`: Autenticacao usando codigo gerado tocando em um YubiKey ou outra chave de seguranca FIFO Compativel;
3. `Token TOTP de Hardware`: Autenticacao usando um token de senha de uso unico com marcacao temporal (TOTP) de hardware;

Geralmente as empresas de seguranca utilizam uma `chave de seguranca` que e um token fisico, ele e uma chave USB e gera o codigo.


## Organizacoes AWS
O `AWS Organization`, criar organizacoes facilita a criacao de politicas de acessos, nao e recomendado que na conta principal possua "Workloads", sendo totalmente destinada para a finalidade de gerenciamento e controle das demais contas.


## habilitando o IAM Identity Center
Com a `AWS Organization` habilitada, podemos habilitar o IAM Identity Center. Para habilitar, selecione o servico `IAM Identity Center` e em `Enable IAM Identity Center`, clique no botao `Enable`


## Politica de Senhas
A AWS possibilita algumas customizacoes na politica de senhas, proporcionando alterar o quao a senha deve possui de caracteres.

Acesse o Painel da AWS > `IAM` > em `Account setting` voce tera a configuracao da politica de senhas em `Password policy`. Esta configuracao e aplicacada tanto no `IAM` quanto no `IAM Identity Center`. A politica so entrara em vigor a partir do momento que em for feito o vencimento da senha atual para uma nova senha.


## CloudShell e AWS CLI
A AWS oferece uma ferramenta via linha de comando chamado `AWS CLI`. Esta ferramenta precisa ser instalada no computador e fornece o modo de gerenciamento e administracao via linha de comando.

Instalacao do AWS CLI: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

Guia de Referencia dos Comandos: https://docs.aws.amazon.com/cli/latest/reference/

Tambem e possivel abrir um terminal via console da AWS, para isso clique no `CloudShell` que fica localizado no canto inferior esquerdo da console da AWS ou no icone de shell que fica no canto superior direito da tela, esta opcao abre uma console via linha de comando que nao fica na sua maquina e sim na AWS, sem a necessidade de autenticacao igual o `AWS CLI`.


## AWS Access Key
Quando estamos trabalhando com o `AWS CLI`, sera necessario configurar uma autenticacao valida para acesso e utilizacao da ferramenta na conta da AWS. Para configuracao, precisamos de uma `Access Key` e uma `Private Key` (chave de acesso), sendo criada por usuario.

Para obter uma `Access Key` e uma `Private Key`, acesse o `IAM` > `Users` > Selecione o usuario que deseja criar o acesso. Clique na aba `Security Credentials` e na secao de `Access keys`, clique no link `Create access key`.

Selecione a opcao `Command Line Interface (CLI)`, no final da tela, aceite a opcao `I understand the above recommendation and want to proceed to create an access key.` e clique em `Next`.

Insira uma tag para identificacao da utilizacao da chave, importante para identificacao em caso futuro. Clique em `Create access key`.

No final da tela, sera exibido as informacoes de `Access Key` e `Secret access key`

> [!NOTE]  
> Apos o fechamento desta tela, nao sera mais possivel recuperar as informacoes de Access Key e Secret Key, sendo necessario a exclusao e criacao de uma nova chave de acesso.


## SDK
O `Software Development Kit` conhecido como SDK, e um conjunto de ferramentas de criacao especifica da plataforma para desenvolvedores. Ela e outra forma de acessar os servicos da AWS, por exemplo, voce tem uma aplicacao que esta dentro da empresa e precisa acessar os recursos na AWS. Voce precisa criar um user e a partir deste usuario voce cria uma `Access Key` e `Secret Key` para poder ser utilizado em uma aplicacao em vez de uma pessoa.


## IAM Credential Report e Access Advisor

Eu tenho um username e a partir da ferramenta da AWS `Credential Report`, conseguimos realizar uma auditoria deste usuario no ambiente da AWS. Tambem temos uma ferramenta chamada `Access Advisor` vai mostrar a lista de servicos da AWS que foi concedida a este usuario.

Para acessar o `Credential Report`, acesse o `IAM` > `Access reports` >  `Credential report`. Clique em `Download credentials report` para fazer o download do arquivo em formatacao .csv contendo a informacao de todos os usuarios com data de criacao, se o password esta enabled, a ultima alteracao da senha, a ultima vez que este usuario obteve acesso, de o MFA foi configurado, Chave de acesso entre outras informacoes. O `Credential Report` fornece uma visao de todos os usuarios.

O `Access Advisor` possibilita a visao a nivel de usuario, para isso acesse o `IAM` > Selecione o usuario > Ao selecionar o usuario, clique na guia `Last Accessed`. De forma simples, voce conseguira ver quais servicos estao permitidos e nivel de permissao que o usuario possui ao servico.

> [!NOTE]  
> Existem servicos na AWS que possuem dependencia de outros servicos, sendo normal aparecer varios servicos na lista.