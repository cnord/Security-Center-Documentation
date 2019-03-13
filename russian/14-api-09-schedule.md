# Расписание

Методы для управления расписанием объекта: Получение, создание, изменение или удаление расписания объекта.

## Поля расписания {#api-schedule-json}

### Расписание

```json
{
    "Id" : Guid,
    "ArmSchedule_EarlyArm" : boolean,
    "ArmSchedule_ControlArm" : boolean,
    "ArmSchedule_LaterArm" : boolean,
    "ArmSchedule_EarlyDisarm" : boolean,
    "ArmSchedule_ControlDisarm" : boolean,
    "ArmSchedule_LaterDisarm" : boolean,
    "ArmSchedule_Deviation" : number,
    "Intervals" : Interval[]
}
```

\definecolor{light-gray}{gray}{0.7}
\renewcommand{\arraystretch}{1.4}
\begin{tabularx}{\textwidth}{llX}
\textbf{Название поля} & \textbf{Тип} & \textbf{Поле в карточке объекта; примечание} \\ \midrule

Id & Guid & Идентификатор объекта \\ \arrayrulecolor{light-gray}\hline
ArmSchedule\_EarlyArm & boolean & Контролировать ранне взятие под охрану \\ \arrayrulecolor{light-gray}\hline
ArmSchedule\_ControlArm & boolean & Контролировать отсутствие взятия под охрану \\ \arrayrulecolor{light-gray}\hline
ArmSchedule\_LaterArm & boolean & Контролировать позднее взятие под охрану \\ \arrayrulecolor{light-gray}\hline
ArmSchedule\_EarlyDisarm & boolean & Контролировать раннее снятие с охраны \\ \arrayrulecolor{light-gray}\hline
ArmSchedule\_ControlDisarm & boolean & Контролировать отсутствие снятия с охраны \\ \arrayrulecolor{light-gray}\hline
ArmSchedule\_LaterDisarm & boolean & Контролировать позднее снятие с охраны \\ \arrayrulecolor{light-gray}\hline
ArmSchedule\_Deviation & number & Отклонение расписания \\ \arrayrulecolor{light-gray}\hline
Intervals & Interval[] & Интервалы расписания \\

\bottomrule
\end{tabularx}

### Интервал расписания (Interval)

```json
{
    "DayNumber" : number,
    "StartDT" : datetime,
    "StopDT" : datetime
}
```

\definecolor{light-gray}{gray}{0.7}
\renewcommand{\arraystretch}{1.4}
\begin{tabularx}{\textwidth}{llX}
\textbf{Название поля} & \textbf{Тип} & \textbf{Поле в карточке объекта; примечание} \\ \midrule

DayNumber & number & День недели (от 1 до 7) \\ \arrayrulecolor{light-gray}\hline
StartDT & datetime & Начальное время \\ \arrayrulecolor{light-gray}\hline
StopDT & datetime & Конечное время \\

\bottomrule
\end{tabularx}

## Получить расписание объекта (GET /api/Schedule) {#api-schedule-get}

Метод предназначен для получения расписания объекта.

**URL** : `/api/Schedule`

**Метод** : `GET`

### Параметры

#### id

Обязательный параметр.

