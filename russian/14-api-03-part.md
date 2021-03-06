\pagebreak

# Раздел

Методы для управления разделами объекта: получение списка разделов, создание, изменение или удаление раздела объекта.

## Поля раздела {#api-part-json}

Элементо JSON, содержащий все поля раздела:

```json
{
    "Id": string,
    "PartNumber": number,
    "ObjectNumber": number,
    "PartDesc": string,
    "PartEquip": string,
    "IsStateArm": boolean,
    "IsStateAlarm": boolean,
    "StateArmDisArmDateTime" : string
}
```

\definecolor{light-gray}{gray}{0.7}
\renewcommand{\arraystretch}{1.4}
\begin{tabularx}{\textwidth}{llX}
\textbf{Название поля} & \textbf{Тип} & \textbf{Поле в карточке раздела; примечание} \\ \midrule

Id & string & Идентификатор раздела \\ \arrayrulecolor{light-gray}\hline
PartNumber & number & Номер раздела (обязательный при создании, натуральное число, почти всегда совпадает с номером, запрограммированным в контрольную панель, установленную на объекте) \\ \arrayrulecolor{light-gray}\hline
ObjectNumber & number & Объектовый номер раздела. Используется только для объектовых приборов, поддерживающих индивидуальные объектовые номера для разделов \\ \arrayrulecolor{light-gray}\hline
PartDesc & string & Название (описание) раздела (обязательный при создании, не может быть пустым) \\ \arrayrulecolor{light-gray}\hline
PartEquip & string & Название (описание) оборудования, установленного в разделе \\ \arrayrulecolor{light-gray}\hline
IsStateArm & boolean & Состояние раздела: взят/снят/неизвестно. Нельзя указывать при создании и модификации. \\ \arrayrulecolor{light-gray}\hline
IsStateAlarm & boolean & Состояние раздела: раздел в тревоге/в норме. Нельзя указывать при создании и модификации. \\ \arrayrulecolor{light-gray}\hline
StateArmDisArmDateTime & string & Состояние раздела: время последнего взятия / снятия. Нельзя указывать при создании и модификации. \\

\bottomrule
\end{tabularx}

## Получить список разделов объекта (GET /api/Parts) {#api-parts-get-list}

Метод предназначен для получения списка разделов объекта.

**URL** : `/api/Parts`

**Метод** : `GET`

### Параметры

#### siteId

Обязательный параметр.

