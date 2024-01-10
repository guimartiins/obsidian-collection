- Message Broker
- Implementa AMQP, MQTT, STOMP and HTTP
- Desenvolvido em Erlang
- Desacomplamento entre serviços
- Rápido e poderoso
- Padrão de mercado


![[rabbitmq.png]]

# Funcionamento básico

## Tipos de Exchange

- Direct
	- Manda uma mensagem para uma fila específica
- Fanout
	- Manda uma mensagem para todas as filas que estão relacionadas à essa exchange
- Topic
	- Conseguimos configurar como será o redirecionamento da mensagem
- Headers
	- Definimos no header em qual fila a mensagem será enviada


![[Pasted image 20240110123548.png]]

## Queues

- Trabalham no padrão FIFO (First in, First Out)
- Propriedades:
	- Durable: Se ela deve ser salva mesmo depois do restart do broker
	- Auto-delete: Removida automaticamente quando o consumer se desconecta
	- Expiry: Define o tempo que não há mensagens ou clientes consumindo
	- Message TTL: Tempo de vida da mensagem
	- Overflow
		- Drop head (remove a última): Quando a fila está lotada, remove o registro mais antigo para adicionar um novo
		- Reject publish: Quando a fila estiver lotada, a fila irá rejeitar automaticamente
	- Exclusive: Somente o channel que criou pode acessar
	- Max length ou bytes: Tamanho em bytes máximo permitido para mensagens

## Dead letter queues

- Algumas mensagens não conseguem ser entregues por qualquer motivo
- São encaminhadas para uma Exchange específica que roteia as mensagens para uma dead letter queue
- Tais mensagens podem ser consumidas e averiguadas posteriormente

## Lazy queues

- Mensagens são armazenadas em disco
- Exige alto I/O