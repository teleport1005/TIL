## RabbitMQ
- AMQP 통신을 기반으로 여러 소프트웨어간 메시지를 주고받게 해 주는 Message 브로커
- Spring Boot AMQP를 이용하여 사용
- 메시지를 Message Broker에 맡겨 전달하여 서버간의 결합성을 감소시키고 확장성을 확보

### Competing Consumers
- 메시지를 주고받는 방식을 정의한 디자인 패턴의 일종
  - 한 서버에서 처리해야 하는 작업을 Queue에 적재
  - 처리하는 기능을 갖춘 소프트웨어가 Queue에서 순차적으로 작업 처리
  - 서버는 작업이 어떻게 진행되는지 관여하지 않는다(결합성 감소)

### Publish Subscribe
- 메시지 생성시 Subscribe들에게 동시에 메시지를 전달하는 패턴
  - Subscribe들은 특정 분류의 메시지만 듣도록 설정
  - 메시지에 따라 Subscribe의 행동이 정의되어 있을 때 유용

### RabbitMQ의 Exchange
- RabbitMQ의 Publisher는 직접 Queue에 메시지를 작성하지 않음
- Exchange에 메시지를 전달 후 연결된 Subscribe의 Queue에 메시지를 전달할지를 결정
- 어떤 규칙으로 전달할지는 Exchange마다 상이
  ### <Exchange 규칙>
  #### Fanout Exchange
    - 연결된 모든 Queue에 조건 없이 전달
  #### Direct Exchange
    - Queue가 연결될 때 사용한 Binding Key와 전달할 메시지의 Routing Key가 일치할 때 전달
  #### Topic Exchange
    - Binding Key를 .으로 구분하고, *과 #의 와일드 카드 활용
    - 계층적 주제에 대하여 메시지의 Routing Key와 일치할 경우 전달

    