Идентификатор объекта, расписание которого нужно получить. Соответствует полю `Id` элемента JSON с [полями объекта](#api-site-json).

#### userName

Необязательный параметр.

Имя пользователя, от имени которого выполняется операция.

### Возможные статусы ответов

`200`, `403` – cм. «[Статусы ответов](#api-status-codes)».

### Возвращаемые данные

При успешном выполнении метод возвращает в теле ответа элемент JSON с [полями расписания](#api-schedule-json).

### Пример использования

```bash
curl --request GET \
  --header 'apiKey: 41c66fd22dcf4742b65e9f5ea5ebde1c' \
  --url 'http://10.7.22.128:9002/api/Schedule?id=082232F8-8B06-4F7A-ABCA-AFDCC5593283&`
        `userName=crm-Ivanova-A-A'
```

**Status:** `200`

```bash
{
    "Id" : '082232F8-8B06-4F7A-ABCA-AFDCC5593283',
    "ObjectId" : 2,
    "ArmSchedule_EarlyArm" : false,
    "ArmSchedule_ControlArm" : false,
    "ArmSchedule_LaterArm" : false,
    "ArmSchedule_EarlyDisarm" : false,
    "ArmSchedule_ControlDisarm" : false,
    "ArmSchedule_LaterDisarm" : true,
    "ArmSchedule_Deviation" : 12,
    "Intervals" :
    [
        {
            "Id" : 1,
            "ObjectID" : 2,
            "DayNumber" : 2,
            "IntervalNumber" : 0,
            "StartDT" : "2012-04-23T01:00:00.000Z",
            "StopDT" : "2012-04-23T01:23:59.999Z"
        },
        {
            "Id" : 2,
            "ObjectID" : 2,
            "DayNumber" : 1,
            "IntervalNumber" : 0,
            "StartDT" : "2012-04-23T01:00:00.000Z",
            "StopDT" : "2012-04-23T01:23:59.999Z"
        },
        {
            "Id" : 3,
            "ObjectID" : 1,
            "DayNumber" : 1,
            "IntervalNumber" : 0,
            "StartDT" : "2012-04-23T02:00:00.000Z",
            "StopDT" : "2012-04-23T02:21:59.999Z"
        }
    ]
}
```

## Создать/изменить расписание (PUT|POST /api/Schedule) {#api-schedule-update}

Метод предназначен для создания/изменения расписания объекта.

**URL** : `/api/Schedule`

**Метод** : `POST` или `PUT`

### Параметры

#### userName

Необязательный параметр.

Имя пользователя, от имени которого выполняется операция.

### Тело запроса

В теле запроса должен быть передан элемент JSON с [полями расписания](#api-schedule-json), который нужно создать/изменить. При создании раздела обязательно указать только идентификатор объекта. Значения для всех остальных полей, можно не указывать: будет использовано значение по умолчанию.

Если расписание уже создано и отличается то оно будет перезаписано.

Если интервалы расписания пересекаются, то метод вернёт ошибку.

### Возможные статусы ответов

`201`, `400`, `403` – cм. «[Статусы ответов](#api-status-codes)».

### Возвращаемые данные

При успешном выполнении метод возвращает в теле ответа элемент JSON с [полями расписания](#api-schedule-json) изменённого объекта.

Если при выполнении запроса возникла ошибка, то запрос вернет код 400 и описание возникшей ошибки в теле ответа – см. «[Код 400: описание ошибки](#api-code-400-result)»

### Пример использования

```bash
curl --request POST \
  --header 'apiKey: 41c66fd22dcf4742b65e9f5ea5ebde1c' \
  --url 'http://10.7.22.128:9002/api/Parts?userName=crm-Ivanova-A-A' \
  --data '{`
    `"Id" : "082232F8-8B06-4F7A-ABCA-AFDCC5593283",`
    `"ArmSchedule_EarlyArm" : false,`
    `"ArmSchedule_ControlArm" : false,`
    `"ArmSchedule_LaterArm" : false,`
    `"ArmSchedule_EarlyDisarm" : false,`
    `"ArmSchedule_ControlDisarm" : false,`
    `"ArmSchedule_LaterDisarm" : true,`
    `"ArmSchedule_Deviation" : 12,`
    `"Intervals" :`
    `[`
        `{`
            `"DayNumber" : 2,`
            `"StartDT" : "2012-04-23T01:00:00.000Z",`
            `"StopDT" : "2012-04-23T01:23:59.999Z"`
        `},`
        `{`
            `"DayNumber" : 1,`
            `"StartDT" : "2012-04-23T01:00:00.000Z",`
            `"StopDT" : "2012-04-23T01:23:59.999Z"`
        `},`
        `{`
            `"DayNumber" : 1,`
            `"StartDT" : "2012-04-23T02:00:00.000Z",`
            `"StopDT" : "2012-04-23T02:21:59.999Z"`
        `}`
    `]`
`}'
```

**Status** : `200`

```bash
{
    "Id" : "082232F8-8B06-4F7A-ABCA-AFDCC5593283",
    "ObjectID" : 2,
    "ArmSchedule_EarlyArm" : false,
    "ArmSchedule_ControlArm" : false,
    "ArmSchedule_LaterArm" : false,
    "ArmSchedule_EarlyDisarm" : false,
    "ArmSchedule_ControlDisarm" : false,
    "ArmSchedule_LaterDisarm" : true,
    "ArmSchedule_Deviation" : 12,
    "Intervals" :
    [
        {
            "Id" : 1,
            "ObjectID" : 2,
            "DayNumber" : 2,
            "IntervalNumber" : 0,
            "StartDT" : "2012-04-23T01:00:00.000Z",
            "StopDT" : "2012-04-23T01:23:59.999Z"
        },
        {
            "Id" : 2,
            "ObjectID" : 2,
            "DayNumber" : 1,
            "IntervalNumber" : 0,
            "StartDT" : "2012-04-23T01:00:00.000Z",
            "StopDT" : "2012-04-23T01:23:59.999Z"
        },
        {
            "Id" : 3,
            "ObjectID" : 1,
            "DayNumber" : 1,
            "IntervalNumber" : 0,
            "StartDT" : "2012-04-23T02:00:00.000Z",
            "StopDT" : "2012-04-23T02:21:59.999Z"
        }
    ]
}
```

## Удалить расписание (DELETE /api/Schedule) {#api-schedule-delete}

Метод предназначен для удаления расписания объекта.

**URL** : `/api/Schedule`

**Метод** : `DELETE`

### Параметры

#### id

Обязательный параметр.

Идентификатор объекта, расписание которого нужно удалить.

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
  --url 'http://10.7.22.128:9002/api/Parts?id=082232F8-8B06-4F7A-ABCA-AFDCC5593283&`
        `userName=crm-Ivanova-A-A'
```