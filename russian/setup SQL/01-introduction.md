# Введение

Программное обеспечение «Центр охраны» разработано научно-технической и коммерческой фирмой «Си-Норд» для работы в составе комплексной системы передачи извещений «Андромеда». Программное обеспечение «Центр охраны» предназначено для эксплуатации под управлением операционных систем Microsoft Windows (7 / 10). Серверную часть программного обеспечения «Центр охраны» рекомендуется эксплуатировать под управлением операционной системы Microsoft Windows Server 2016.

Необходимо отметить следующие особенности программного обеспечения «Центр охраны»:

* Программное обеспечение «Центр охраны» состоит из независимых функциональных частей (модулей), каждая из которых предназначена для решения конкретной задачи. Это, с одной стороны, позволяет максимально защитить каждый модуль от возможного сбоя другого, а с другой стороны позволяет устанавливать каждый модуль на отдельном компьютере сети.

* Программное обеспечение «Центр охраны» ориентировано на работу в сети, поддерживающей протокол TCP/IP. Таким образом, изменения, произведенные в системе на любом компьютере сети, немедленно применяются ко всем модулям программного обеспечения, работающим в этой сети.

* Права оператора в программном обеспечении «Центр охраны» определяются по отношению к конкретному действию в конкретном модуле программного обеспечения. Таким образом, реализуются уровни доступа операторов как к программе целиком, так и к отдельным ее составляющим. Например, можно ограничить доступ оператора как ко всему модулю «Менеджер объектов», так и только к функции редактирования расписания охраны объекта.

Приемное оборудование центральной станции позволяет принимать и обрабатывать события с контрольных панелей (концентраторов, объектовых блоков), имеющих встроенные коммуникаторы (блоки передачи цифровых сообщений — специализированные модемы). В зависимости от типа контрольной панели, ее функциональных и сервисных возможностей, от нее можно получать ту или иную информацию о состоянии объекта. Большинство контрольных панелей могут передавать широкий спектр информации. Например, данные о пользователе, выполнившем взятие или снятие с охраны; место (номер зоны) тревоги или неисправности (обрыв, замыкание); частичное взятие с указанием неохраняемых зон и многое другое. Благодаря этому, дежурный оператор комплекса имеет самую полную информацию как о состоянии объекта (поставлен на охрану, снят с охраны, тревога и т.д.), так и о техническом состоянии оборудования (разряжен аккумулятор, отсутствует 220В, неисправна телефонная линия и т.д.).

## Аппаратные требования к системе

Минимальная конфигурация: Процессор Intel Core i5, RAM 4Gb, 17\" SVGA монитор, звуковая карта, USB-порт для установки электронного ключа защиты.

Рекомендуемая конфигурация: Процессор Intel Core i7, RAM 8Gb, 19\" SVGA монитор, звуковая карта и сетевая карта для эксплуатации программного обеспечения в сети, USB-порт для установки электронного ключа защиты.

## Требования к операционной системе

Поддерживаются следующие операционные системы:

* Microsoft Windows 7
* Microsoft Windows 8
* Microsoft Windows Server 2003
* Microsoft Windows Server 2008
* Microsoft Windows Server 2012
* Microsoft Windows Server 2016

Работа с Microsoft Windows XP, Microsoft Windows Server 2003, Microsoft Windows Server 2008 возможна, но если еть выбор, то лучше использовать более новую операционную систему.
Программное обеспечение «Центр охраны» версии 5 предназначено для эксплуатации как на 32-битных, так и на 64-битных версиях перечисленных операционных систем.

Перед установкой «Центра охраны» рекомендуется проверить, что для операционной системы установлен последний из пакетов обновления, предлагаемых компанией «Microsoft».

## Электронный ключ защиты
Программное обеспечение «Центр охраны» защищено от нелегального копирования электронным ключом защиты. Перед использованием «Центра охраны» необходимо подключить электронный ключ к USB-порту компьютера и выполнить установку его драйвера.

## Комплект поставки
Программное обеспечение «Центр охраны» поставляется в следующем комплекте:

* Дистрибутив полной версии «Центра охраны», предназначенный для установки «Центра охраны» на новый компьютер, где программное обеспечение ранее не было установлено.

* Дистрибутив пакета обновления «Центра охраны», предназначенный для обновления уже установленного программного обеспечения «Центр охраны» (или программного обеспечения «Андромеда 2.8») до «Центра охраны» версии 5.

* Электронный ключ защиты, устанавливаемый в USB-порт компьютера.
	* Дистрибутив драйверов электронного ключа защиты.

Все перечисленные дистрибутивы можно скачать с сайта support.cnord.ru.