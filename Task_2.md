# Запрос

```http
GET /api/v1/shops/nearby
Host: api.zelenaya-petrushka.ru
Authorization: Bearer <token>
Accept: application/json
```

# Ответ

```json
{
  "status": "success",
  "data": {
    "shops": [
      {
        "id": "23",
        "name": "METRO",
        "delivery_info": {
          "type": "closest",
          "text": "Ближайшая доставка сегодня 21:00–23:00"
        },
        "external_url": "https://metro.ru"
      },
      {
        "id": "456",
        "name": "Ашан",
        "delivery_info": {
          "type": "closest",
          "text": "Ближайшая доставка сегодня 18:00–20:00"
        },
        "external_url": "https://ashan.ru"
      },
      {
        "id": "789",
        "name": "ВкусВилл",
        "delivery_info": {
          "type": "express",
          "text": "Быстрая доставка от 20 до 60 минут"
        },
        "external_url": "https://vkusvill.ru"
      },
      {
        "id": "101",
        "name": "ВИКТОРИЯ",
        "delivery_info": {
          "type": "closest",
          "text": "Ближайшая доставка сегодня 17:00–19:00"
        },
        "external_url": "https://victoria.ru"
      }
    ]
  }
}
```
