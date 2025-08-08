## AWS Kinesis
O Servico `AWS Kinesis` foi criado para `Real-Time Data Streaming`, em pratica, existe equipamentos IOT no qual envia dados em tempo real.
Esses dados precisam ser analisados, e a captura dos dados e o `Kinesis Stream`, voce pode analisar os dados com o `Kinesis Analytics` e armazena no `Kinesis Firehouse`.

O `Kinesis Firehouse` coloca os dados em um `S3` ou RedShift.

## AWS SQS
O `Simple Queue Service`, e um servico de fila de mensagem, utilizando para ficar no meio de aplicacoes que necessitam de comunicacao `Asynchrony`, controlar a fila de comunicacao, reduzindo a sobre carga de processamento na aplicacao.


## AWS SNS
O `Simple Notification Service (SNS)` e um servico de notificacao (mensagenria) no qual pode ser utilizado em varios servicos na AWS ou ate mesmo em uma aplicacao.

O SNS possibilita criar `Topics` que sao basicamente grupos e `subscribers` no qual seria os contatos para receber as notificacoes dos Topics.