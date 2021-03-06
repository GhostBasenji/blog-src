+++
title = "Создаем проект базы данных в Visual Studio 2019"
date = "2019-10-17"
tags = [
    "MS SQL",
    "Visual Studio 2019",
    "Разработка проектов БД",
    "Database Project",
    "Базы данных"
]
+++

В настоящее время базы данных (БД) являются проблемой для разработчиков, и это одна из самых сложных задач в любом проекте ПО для управления изменениями БД и синхронизации этих изменений.
Для решения этой проблемы в Visual Studio имеются проекты баз данных SQL. Можно с легкостью разрабатывать, управлять, сравнивать и развертывать изменения базы данных с помощью Visual Studio.
<!--more-->
А также можем отслеживать изменения всех объектов БД через систему контроля версий.
Visual Studio Database Project предоставляет гибкие возможности для создания нового проекта базы данных из существующей БД с помощью нажатия на кнопку или возможность создания проекта базы данных с нуля.

### Итак, поехали
Запускаем Visual Studio 2019, выбираем Create a new project, потом выбираем SQL Server Database Project.

![](https://i.postimg.cc/tT98RPR0/gb0045.jpg)

Введем название базы данных и выберем место расположения файла.

![](https://i.postimg.cc/Y98Zv9jv/gb0046.jpg)

После чего щелкаем по кнопке Create.
А теперь правой кнопкой мыши щелкаем по проекту SampleDB и из появившейся меню выбираем Add > Table.

![](https://i.postimg.cc/VkMhj4dQ/gb0047.jpg)

Присваиваем имя таблице – “Student” и щелкаем по кнопке Add.

![](https://i.postimg.cc/d31XrYT4/gb0048.jpg)

После того, как добавили таблицу, появится окно конструктора таблицы. Здесь мы можем добавлять столбцы с типом данных.

![](https://i.postimg.cc/N0kPnM6d/gb0049.jpg)

Добавим несколько столбцов в эту таблицу. Мы увидим, что сгенерируется скрипт в нижней части окна и сохраняется схема таблицы.

![](https://i.postimg.cc/MTZrJStq/gb0050.jpg)



### Теперь пора опубликовать базу данных в SQL Server
Щелкаем правой кнопкой мыши в окне Solution Explorer по проекту базы данных. В появившемся меню выбираем Properties.
В параметрах проекта выбираем версию SQL Server.

![](https://i.postimg.cc/qMWYhWBx/gb0051.jpg)

Кроме того, мы можем изменять подключение по умолчанию на вкладке **Debug** Щелкаем по кнопке **Edit**.

![](https://i.postimg.cc/CKgQJDqZ/gb0052.jpg)

Изменяем свойства соединения в соответствии с параметрами ПК. Введем имя сервера, имя пользователя, пароль и выберем базу данных. Потом щелкаем по кнопке OK. Если есть проверка подлинности Windows, то не нужно указывать имя пользователя и пароль. Нам нужно только имя сервера и база данных.

![](https://i.postimg.cc/nVRNZC65/gb0053.jpg)

Не забываем сохранять все изменения.
А теперь щелкаем правой кнопкой мыши на проекте БД и выбираем **Publish…** Редактируем настройки **Target Database**.

![](https://i.postimg.cc/RhDYTD79/gb0054.jpg)

Введем свойства подключения, такие как – если это проверка подлинности SQL Server, то указываем имя сервера, имя пользователя, пароль и выбираем базу; а если это аутентификация Windows, то указываем имя сервера и базу данных.

![](https://i.postimg.cc/281M5CY5/gb0055.jpg)

![](https://i.postimg.cc/8cjKsmqY/gb0056.jpg)

После чего мы жмем на кнопку Publish. Немного подождем, пока БД не будет опубликована.

![](https://i.postimg.cc/zBd2JcPW/gb0057.jpg)

Теперь запускаем SQL Server Management Studio и проверяем, есть ли база данных SampleDB или нет.

![](https://i.postimg.cc/Zn2fNym5/gb0058.jpg)

### Вывод
В этой статье мы узнали, как создать проект базы данных в Visual Studio 2019 и публиковать ту же БД в SQL Server 2017.

Переведен и переработан [оригинал](https://www.c-sharpcorner.com/article/create-database-project-in-visual-studio-2015/)