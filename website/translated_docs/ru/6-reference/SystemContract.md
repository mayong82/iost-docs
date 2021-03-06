---
id: SystemContract
title: Системный контракт
sidebar_label: Системный контракт
---

## vote_producer.iost
---

### Описание
Контракт Super Node (также известен как, Узел Servi) агитирует за голосование.

### Информация
| contract_id | vote_producer.iost |
| :----: | :------ |
| language | javascript |
| version | 1.0.0 |

### API

#### applyRegister
Подать заявку на регистрацию, чтобы стать кандидатом в супер-узлы.

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Account Name | string |
| public key base58 encoding | string |
| Location | string |
| Website url | string |
| network id | string |
| is producer | bool |

#### applyUnregister
Подать заявку на отмену.

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Account Name | string |


#### unregister
Для отмены регистрации вначале необходимо вызвать ApplyUnregister. После прохождения аудита вы можете вызвать этот интерфейс.

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Account Name | string |

#### updateProducer
Обновить регистрационную информацию.

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Account Name | string |
| public key base58 encoding | string |
| Location | string |
| Website url | string |
| network id | string |

#### logInProducer
Выйти в Онлайн, указывая, что узел в настоящее время доступен для работы.

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Account Name | string |

#### logOutProducer
Выйти в Оффлайн означает, что узел в настоящее время недоступен для работы.

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Account Name | string |

#### vote
Проголосовать.

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Voter Account Name | string |
| Candidate Account Name | string |
| Number of votes | string |

#### unvote
Отменить голоса.

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Voter Account Name | string |
| Candidate Account Name | string |
| Number of votes | string |

#### voterWithdraw
Избиратели получают бонусные вознаграждения.

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Voter Account Name | string |

#### candidateWithdraw
Кандидат получает бонусные вознаграждения.

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Candidate Account Name | string |

## vote.iost
---

### Описание
Универсальный контракт голосования используется для создания голосов, сбора голосов и статистики голосов. Вы можете реализовывать свои собственные функции голосования основываясь на этом контракте.

### Информация
| contract_id | vote.iost |
| :----: | :------ |
| language | javascript |
| version | 1.0.0 |

### API

#### newVote
Создать голосование.

| Список параметров | Тип данных параметров | Примечания |
| :----: | :------ | :------ |
| Vote creator account name | string | Создайте голосование, которое требует залога 1000 IOST, которые будут вычтены с аккаунта создателя, а аккаунт создателя имеет права администратора голосования |
| Vote Description | string ||
| Voting Settings | json object| содержит 5 ключей: <br>resultNumber —— тип данных number(число), количество результатов голосования, максимум 2000; <br> minVote —— тип данных number, минимальное количество голосов, кандидаты набравшие голосов больше этого значения будут введены в набор результатов голосования; <br>options - тип данных array(массив), набор кандидатов, каждый элемент это string(строка), представляет кандидата, изначально может быть пустым []; <br>anyOption - тип данных bool(булевые), разрешить ли кандидату в коллекцию без опций, передача false означает, что пользователь может приводить кандидатов только в коллекции options; <br>freezeTime - тип данных number, время отмены заморозки токенов, в секундах;
Успешный вызов возвращает глобально уникальный ID голосования.

#### addOption
Увеличение опций голосования.

| Список параметров | Тип данных параметров | Примечания |
| :----: | :------ | :------ |
| Vote ID| string | ID возвращенный интерфейсом NewVote |
| Options | string ||
| Очистить ли предыдущие голоса | bool ||

#### removeOption
Удаление опции голосования при сохранении результата голосования, удаление опции, а затем добавление этой опции через AddOption, чтобы выбрать следует ли восстанавливать количество голосов.

| Список параметров | Тип данных параметров | Примечания |
| :----: | :------ | :------ |
| Vote ID| string | ID возвращенный интерфейсом NewVote|
| Options | string ||
Нужно ли удалять | bool | false означает, что опция не удалена, когда она находится в наборе результатов, true означает принудительно удалить и обновить набор результатов |

