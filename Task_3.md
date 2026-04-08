Я составила схему верхнеуровневой архитектуры PUSH-уведомлений для микросервисной системы интернет-магазина "Петрушка Зеленая".
<img src="./picture_2.png" width="600" />

### Источники событий (Producers)
Это микросервисы, где происходят события: Order Service — действия с заказом, Cart Service — действия с корзиной и её состояния, Marketing Service — рассылка.

### Message Broker
Например: Kafk, RabbitMQ

### Notification Service
Главный сервис, который: подписывается на события, решает кому отправлять, формирует сообщение, выбирает канал.

### Push Gateway
Сервис-адаптер к внешним платформам.

```plantuml
@startuml
title Push Notification Architecture - "Петрушка Зеленая"

package "Mobile App" {
  [iOS / Android App] --> [Push SDK]
}

package "Backend (Microservices)" {

  package "Producers" {
    [Order Service]
    [Cart Service]
    [Marketing Service]
  }

  package "Messaging" {
    [Message Broker (Kafka/RabbitMQ)]
  }

  package "Notification Domain" {
    [Notification Service]
    [Template Engine]
    [User Preferences Service]
  }

  package "Push Infrastructure" {
    [Push Gateway]
    [Device Token Store]
  }
}

package "External Systems" {
  [Firebase Cloud Messaging]
  [Apple Push Notification Service]
}

' Event flow
[Order Service] --> [Message Broker (Kafka/RabbitMQ)]
[Cart Service] --> [Message Broker (Kafka/RabbitMQ)]
[Marketing Service] --> [Message Broker (Kafka/RabbitMQ)]

' Consumption
[Message Broker (Kafka/RabbitMQ)] --> [Notification Service]

' Internal logic
[Notification Service] --> [Template Engine]
[Notification Service] --> [User Preferences Service]

' Push sending
[Notification Service] --> [Push Gateway]
[Push Gateway] --> [Device Token Store]

' External push providers
[Push Gateway] --> [Firebase Cloud Messaging]
[Push Gateway] --> [Apple Push Notification Service]

' Delivery to device
[Firebase Cloud Messaging] --> [Push SDK]
[Apple Push Notification Service] --> [Push SDK]

@enduml
```
