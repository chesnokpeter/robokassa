# Подтверждение и переадресация

## Подтверждение оплаты

Для подтверждения оплаты используется метод `is_result_notification_valid()`. В основе этого метода лежит создание хеша и сравнение его с заданным, чтобы убедиться, что данные не были скомпроментированы. Метод использует безопасное сравнение хешей, то есть метод не уязвим к атакам по времени. 

Метод возвращает булево значение, в случае успеха — `True`, а в случае неудачи — `False`.

Именно этот метод стоит использовать, чтобы понять, что оплата была совершена. Это означает, что этот метод нужно использовать, когда мы получаем данные с эндпоинта, который как раз и принимает данные с `ResultUrl` или `ResultUrl2` (в терминологии официальной документации).


## Переадресация

Для переадресации применяется метод `is_redirect_valid()`, он используется, когда пользователь после оплаты переходит на заданные эндпоинты `FailUrl`, `FailUrl2` `SuccessUrl`, `SuccessUrl2` (в терминологии официальной документации). Метод также возвращает булево значение, в случае успеха — `True`, а в случае неудачи — `False`.



!!! danger
    Не используйте данные, полученные через эндпоинты для переадресации. Эта возможность создана не для подтверждения оплаты. Переадресация — это лишь способ показать пользователю, что оплата прошла успешно либо неудачно, при этом рекомендуется перепроверять данные, с которыми "пришёл" пользователь. 
    
    Не применяйте это, как способ подтверждения оплаты, для этого существует способ описанный выше.

## Параметры

| Наименование  | Описание |
|:----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `signature` | В официальной терминологии — `SignatureValue`<br>Так называемая подпись, которая получается после некоторого взаимодействия с данными и хешированием их  <br><br> **Тип:** `str`  <br> **Обязательный:** ✅ |
| `out_sum` | Сумма (буквально — стоимость заказа, сделанного клиентом)  <br><br> **Тип:** `Union[float, int]`  <br> **Обязательный:** ✅ |
| `inv_id` | Номер счета, указанный при создании ссылки<br><br> **Тип:** `int`  <br> **Обязательный:** ✅ |
| `kwargs` | Позиционные аргументы, представляющие собой дополнительные параметры, начинающиеся с `shp_`. Можно передать в функцию, например, так: <br>`**{"shp_telegram_id": 246469321}`<br><br> **Тип:** `Dict[str, Any]`  <br> **Обязательный:** ❌ |


*[Union]: typing.Union
*[Dict]: typing.Dict
*[Any]: typing.Any