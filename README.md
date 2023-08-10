
# Teste para Tutor

## Descrição

O projeto consiste na criação de um sistema de reserva de hotel.

## Tecnologias e requisitos

* Back-end (Pode ser usado qualquer lib ou framework);
* Docker para orquestar o ambiente da aplicação;
* Banco de dados MySQL;
* Testes;
* Mensageria
* Utilize DDD, Clean Architecture;

## Contexto do sistema

#### Administrator
- Cadastrar um novo hotel contendo: nome, endereço e quantidade de quartos disponíveis.
- Cadastrar um novo quarto de hotel contendo: numero do quarto, valor por noite e status (disponível/indisponível).
- Gerir quais quartos estão disponíveis e indisponíveis.

#### Cliente
- Poderá reservar em uma data especifica determinado quarto em determinado hotel se ele estiver disponível.
- Dois clientes não poderão reservar o mesmo quarto numa mesma data.
  
## Design do sistema

### Back-end

Você deve criar uma API Rest que terá os seguintes endpoints:

* POST /hotels - Realiza a criação de um novo hotel.
```json
{
    "name": "admin@user.com",
    "address": {
      "street": "",
      "zipcode": "",
      "country": "" 
    },
    "rooms_avaliable": 100,
    "rooms_booked": 98
}
```
* PUT /hotels/:hotel_id - Realiza a atualização de um hotel pelo ID.
```json
{
    "name": "admin@user.com",
    "price": {
      "street": "",
      "zipcode": "",
      "country": "" 
    },
    "rooms_avaliable": 150
}
```
* POST /hotels/:hotel_id/rooms - Realiza a criação de um novo quarto no hotel.
```json
{
    "number": 100,
    "price": 80,
    "status": "AVAILABLE" | "UNAVAILABLE"
}
```
* POST book/:hotel_id - Realiza a reserva de um quarto do hotel.
```json
{
    "room_number": 101,
    "start_date": "01/01/2023",
    "end_date": "04/01/2023",
}
```
* GET book/:hotel_id - Realiza a listagem de todos os quartos e respectivos status.
```json
[
    {
        "id": 1,
        "number": 101,
        "status": "AVAILABLE"
    },
    {
        "id": 2,
        "number": 120,
        "status": "UNAVAILABLE"
    }
]
```

### Pontos de atenção

- Um quarto não poderá ser reservado durante a mesma data em um mesmo hotel.

- Sempre quando uma reserva for realizada, deve-se registrar isto, atualizando a contagem de quartos disponíveis no hotel. 

- Ao realizar uma reserva, utilize o RabbitMQ para registrar em uma fila e enviar uma mensagem com os dados da reserva.

- Crie dados falsos para hotel e quartos. Crie pelo menos 2 hoteis e 20 quartos já previamente cadastrados no banco de dados.

- Criar a aplicação usando testes automatizados será um grande diferencial.

## Docker

Crie as duas aplicações montando-as com Docker de forma que ao fazer `docker-compose up` seja possível testar todo o ambiente. 
O Docker deve levantar back-end, banco de dados e mensageria.

## Integração continua
Essa tarefa **é opcional, ou seja, não é essencial** porém pode ser realizada. Você deverá criar uma pipeline de integração continua: 
- Criar um Dockerfile.prod;
- Criar rotina Github Actions;
- Rodar testes;

## Vídeo-aula

Você deverá gravar 1 até 4 aulas, cada aula não deve passar de 20 min. Aulas deverão ser gravadas com a utilização de câmera.

Duas aulas deverão ser codificando alguma parte do sistema (de sua escolha) no ato da aula. 

Duas aulas deverão explicar alguma parte do sistema já criado, o objetivo da aula será focar na explicação da implementação e explicar os motivos desta implementação.

Explique com clareza o que será desenvolvido, monte sua didática para que um aluno consiga entende-la facilmente.

## Entrega

Entregue o projeto em um repositório Git remoto (as aulas deverão estar presentes no repositório, renderize-as em baixa qualidade) e disponibilize o link atraves do e-mail miriane@fullcycle.com.br / leonan@fullcycle.com.br.