#### getOption
Получение голосов за кандидата.

| Список параметров | Тип данных параметров | Примечания |
| :----: | :------ | :------ |
| Vote ID| string | ID возвращенный интерфейсом NewVote|
| Options | string ||

Результатом является объект json:

| ключ | тип данных | примечания |
| :----: | :------ | :------ |
| votes| string | Голоса |
| deleted| bool | Помечены ли как удаленные |
| clearTime| number | Номер блока, где в последний раз произошло очищение количества голосов |

#### voteFor
Голосовать за других, IOST заложенные для голосования будет вычтено с аккаунта агента.

| Список параметров | Тип данных параметров | Примечания |
| :----: | :------ |:------ |
| Vote ID| string | ID возвращенный интерфейсом NewVote|
| Agent account name | string ||
| Voter Account Name | string ||
| Options | string ||
| Number of votes | string ||

#### vote
Проголосовать.

| Список параметров | Тип данных параметров | Примечания |
| :----: | :------ |:------ |
| Vote ID| string | ID возвращенный интерфейсом NewVote|
| Voter Account Name | string ||
| Options | string ||
| Number of votes | string ||

#### unvote
Отменить голоса.

| Список параметров | Тип данных параметров | Примечания |
| :----: | :------ |:------ |
| Vote ID| string | ID возвращенный интерфейсом NewVote|
| Voter Account Name | string ||
| Options | string ||
| Number of votes | string ||

#### getVote
Получить запись о голосовании аккаунта.

| Список параметров | Тип данных параметров | Примечания |
| :----: | :------ |:------ |
| Vote ID| string | ID возвращенный интерфейсом NewVote|
| Voter Account Name | string ||

Результатом будет массив json, каждый элемент которого является следующим объектом:

| ключ | тип данных | примечания |
| :----: | :------ | :------ |
| option| string | опции |
| votes| string | Число голосов |
| voteTime| number | Номер блока последнего голоса |
| clearedVotes| string | Число очищенных голосов |

#### getResult
Получить результат голосования и вернуть опцию resultNumber перед количеством голосов.

| Список параметров | Тип данных параметров | Примечания |
| :----: | :------ |:------ |
| Vote ID| string | ID возвращенный интерфейсом NewVote|

Результатом будет массив json, каждый элемент которого является следующим объектом:

| ключ | тип данных | примечания |
| :----: | :------ | :------ |
| option| string | опции |
| votes| string | Количество голосов |

#### delVote
Удалить голосование и вернуть IOST, которые были созданы во время голосования, аккаунту создателя.

| Список параметров | Тип данных параметров | Примечания |
| :----: | :------ | :------ |
| Vote ID| string | ID возвращенный интерфейсом NewVote|

## auth.iost
---

### Описание
Система аккаунтов и управления их правами

### Информация
| contract_id | auth.iost |
| :----: | :------ |
| language | javascript |
| version | 1.0.0 |

### API

#### signUp
Создать аккаунт

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Username | string |
| ownerKey | string |
| activeKey | string |

#### addPermission
Добавить разрешения аккаунту

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Username | string |
| Permission name | string |
| Permission threshold | number |

#### dropPermission
Удалить разрешение

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Username | string |
| Permission name | string |

#### assignPermission
Указать разрешения для элемента

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Username | string |
| Permissions | string |
| item | string |
| Weight | number |


#### revokePermission
Отозвать разрешение

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Username | string |
| Permissions | string |
| item | string |

#### addGroup
Добавить группу разрешений

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Username | string |
| Group name | string |

#### dropGroup
Удалить группу разрешений

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Username | string |
| Group name | string |

#### assignGroup
Указать элемент для группы разрешений

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Username | string |
| Group name | string |
| item | string |
| Weight | number |

#### revokeGroup
Отозвать элемент группы разрешений

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Username | string |
| Group name | string |
| item | string |


#### assignPermissionToGroup
Добавить разрешения в группу

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Username | string |
| Permission name | string |
| Group name | string |


