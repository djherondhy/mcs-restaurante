# 🍽️ Microservices - Restaurante e Item Service

Este projeto contém dois microserviços: **ItemService** e **RestauranteService**. O **RestauranteService** envia informações sobre um restaurante para o **ItemService** via HTTP e RabbitMQ, permitindo o gerenciamento e comunicação entre serviços.

## 🛠️ Microserviços

- **ItemService**: Gerencia os itens de um restaurante.
- **RestauranteService**: Gerencia restaurantes e envia suas informações para o ItemService.

## 🐳 Comandos Docker

### Build dos Microserviços

1. **ItemService**:  
   ```bash
   docker build -t itemservice:1.2 .

2. **RestauranteService**
   ```bash
   docker build -t restauranteservice:1.2 .

### Rodando os Contêineres

1. **RabbitMQ:**:
   Inicia o contêiner do RabbitMQ para comunicação entre os microserviços.   
   ```bash
   docker run -d --hostname rabbitmq-service --name rabbitmq-service --network restaurante-bridge rabbitmq:3-management

2. **MySQL**
   Inicia o contêiner do MySQL.
   ```bash
   docker run --name=mysql -e MYSQL_ROOT_PASSWORD=root -d --network restaurante-bridge mysql:5.6

3. **ItemService**
   Roda o serviço de itens na porta 8080.
    ```bash
    docker run --name=item-service -p 8080:80 --network restaurante-bridge itemservice:1.2

4. **RestauranteService**
   Roda o serviço de restaurante na porta 8081.
    ```bash
   docker run --name=restaurante-service -p 8081:80 --network restaurante-bridge restauranteservice:1.5

## 📦 Comunicação entre Microserviços

- **HTTP**: O RestauranteService faz chamadas HTTP para enviar informações de restaurantes para o ItemService.
- **RabbitMQ**: O RestauranteService também envia mensagens via RabbitMQ para o ItemService com dados do restaurante.
