# Определения и термины

- Программное обеспечение (ПО) – программа или множество программ, используемых для управления компьютером.

- Библиотека – сборник подпрограмм или объектов, используемых для разработки программного обеспечения.

- LibSL – язык спецификации компонентов программного обеспечения.

- Подсветка синтаксиса – выделение синтаксических конструкций текста с использованием различных цветов, шрифтов и начертаний. 

- Конечный автомат – абстрактная математическая модель, представленная в виде ориентированного графа, вершины котрого характеризуют текущее состояние автомата, а дуги между вершинами характеризуют возможные переходы между состояниями, осуществляемые в зависимости от входных данных.

- PAP (Password Authentication Protocol) – протокол аутентификации, предусматривающий отправку имени пользователя и пароля на сервер аутентификации.

- OAuth – протокол авторизации, обеспечивающий предоставление третьей стороне ограниченного доступа к защищённым ресурсам пользователя без передачи ей (третьей стороне) данных для аутентификации.

# Общие положения

Требуется реализовать сетевую систему хранения, отображения и редактирования спецификаций программных библиотек на языке LibSL. 

Система дожлна предоставлять пользователям следующие возможности:

- любой пользователь может осуществлять навигацию по каталогу загруженных в систему спецификаций на языке LibSL;

- любой пользователь может скачивать или просматривать имеющиеся в файловой системе файлы спецификаций;

- отображение спецификаций должно быть представлено в 2 вариантах:
  
  - текстовое содержание файла спецификации на языке LibSL с подсветкой синтаксиса;
  
  - визуализация конечных автоматов, описанных в файле спецификации при помощи синтаксической конструкции `automaton`;

- любой пользователь может авторизироваться;

- авторизованный пользователь может загружать новые файлы спецификации LibSL;
  
  - при загрузке для спецификаций должна задаваться метаинформация о специфицируемой библиотеке;
  
  - при загрузке спецификации должны пройти проверку на синтаксическую корректность;

# Требования, ограничения и допущения

## EPIC: Авторизация пользователей

### STORY: Создание аккаунта суперпользователя

### STORY: Регистрация новых пользователей

### STORY: Аутентификация пользователей по протоколу PAP

### STORY: Аутентификация пользвателя по протоколу OAuth

### STORY: Отображение окна аутентификации

### STORY: Отображение окна регистрации

## 

## EPIC: Навигация по имеющимся спецификациям

### STORY: Фильтрация отображаемых спецификаций

### STORY: Навигация между элементами хранилища

### STORY: Отображение хранилища спецификаций

### STORY: Отображение параметров фильрации спецификаций

### STORY: Отображение панели управления

## 

## EPIC: Просмотр спецификаций

### STORY: Отображение мета-информации спецификации

### STORY: Отображение содержимого спецификаций

### STORY: Отображение визуализации конечных автоматов спецификаций

### STORY: Отображение подсветка синтаксических конструкций LibSL

## EPIC: Изменение спецификаций

### STORY: Редактирование содержимого спецификации

### STORY: Удаление спецификаций

### STORY: Отображение редактора мета-информации спецификации

### STORY: Отображение редактора содержимого спецификации

### STORY: Проверка авторизации при попытке изменить спецификацию

## EPIC: Импорт спецификаций

### STORY: Отображение окна выбора файлов

### STORY: Загрузка файлов

## EPIC: Развертывание системы

### STORY: Создание docker-compose инфраструктуры

На данный момент планируется деление проекта на три контейнера:

- БД

- Фронтэнд - веб-сервер

- Бэкэнд - реализация бизнес-логики

Для обеспечения взаимодействия контейнеров между собой планируется использование двух внутренних docker-сетей:

- БД-бэкэнд

- бэкэнд-фронтэнд

Следует отметить, что контейнер с веб-сервером должен иметь доступ к внешней сети для протоколов http/https.

### STORY: Настройка веб-сервера

Необходимо обеспечить как сборку проекта с фронтэндом, так и развёртывание артефактов сборки (сайт) на веб-сервере (e.g. Nginx). 

Так как требуется обеспечить подключение как с использованием http, так и с использованием https, необходимо озаботиться сертификатами (использовать let's encrypt). 

### STORY: Настройка бэкэнда

Необходимо обеспечить сборку бэкэнда с использованием выбранной системы сборки (e.g. Gradle) и запуском полученного в результате сборки артефакта.

### STORY: Настройка БД

Необходимо настроить запуск контейнера с БД (e.g. Postgres) с сохранением данных в volume и первичной инициализацией при отсутствии данных (пустом volume). Данные для доступа к БД будут находиться во внешнем .conf-файле и записываться в глобальные переменные бэкэнд-контейнера при его запуске.

### STORY: Настроить CI

В рамках реализации CI необходимо настроить автоматический запуск автотестов при появлении MR или коммите в main и develop-ветки.

### STORY: Настроить CD

Необходимо настроить автосборку контейнера и его выгрузку в docker registry для последующего автоматического обновления на конечном сервере с импользованием watchtower-контейнера.
