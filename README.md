# fullcycle-eda


- Desafio módulo EDA full cicle...

- Repositorio código base: https://github.com/devfullcycle/fc-eda

- Servico do desafio feito em java: pasta kafka, consiste em uma app que le os eventos do kafka gerados pela wallet app go e grava os balances.

- para rodar o projeto:

```
docker compose up -d
Acessar o container go 
Executar cd cmd/walletcore 
go run main.go
```

Toda chamada a funcionalidade de transactions da wallet core, disparada 2 eventos para o kafka, de transactions e balances. A app java le os eventos de balance e mantem um banco  com os balances recedidos via kafka. 