Идентификатор объекта, список разделов которого нужно получить. Соответствует полю `Id` элемента JSON с [полями объекта](#api-site-json).

#### userName

Необязательный параметр.

Имя пользователя, от имени которого выполняется операция.

### Возможные статусы ответов

`200`, `403` – cм. «[Статусы ответов](#api-status-codes)».

### Возвращаемые данные

При успешном выполнении метод возвращает в теле ответа список элементов JSON с [полями раздела](#api-part-json).

### Пример использования

```bash
curl --request GET \
  --header 'apiKey: 41c66fd22dcf4742b65e9f5ea5ebde1c' \
  --url 'http://10.7.22.128:9002/api/Parts?siteId=b8144107-31d1-4800-b83d-764f015a54a5&`
        `userName=crm-Ivanova-A-A'
```

**Status:** `200`

```json
[
    {
        "Id": "524bf1a5-76ce-43a7-9ed5-56291750933d",
        "PartNumber": 1,
        "ObjectNumber": 0,
        "PartDesc": "Вход и периметр",
        "PartEquip": "",
        "IsStateArm": True,
        "IsStateAlarm": False,
        "StateArmDisArmDateTime" : "1899-12-30T00:00:00"
    },
    {
        "Id": "524bf1a5-76ce-43a7-9ed5-56291750933e",
        "PartNumber": 2,
        "ObjectNumber": 0,
        "PartDesc": "Внутренние помещения",
        "PartEquip": "",
        "IsStateArm": True,
        "IsStateAlarm": False,
        "StateArmDisArmDateTime" : "1899-12-30T00:00:00"
    },
]
```

## Получить раздел по идентификатору (GET /api/Parts) {#api-parts-get-single}

Метод предназначен для получения информации о конкретном разделе. Для поиска раздела должен быть использован его идентификатор.

**URL** : `/api/Parts`

**Метод** : `GET`

### Параметры

#### id

Обязательный параметр.

Идентификатор раздела, информацию о котором нужно получить.

#### userName

Необязательный параметр.

Имя пользователя, от имени которого выполняется операция.

### Возможные статусы ответов

`200`, `400`, `403` – cм. «[Статусы ответов](#api-status-codes)».

### Возвращаемые данные

При успешном выполнении метод возвращает в теле ответа элемент JSON с [полями раздела](#api-part-json).

### Пример использования

```bash
curl --request GET \
  --header 'apiKey: 41c66fd22dcf4742b65e9f5ea5ebde1c' \
  --url 'http://10.7.22.128:9002/api/Parts?id=524bf1a5-76ce-43a7-9ed5-56291750933e&`
        `userName=crm-Ivanova-A-A'
```

**Status:** `200`

```json
{
    "Id": "524bf1a5-76ce-43a7-9ed5-56291750933e",
    "PartNumber": 2,
    "ObjectNumber": null,
    "PartDesc": "Внутренние помещения",
    "PartEquip": null,
    "IsStateArm": True,
    "IsStateAlarm": True,
    "StateArmDisArmDateTime" : "1899-12-30T00:00:00"
}
```

## Создать раздел (POST /api/Parts) {#api-parts-post}

Метод предназначен для создания нового раздела для объекта.

**URL** : `/api/Parts`

**Метод** : `POST`

### Параметры

#### siteId

Обязательный параметр.

Идентификатор объекта, для которого нужно создать объект. Соответствует полю `Id` элемента JSON с [полями объекта](#api-site-json).

#### userName

Необязательный параметр.

Имя пользователя, от имени которого выполняется операция.

### Тело запроса

В теле запроса должен быть передан элемент JSON с [полями раздела](#api-part-json), который нужно создать. Значения для всех полей, можно не указывать: будет использовано значение по умолчанию.

Если указан идентификатор раздела, то он будет проигнорирован.

Если номер раздела указан и раздела с таким номером уже есть в списке разделов объекта, то метод вернет ошибку.

### Возможные статусы ответов

`201`, `400`, `403` – cм. «[Статусы ответов](#api-status-codes)».

### Возвращаемые данные

При успешном выполнении метод возвращает в теле ответа элемент JSON с информацией об идентификаторе, который получил созданный раздел:

```json
{
    "Id": string
}
```

Если при выполнении запроса возникла ошибка, то запрос вернет код 400 и описание возникшей ошибки в теле ответа – см. «[Код 400: описание ошибки](#api-code-400-result)»

### Пример использования

```bash
curl --request POST \
  --header 'apiKey: 41c66fd22dcf4742b65e9f5ea5ebde1c' \
  --url 'http://10.7.22.128:9002/api/Parts?siteId=b8144107-31d1-4800-b83d-764f015a54a5&`
        `userName=crm-Ivanova-A-A' \
  --data '{"PartNumber": 3,"PartDesc": "Подвал"}'
```

**Status** : `201`

```bash
{
    "Id": "524bf1a5-76ce-43a7-9ed5-56291750933f"
}
```

## Изменить раздел (PUT /api/Parts) {#api-parts-put}

Метод предназначен для изменения полей раздела.

**URL** : `/api/Parts`

**Метод** : `PUT`

### Параметры

#### id

Обязательный параметр.

Идентификатор раздела, который нужно изменить.

#### userName

Необязательный параметр.

Имя пользователя, от имени которого выполняется операция.

### Тело запроса

В теле запроса должен быть передан элемент JSON с [полями раздела](#api-part-json), которые нужно изменить. Если поле необходимо оставить без изменения, то оно не должно быть указано в эелементе JSON.

Идентификатор объекта передается параметром в заголовке запроса, поэтому поле `id` в элементе JSON может быть не указано или будет проигнорировано.

### Возможные статусы ответов

`200`, `400`, `403` – cм. «[Статусы ответов](#api-status-codes)».

### Возвращаемые данные

При успешном выполнении метод возвращает в теле ответа элемент JSON с [полями раздела](#api-part-json) – с учетом изменений, которые произошли в результате выполнения запроса.

Если при выполнении запроса возникла ошибка, то запрос вернет код 400 и описание возникшей ошибки в теле ответа – см. «[Код 400: описание ошибки](#api-code-400-result)»

### Пример использования

```bash
curl --request PUT \
  --header 'apiKey: 41c66fd22dcf4742b65e9f5ea5ebde1c' \
  --url 'http://10.7.22.128:9002/api/Parts?id=524bf1a5-76ce-43a7-9ed5-56291750933f&`
        `userName=crm-Ivanova-A-A' \
  --data '{"PartDesc": "Чердак"}'
```

## Удалить раздел (DELETE /api/Parts) {#api-parts-delete}

Метод предназначен для удаления раздела объекта.

**URL** : `/api/Parts`

**Метод** : `DELETE`

### Параметры

#### id

Обязательный параметр.

Идентификатор раздела, который нужно удалить.

#### userName

Необязательный параметр.

Имя пользователя, от имени которого выполняется операция.

### Возможные статусы ответов

`200`, `400`, `403` – cм. «[Статусы ответов](#api-status-codes)».

### Возвращаемые данные

При успешном выполнении метод не возвращает данных. Если при выполнении запроса возникла ошибка, то запрос вернет код 400 и описание возникшей ошибки в ответе – см. «[Код 400: описание ошибки](#api-code-400-result)»

### Пример использования

```bash
curl --request DELETE \
  --header 'apiKey: 41c66fd22dcf4742b65e9f5ea5ebde1c' \
  --url 'http://10.7.22.128:9002/api/Parts?id=524bf1a5-76ce-43a7-9ed5-56291750933f&`
        `userName=crm-Ivanova-A-A'
```
