# fullcycle-eda


- Desafio módulo EDA full cicle...

- Repositorio código base: https://github.com/devfullcycle/fc-eda

- Servico do desafio feito em java: pasta kafka, consiste em uma app que le os eventos do kafka gerados pela wallet app go e grava os balances.

- para rodar o projeto:

```
docker compose up -d  ou caso ja tenha executado alguma vez e alterar algum parametro no projeto: docker compose up -d --build
```

Toda chamada a funcionalidade de transactions da wallet core, disparada 2 eventos para o kafka, de transactions e balances. A app java le os eventos de balance e mantem um banco  com os balances recedidos via kafka. 


- arquivo teste servico de balances: kafka/api/client.http

### Atualização 02/04:

Olá Diego,
Obrigado por enviar a sua resopsta ao desafio!
Ao executar a aplicação e enviar a request em transactions, o seguinte erro ocorreu. Por favor, adicione as instruções no readme e as migrações necessárias.
Bom trabalho!
HTTP/1.1 400 Bad Request Date: Tue, 02 Apr 2024 18:49:59 GMT Content-Length: 26 Content-Type: text/plain; charset=utf-8 Connection: close sql: no rows in result set

Resposta:

Gabriel, boa tarde! Poderia verificar se quando você subiu a base do wallet foi criada e os dados polulados? Eles estão no arquivo db/init.wallet.sql , pelo exclui o container e recriei novamente e aqui funcionou. Pelo erro reportado por você ele criou o banco porem não populou, estranho os comandos dos inserts estão no mesmo arquivo e sao os abaixo:

```
INSERT INTO `wallet`.`clients` (id, name,email) VALUES ('f8df753c-3b58-43aa-8016-12aaa4f1ea3e', 'diego', 'diego@diego.com');
INSERT INTO `wallet`.`clients` (id, name,email) VALUES ('0216ea38-524f-4e85-8743-d484a8f7538e', 'teste', 'teste@teste.com');
INSERT INTO `WALLET`.`ACCOUNTS`(id, client_id,balance) VALUES ('87495b95-1c7f-4038-ae55-ab36ed6a9411','f8df753c-3b58-43aa-8016-12aaa4f1ea3e', 100.00);
INSERT INTO `WALLET`.`ACCOUNTS`(id, client_id,balance) VALUES ('9e3c6bb1-bf75-11e9-9ea7-2a2ae2dbcce4','0216ea38-524f-4e85-8743-d484a8f7538e', 25.00);
```

Não consegui simular porque no seu ele criou as tabelas no banco mas não populou os dados. Aguardo retorno.


### Atualização 03/04:

Diego,
Por alguma razão populou clients mas não o transactions e accounts.


Resposta:
Gabriel bom dia, 

- accounts ele deveria ter preenchido, a diferença no arquivo de dump que clients que deu certo ta minusculo e accounts que deu errado ta maiúsclo. ajustei.

- transactions realmente não tem, pois a mesma esta configurada pra ser criada via aplicação na hora que envia o servico do wallet, para ele poder disparar o evento do kafka e a aplicação balance ler do outro lado, e popular sua base etc.

Outros ajustes:
- removi a linha #- .docker/mysql-balance:/var/lib/mysql , no arquivo docker-compose.yaml do Volumes dos bancos, pois na hora de testar aqui fui tentar descobri porque o seu não estava carregando e com o sem ele não deu diferença.
