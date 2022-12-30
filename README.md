# Анализатор онлайн-курсов
[![.github/workflows/CI.yml](https://github.com/YuriUfimtsev/OnlineCoursesAnalyzer/actions/workflows/CI.yml/badge.svg)](https://github.com/YuriUfimtsev/OnlineCoursesAnalyzer/actions/workflows/CI.yml)

![Image alt](https://github.com/YuriUfimtsev/OnlineCoursesAnalyzer/raw/main/./AppView.png)

[**Анализатор онлайн-курсов**](https://bit.ly/3BUwF2H) - это веб-приложение, которое обрабатывает отчеты о прохождении онлайн-курсов и в удобном виде отображает необходимые данные. Доступно по ссылке: https://bit.ly/3BUwF2H
## Содержание
- [О технологии](#о-технологии)
- [Формат отчетов](#формат-отчетов)
- [Сборка и запуск](#сборка-и-запуск)

## О технологии
Приложение создано для сотрудников учебного отдела матмеха СПбГУ. С его помощью получение информации, необходимой для выставления оценок за онлайн-курс, упрощается: загрузив данные с баллами за итоговый тест, данные с результатами проохождения прокторинга, можно легко получить отсортированный по алфавиту список с почтой, ФИО, посчитанной на основе балла оценкой и статусом прохождения прокторинга каждого студента. Кроме того, приложение позволяет скрыть некоторые элементы для сохранения и печати страницы путем нажатия на "Вид для печати". О статусе текущей операции можно узнать в информационном поле, при нажатии увеличивается.

## Формат отчетов
Поддерживаются два типа отчетов в формате .xlsx. Для каждого приведен список столбцов, наличие которых необходимо для корректной обработки файла.
### О баллах за курс

| Email | Last Name | First Name | Second Name | Контрольные задания (Avg) | Итоговая аттестация (Avg) | Cohort Name |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |

Столбцы **Итоговая аттестация (Avg)** и **Контрольные задания (Avg)** содержат число от 0 до 1, описывающее результат прохождения тестов курса. **Cohort Name** содержит название факультета: например, "матмех" (регистр не учитывается).

### О прохождении прокторинга

| User email | Status is correct |
| ---- | ---- |

Столбец **Status is correct** содержит "yes" либо "no", описывает результат прохождения прокторинга.

Если определенные выше значения для столбцов некорректны для более чем 150 строк, обработка файла прерывается. Аналогично при отсутствии данных о прокторинге для более чем 150 студентов из первого отчета.

## Сборка и запуск
Актуальная версия приложения доступна в виде docker-образа по [ссылке](https://hub.docker.com/repository/registry-1.docker.io/yuriufimtsev/online_courses_analyzer/tags?page=1&ordering=last_updated). Для запуска необходимо наличие установленного [движка Docker](https://docs.docker.com/engine/).

1. Склонируйте докер-образ из репозитория, исполнив команду
~~~
docker pull yuriufimtsev/online_courses_analyzer:latest
~~~

2. Запустите докер-образ с указанием порта
~~~
docker run -d -p 80:82 -e PORT=82 yuriufimtsev/online_courses_analyzer:latest
~~~

3. Приложение доступно по адресу localhost:{PORT}