#### revokePermissionInGroup
Удалить разрешения в группе

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Username | string |
| Permission name | string |
| Group name | string |


## bonus.iost
---

### Описание

Формальное управление вознаграждениями узлов

### Информация

| contract_id | bonus.iost |
| :----: | :------ |
| language | javascript |
| version | 1.0.0 |

### API

#### issueContribute

Расчет значения вклада. Это вызывается системой автоматически.

| Список параметров | Тип данных параметров |
| :----: | :------ |
| data | json |

#### exchangeIOST

Использовать значение вклада для выплаты IOST

| Список параметров | Тип данных параметров |
| :----: | :------ |
| Account Name | string |
| Quantity | string |


## system.iost

---

### Описание
Базовый системный контракт для выпуска и обновления контрактов и других базовых системных функций.

### Информация
| contract_id | system.iost |
| :----: | :------ |
| language | native |
| version | 1.0.0 |

### API

#### setCode (code)
Развертывание смарт-контрактов.

| Имя параметра | Описание параметра | Тип данных параметра |
| :----: | :----: | :------ |
| code | Код смарт-контракта | string |

| Return Value | Тип возвращаемого значения |
| :----: | :------ |
| contractID | string |

Код смарт-контракта включает в себя код и информацию о смарт-контракте, такую как определения языка программированая и интерфейса смарт-контракта. Параметр code поддерживает два формата: формат json и формат сериализации кодирования protobuf.
Для разработчиков при развертывании контрактов как правило нет необходимости вызывать напрямую этот интерфейс. Рекомендуется использовать iwallet или реализации SDK на языке программирования связанного с этим контрактом.

При развертывании смарт-контракта система автоматически вызывает функцию init() смарт-контракта. Разработчик может выполнить некоторую работу по инициализации в функции init.

Возвращаемое значение contractID является ID смарт-контракта, который глобально уникален и генерируется с помощью хеша транзакции, которая разворачивает контракт в сети. contractID начинается с "Contract" и состоит из букв верхнего и нижнего регистра, а также чисел. В транзакции можно развернуть только один смарт-контракт.

#### updateCode (code, data)
Обновление смарт-контрактов.

| Имя параметра | Описание параметра | Тип данных параметра |
| :----: | :----: | :------ |
| code | Код смарт-контракта | string |
| data | параметры функции upgrade | string |

| Return value | None |
| :----: | :------ |

Обновление смарт-контракта, code это код смарт-контракта, формат такой же как в параметрах SetCode.

При обновлении смарт-контракта система автоматически проверит разрешения на обновление, есть ли функция can_update(data) в контракте, а также является ли параметр data вторым параметром в UpdateCode, только в случае есть ли функция can_update существует, вызов возвращает true.
Обновление контракта будет выполнено успешно, в противном случае обновление завершится неудачно, и будет определено, что разрешение на обновление отсутствует.

#### cancelDelaytx (txHash)
Отмена отложенной транзакции, для отмены отложенной транзакции вызывайте эту функцию перед выполнением отложенной транзакции.

| Имя параметра | Описание параметра | Тип данных параметра |
| :----: | :----: | :------ |
| txHash | Хеш транзакции | string |

| Return value | None |
| :----: | :------ |

#### requireAuth (acc, permission)
Проверка, есть ли у транзакции разрешение аккаунта.

| Имя параметра | Описание параметра | Тип данных параметра |
| :----: | :----: | :------ |
| acc | имя аккаунта | string |
| permission | имя разрешения | string |

| Возвращаемое значение | Тип данных |
| :----: | :------ |
| ok | bool |

#### receipt (data)
Генерация квитанции транзакции, квитанция хранится в блоке, а также может быть запрошена с помощью хеша транзакции.

| Имя параметра | Описание параметра | Тип данных параметра |
| :----: | :----: | :------ |
| data | контент квитанции | string |

| Возвращаемое значение | None |
| :----: | :------ |
