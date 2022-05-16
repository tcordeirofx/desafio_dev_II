Desafio de Desenvolvimento Globo Dev II

===

# Desafio

Sistemas distribuídos têm inúmeros desafios, um deles é a gestão de transações distribuídas entre diferentes serviços.

Dada uma API que receba **PEDIDOS** no seguinte formato:
```javascript
{
  "data_necessidade" : "2023-01-01",
  "account_id": "111111",
  "valor": 654.32
}
```

Ao receber um **PEDIDO**, precisamos gravar na API_ACIONAMENTO o **PEDIDO** que foi solicitado na API_PEDIDOS o **VALOR** total do pedido e a chave do acionamento.

**VALOR POR ACIONAMENTO**:
```javascript
{
  "id_acionamento": "201023"
  "id_pedido": "654321",
  "valor": 654.32
}
```

A gravação desses dados deve ser feita de forma que não se crie inconsistências, por isso a necessidade de uma transação.

### Requisitos funcionais

- Desenvolva 3 applicações dentro de uma mesma solução (Transação, Pedidos, Acionamentos);
- O serviço de transação recebe dados do **PEDIDO** e cria uma nova transação;
- As transações têm 2 passos: gravar **PEDIDO** na API_PEDIDOS e **VALOR POR PEDIDO** na API_ACIONAMENTOS;
- A execução dos passos das transações não precisa ser feita em nenhuma ordem específica;
- Quando algum passo da transação falha, este passo precisa ser retentado algumas vezes um tempo depois (pode ter um problema de rede momentâneo, por exemplo)

#### Sobre o serviço de Transação:
- É preciso poder consultar o estado e os dados da transação criada.
- Cada transação pode ter 4 estados: `pending`, `in_process`, `success` ou `fail`;
- Deve fazer com que as requisições à API_PEDIDOS e API_ACIONAMENTOS sejam executadas com sucesso;
- É preciso poder saber o que aconteceu quando houver falhas.

#### Sobre o serviço API_PEDIDOS:
- O serviço API_PEDIDOS recebe dados do **PEDIDO** para armazena-los;
- É preciso poder consultar a quantidade de pedidos por conta;
- Dado uma consulta com `id_pedido` e um `account_id`, é preciso saber se é uma combinação válida

#### Sobre o serviço API_ACIONAMENTOS:
- O serviço API_ACIONAMENTOS recebe dados do **PEDIDO** para armazenar os **VALORES POR PEDIDO** e agrupa-los posteriormente por acionamento;
- É preciso poder consultar o valor total de pedidos por acionamento;

```cypher
(request) ---[SOLICITAÇÃO]---> (Transação) -----> (API_PEDIDOS)
                                                   \
                                                    `---> (API_ACIONAMENTOS)
```

### Será avaliada:
- A clareza do código
- A escolha das tecnologias
- A eficiência e eficácia dos testes

### Procedimento:
- O projeto deve ser colocado em algum repositório público
- Em caso de dúvidas sobre o desafio, entre em contato 

### Tecnologias que usamos:
- Node.js ou Java
- MySQL ou MongoDB
- RabbitMQ
