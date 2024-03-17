# Booking

---

## 1. Тема и целевая аудитория.

**Booking.com** — система интернет-бронирования отелей, основанная в 1996 году в Амстердаме (Нидерланды).
Компания прошла путь от маленького голландского стартапа до одного из мировых цифровых лидеров в сфере путешествий. Миссия Booking.com, подразделения Booking Holdings Inc. (NASDAQ: BKNG), — делать путешествия доступными каждому.


### MVP

- Поиск с фильтрами по объявлениям.
- Объявления с фотографиями.
- Бронирование объявлений.
- Профиль арендодателя.
- Рейтинг арендодателя.
- Профиль арендатора.
- Рейтинг арендатора.
- Статус объявления.


### Целевая аудитория

Согласно информации с [Booking.com](https://www.booking.com/content/about.en-gb.html), [hypestat](https://hypestat.com/info/booking.com) и [businessofapps](https://www.businessofapps.com/data/booking-statistics/):

- 500+ миллионов посещений в месяц.
- 18+ миллионов пользователей в день.
- В 2022 было забронировано 895 миллионов ночей.
- Самая многочисленная возрастная группа посетителей: 25 - 34 лет.
- В среднем, пользователи проводят на ресурсе более 8 минут за сессию.
- В среднем, пользователи на сайте открывают 8 страниц за сессию.

#### Демография аудитории Booking

![Демография аудитории Booking](images/image.png)

#### Количество пользователей Booking по странам

| Страна            | Процент пользователей от общего числа |
|-------------------|:-------------------------------------:|
| Соединенные Штаты |                 10.06%                 |
| Великобритания    |                 7.89%                  |
| Германия          |                 7.38%                  |
| Франция           |                 5.61%                  |
| Италия            |                 5.59%                  |

![Количество пользователей Booking по странам](images/booking-users.jpg)

Предположим, что в booking.com зарегистрировано 500 миллионов пользователей-арендаторов и 10 миллионов пользователей-арендодателей.
Также, учитывая данные исследовния [OneTwoTrip](https://ria.ru/20190913/1558631353.html), возьмем, что в 5% случаев арендаторы оставляют отзывы после каждой брони жилья. Преположим, что в среднем каждый пользователь за все время существования сервиса сделал 5 бронирований. Получим:
```
500.000.000 * 5 * 0.05 = 125.000.000
```
Будем считать, что число всех отзывов об арендадателе и арендаторе равно, т.е. 125 миллионов у арендаторов и арендадателей. В среднем объявление может содержать до 10 картинок. В сервисе размещается до 30 000 000 объявлений.

---

## 2. Расчет нагрузки.

### Продуктовые метрики

Согласно [hypestat](https://hypestat.com/info/booking.com) количество уникальных пользователей в день составляет около
**18M** (DAU).
Месячная аудитория составляет **550M** активных пользователей (MAU).

Средний размер профиля пользователя включающим в себя персональные данные пользователя, никнейм, аватар и контактные данные(номер телефона, email) равным 1.5 КБ.

Используя данные с [similarweb](https://www.similarweb.com/ru/website/booking.com/#geography) возьмем данное разбиение по регионам:

| Регион                  | Процент от общего количества пользователей |    MAU    |   DAU   |
|-------------------------|--------------------------------------------|-----------|---------|
| Северная Америка        |                     25%                    | 137.5 млн | 4.5 млн |
| Южная Америка           |                     15%                    | 85.5  млн | 2.7 млн |
| Европа                  |                     35%                    | 192.5 млн | 6.3 млн |
| Азия (влючая Австралию) |                     20%                    | 110   млн | 3.6 млн |
| Африка                  |                      5%                    | 27.5  млн | 0.9 млн |

#### Среднее значение действий пользователя в день:

| Действие                          | Среднее количество в день на пользователя |
|-----------------------------------|-------------------------------------------|
| Поиск по параметрам               | 2                                         |
| Получение объявления (с отзывами) | 6                                         |
| Загрузка/изменение объявления     | 0.1                                       |
| Регистрация/Авторизация           | 0.5                                       |
| Бронирование                      | 0.2                                       |

### Технические метрики:

#### Объем хранилища:

---

#### Общий объем:

Средний размер хранилища на транзакцию - 0.5 КБ, количество транзакций за последние 5 лет в среднем 4475 млн. Размер хранилища на транзакции

```4475 млн. * 0.5 КБ = 2.3 ТБ```

Средний размер хранилища на отзыв - 1 КБ, количество объявлений - 30 млн. и аурендаторов - 10 млн. Возьмем по 5 отзывов на арендатора и 100 на объявление арендадателя => Размер хранилища на отзывы

```30 млн. * 1 КБ * 100 + 10 млн. * 1 КБ * 5 = 3.05 ТБ```

Средний размер хранилища на объявление - 130 КБ, количество объявлений - 30 млн. Размер хранилища на объявления

```30 млн. * 130 КБ = 3.9 ТБ``` 

Средний размер хранилища на профиль - 1.5 КБ, количество пользователей 500 млн. Размер хранилища на пользователей 

```500 млн * 1.5 КБ = 750 ГБ```

Общий размер хранилища примерно равен `10 ТБ.`

---

#### Северная Америка:

Средний размер хранилища на объявление - `130 КБ`, количество объявлений -  `30 млн. * 25%` => Размер хранилища на объявления

```30 млн. * 0.25 * 130 КБ = 0.975 ТБ``` 

Средний размер хранилища на профиль - `1.5 КБ`, количество пользователей `500 млн. * 25%`=> Размер хранилища на пользователей 

```500 млн. * 0.25 * 1.5 КБ = 187.5 ГБ```

Средний размер хранилища на транзакцию - `0.5 КБ`, количество транзакций за последние 5 лет в среднем `4475 млн. * 25%` => Размер хранилища на транзакции

```4475 млн. * 0.25 * 0.5 КБ = 0.575 ТБ```

Средний размер хранилища на отзыв - `1 КБ`, количество объявлений - `30 млн. * 25%` и арендаторов - `10 млн. * 25%`. Возьмем по 5 отзывов на арендатора и 100 на объявление арендадателя => Размер хранилища на отзывы

```30 млн. * 0.25 * 1 КБ * 100 + 10 млн. * 0.25 * 1 КБ * 5 = 0.7625 ТБ```

Общий размер хранилища примерно равен `2.5 ТБ.`

---

#### Южная Америка:

Средний размер хранилища на объявление - `130 КБ`, количество объявлений -  `30 млн. * 15%` => Размер хранилища на объявления

```30 млн. * 0.15 * 130 КБ = 0.585 ТБ``` 

Средний размер хранилища на профиль - `1.5 КБ`, количество пользователей `500 млн. * 15%`=> Размер хранилища на пользователей 

```500 млн. * 0.25 * 1.5 КБ = 112.5 ГБ```

Средний размер хранилища на транзакцию - `0.5 КБ`, количество транзакций за последние 5 лет в среднем `4475 млн. * 25%` => Размер хранилища на транзакции

```4475 млн. * 0.15 * 0.5 КБ = 0.345 ТБ```

Средний размер хранилища на отзыв - `1 КБ`, количество объявлений - `30 млн. * 15%` и арендаторов - `10 млн. * 15%`. Возьмем по 5 отзывов на арендатора и 100 на объявление арендадателя => Размер хранилища на отзывы

```30 млн. * 0.15 * 1 КБ * 100 + 10 млн. * 0.15 * 1 КБ * 5 = 0.4575 ТБ```

Общий размер хранилища примерно равен `1.5 ТБ.`

---

#### Европа:

Средний размер хранилища на объявление - `130 КБ`, количество объявлений -  `30 млн. * 35%` => Размер хранилища на объявления

```30 млн. * 0.35 * 130 КБ = 1.365 ТБ``` 

Средний размер хранилища на профиль - `1.5 КБ`, количество пользователей `500 млн. * 35%`=> Размер хранилища на пользователей 

```500 млн. * 0.35 * 1.5 КБ = 262.5 ГБ```

Средний размер хранилища на транзакцию - `0.5 КБ`, количество транзакций за последние 5 лет в среднем `4475 млн. * 35%` => Размер хранилища на транзакции

```4475 млн. * 0.35 * 0.5 КБ = 0.805 ТБ```

Средний размер хранилища на отзыв - `1 КБ`, количество объявлений - `30 млн. * 35%` и арендаторов - `10 млн. * 35%`. Возьмем по 5 отзывов на арендатора и 100 на объявление арендадателя => Размер хранилища на отзывы

```30 млн. * 0.35 * 1 КБ * 100 + 10 млн. * 0.35 * 1 КБ * 5 = 1.0675 ТБ```

Общий размер хранилища примерно равен `3.5 ТБ.`

---

#### Азия (влючая Австралию):

Средний размер хранилища на объявление - `130 КБ`, количество объявлений -  `30 млн. * 20%` => Размер хранилища на объявления

```30 млн. * 0.20 * 130 КБ = 0.78 ТБ``` 

Средний размер хранилища на профиль - `1.5 КБ`, количество пользователей `500 млн. * 20%`=> Размер хранилища на пользователей 

```500 млн. * 0.20 * 1.5 КБ = 150 ГБ```

Средний размер хранилища на транзакцию - `0.5 КБ`, количество транзакций за последние 5 лет в среднем `4475 млн. * 20%` => Размер хранилища на транзакции

```4475 млн. * 0.20 * 0.5 КБ = 0.4475 ТБ```

Средний размер хранилища на отзыв - `1 КБ`, количество объявлений - `30 млн. * 20%` и арендаторов - `10 млн. * 20%`. Возьмем по 5 отзывов на арендатора и 100 на объявление арендадателя => Размер хранилища на отзывы

```30 млн. * 0.20 * 1 КБ * 100 + 10 млн. * 0.20 * 1 КБ * 5 = 0.601 ТБ```

Общий размер хранилища примерно равен `2 ТБ.`

---

#### Африка:

Средний размер хранилища на объявление - `130 КБ`, количество объявлений -  `30 млн. * 5%` => Размер хранилища на объявления

```30 млн. * 0.05 * 130 КБ = 0.195 ТБ``` 

Средний размер хранилища на профиль - `1.5 КБ`, количество пользователей `500 млн. * 5%`=> Размер хранилища на пользователей 

```500 млн. * 0.05 * 1.5 КБ = 37.5 ГБ```

Средний размер хранилища на транзакцию - `0.5 КБ`, количество транзакций за последние 5 лет в среднем `4475 млн. * 5%` => Размер хранилища на транзакции

```4475 млн. * 0.05 * 0.5 КБ = 0.115 ТБ```

Средний размер хранилища на отзыв - `1 КБ`, количество объявлений - `30 млн. * 5%` и арендаторов - `10 млн. * 5%`. Возьмем по 5 отзывов на арендатора и 100 на объявление арендадателя => Размер хранилища на отзывы

```30 млн. * 0.05 * 1 КБ * 100 + 10 млн. * 0.05 * 1 КБ * 5 = 0.1525 ТБ```

Общий размер хранилища примерно равен `0.5 ТБ.`

---

#### Сетевой трафик и RPS

Используя. "инструменты разработчика" в браузере мы можем примерно рассчитать размер .html, .js и .css файлов для
отрисовки каждой из страниц и количество запросов для их получения, в качестве данных возьмём средний результат
знакомых:

| Страница                         | Размер в Кб | Кол-во запросов |
|----------------------------------|-------------|-----------------|
| Поиск по параметрам              | 613         | 260             |
| Получение объявления(с отзывами) | 1000        | 560             |
| Регистрация/Авторизация          | 455         | 40              |
| Бронирование                     | 770         | 190             |

Получаем средний размер трафика и запросов для **статики на одного пользователя в день**:

```azure
Трафик: 613 * 2 + 1000 * (6 + 1) + 455 + 770 = 9.5 Мб
Кол-во
запросов: 260 * 2 + 560 * (6 + 1) + 40 + 190 = 4670
```

Тогда учитывая `18M MAU`, получаем:

```azure
Трафик: 9.5 Мб * 18М / 86 400 = 1.98 Гб/c
RPS: 4670 * 18М / 86 400 = 973 000
```

---

#### Северная Америка:

Учитывая `18M * 25% MAU`, получаем:

##### Поиск по параметрам

```azure
Трафик: 0.6 Мб * 18М * 0.25 * 2 / 86 400 = 62.5 МБ/c
RPS: 260 * 18М * 0.25 * 2 / 86 400 = 27 000
```

##### Получение объявления (с отзывами)

```azure
Трафик: 1 Мб * 18М * 0.25 * 6 / 86 400 = 312.5 МБ/c
RPS: 560 * 18М * 0.25 * 6 / 86 400 = 175 000
```

##### Загрузка/изменение объявления

```azure
Трафик: 1 Мб * 18М * 0.25 * 0.1 / 86 400 = 5.2 МБ/c
RPS: 560 * 18М * 0.25 * 0.1 / 86 400 = 2 917
```

##### Регистрация/Авторизация

```azure
Трафик: 0.455 Мб * 18М * 0.25 * 0.5 / 86 400 = 11.85 МБ/c
RPS: 40 * 18М * 0.25 * 0.5 / 86 400 = 1 042
```

##### Бронирование

```azure
Трафик: 0.77 Мб * 18М * 0.25 * 0.2 / 86 400 = 8.02 МБ/c
RPS: 190 * 18М * 0.25 * 0.2 / 86 400 = 1 980
```

---

#### Южная Америка:

Учитывая `18M * 15% MAU`, получаем:

##### Поиск по параметрам

```azure
Трафик: 0.6 Мб * 18М * 0.15 * 2 / 86 400 = 37.5 МБ/c
RPS: 260 * 18М * 0.15 * 2 / 86 400 = 16 250
```

##### Получение объявления (с отзывами)

```azure
Трафик: 1 Мб * 18М * 0.15 * 6 / 86 400 = 187.5 МБ/c
RPS: 560 * 18М * 0.15 * 6 / 86 400 = 105 000
```

##### Загрузка/изменение объявления

```azure
Трафик: 1 Мб * 18М * 0.15 * 0.1 / 86 400 = 3.125 МБ/c
RPS: 560 * 18М * 0.15 * 0.1 / 86 400 = 1 750
```

##### Регистрация/Авторизация

```azure
Трафик: 0.455 Мб * 18М * 0.15 * 0.5 / 86 400 = 7.11 МБ/c
RPS: 40 * 18М * 0.15 * 0.5 / 86 400 = 625
```

##### Бронирование

```azure
Трафик: 0.77 Мб * 18М * 0.15 * 0.2 / 86 400 = 4.82 МБ/c
RPS: 190 * 18М * 0.15 * 0.2 / 86 400 = 1 188
```

---

#### Европа:

Учитывая `18M * 35% MAU`, получаем:

##### Поиск по параметрам

```azure
Трафик: 0.6 Мб * 18М * 0.35 * 2 / 86 400 = 87.5 МБ/c
RPS: 260 * 18М * 0.35 * 2 / 86 400 = 37 917
```

##### Получение объявления (с отзывами)

```azure
Трафик: 1 Мб * 18М * 0.35 * 6 / 86 400 = 437.5 МБ/c
RPS: 560 * 18М * 0.35 * 6 / 86 400 = 245 000
```

##### Загрузка/изменение объявления

```azure
Трафик: 1 Мб * 18М * 0.35 * 0.1 / 86 400 = 7.3 МБ/c
RPS: 560 * 18М * 0.35 * 0.1 / 86 400 = 4 084
```

##### Регистрация/Авторизация

```azure
Трафик: 0.455 Мб * 18М * 0.35 * 0.5 / 86 400 = 16.59 МБ/c
RPS: 40 * 18М * 0.35 * 0.5 / 86 400 = 1 459
```

##### Бронирование

```azure
Трафик: 0.77 Мб * 18М * 0.35 * 0.2 / 86 400 = 11.23 МБ/c
RPS: 190 * 18М * 0.35 * 0.2 / 86 400 = 2 771
```

---

#### Азия (влючая Австралию):

Учитывая `18M * 20% MAU`, получаем:

##### Поиск по параметрам

```azure
Трафик: 0.6 Мб * 18М * 0.20 * 2 / 86 400 = 50 МБ/c
RPS: 260 * 18М * 0.20 * 2 / 86 400 = 21 667
```

##### Получение объявления (с отзывами)

```azure
Трафик: 1 Мб * 18М * 0.20 * 6 / 86 400 = 250 МБ/c
RPS: 560 * 18М * 0.20 * 6 / 86 400 = 140 000
```

##### Загрузка/изменение объявления

```azure
Трафик: 1 Мб * 18М * 0.20 * 0.1 / 86 400 = 4.17 МБ/c
RPS: 560 * 18М * 0.20 * 0.1 / 86 400 = 2 334
```

##### Регистрация/Авторизация

```azure
Трафик: 0.455 Мб * 18М * 0.20 * 0.5 / 86 400 = 9.48 МБ/c
RPS: 40 * 18М * 0.20 * 0.5 / 86 400 = 834
```

##### Бронирование

```azure
Трафик: 0.77 Мб * 18М * 0.20 * 0.2 / 86 400 = 6.42 МБ/c
RPS: 190 * 18М * 0.20 * 0.2 / 86 400 = 1 584
```

---

#### Африка:

Учитывая `18M * 5% MAU`, получаем:

##### Поиск по параметрам

```azure
Трафик: 0.6 Мб * 18М * 0.05 * 2 / 86 400 = 12.5 МБ/c
RPS: 260 * 18М * 0.05 * 2 / 86 400 = 5 417
```

##### Получение объявления (с отзывами)

```azure
Трафик: 1 Мб * 18М * 0.05 * 6 / 86 400 = 62.5 МБ/c
RPS: 560 * 18М * 0.05 * 6 / 86 400 = 35 000
```

##### Загрузка/изменение объявления

```azure
Трафик: 1 Мб * 18М * 0.05 * 0.1 / 86 400 = 1.05 МБ/c
RPS: 560 * 18М * 0.05 * 0.1 / 86 400 = 584
```

##### Регистрация/Авторизация

```azure
Трафик: 0.455 Мб * 18М * 0.05 * 0.5 / 86 400 = 2.37 МБ/c
RPS: 40 * 18М * 0.05 * 0.5 / 86 400 = 209
```

##### Бронирование

```azure
Трафик: 0.77 Мб * 18М * 0.05 * 0.2 / 86 400 = 1.61 МБ/c
RPS: 190 * 18М * 0.05 * 0.2 / 86 400 = 396
```

---

## 3. Глобальная балансировка нагрузки.

### Нахождение ЦОДов

Основываясь на [карту популяции мира](https://www.luminocity3d.org/WorldPopDen), процент трафик и DAU были расположеный ЦОДы в: Лондон(Великобритания), Цюрих(Швейцария), Рим(Италия), Нью-Йорк(США), Лос-Анджелес(США), Сеул(Южная Корея), Джакарта(Индонезия), Сантьяго(Чили), Рио-де-Жанейро(Бразилия), Найроби(Кения).

- Самый большой трафик приходится на Европу (35% от всего трафика и 6.3 млн. DAU), это важнейший регион, в котором важна отказаустойчивость и присутсвует высокая нагрузка. В нем будет располагаться 3 дата-центра: Лондон(Великобритания), Цюрих(Швейцария) и Рим(Италия).

  ![image](https://github.com/scremyda/Coursework_Highload_VK/assets/63557586/50fccfab-a4cb-402e-852b-0488ed6f2267)

- Второй по величине трафик идет из Северной Америки (25% от всего трафика и 4.5 млн. DAU). Для него будут расположены 2 дата-центра: Нью-Йорк(США) и Лос-Анджелес(США).

  ![image](https://github.com/scremyda/Coursework_Highload_VK/assets/63557586/f49316fb-8d94-4c77-aab4-177adad200d5)

- Третий поток пользоватлей приходит из Азии(влючая Австралию) (20% от всего трафика и 3.6 млн. DAU). Необходимы дата-центры в: Сеул(Южная Корея) и Джакарта(Индонезия). Было принято решение расположить ЦОД в Южной Корее, а не в более густонаселенном Китае, т.к. [санкции со стороны США](https://www.similarweb.com/ru/website/booking.com/#geography) и [вероятность ограничейний Китая](https://habr.com/ru/companies/kingservers/articles/310298/) не позволяют использовать ЦОД подходящей конфигурации без рисков для компании.
  
  ![image](https://github.com/scremyda/Coursework_Highload_VK/assets/63557586/e144a7f5-9d82-4c99-8944-2956f48f7f71)

- Четвертый по величине трафик идет из Южной Америки (15% от всего трафика и 2.7 млн. DAU). Для него будут расположены 2 дата-центра: Сантьяго(Чили) и Рио-де-Жанейро(Бразилия).

  ![image](https://github.com/scremyda/Coursework_Highload_VK/assets/63557586/61d2ad27-2169-43ac-9b70-6119e5eb0150)

- Пятый по величине трафик идет из Африки (5% от всего трафика и 0.9 млн. DAU). Для него будет расположен 1 дата-центр: Найроби(Кения)

  ![image](https://github.com/scremyda/Coursework_Highload_VK/assets/63557586/e769832e-54c2-4c89-9bb6-675706eccec7)

### DNS балансировка
Для обеспечения эффективной балансировки нагрузки и доставки контента в разных регионах, мы можем использовать комбинацию Latency-based DNS и CDN (Content Delivery Network). Благодаря использованию CDN, контент может быть кэширован на серверах, распределенных по всему миру. Это позволяет снизить время загрузки страниц и ресурсов для пользователей в различных регионах, так как они получают контент из ближайших к ним узлов CDN. А c помощью Latency-based DNS мы обеспечим глобальное обслуживание пользователей, направляя их к ближайшему по времени отклика серверу независимо от их местоположения.

### BGP Anycast
Внутри регионов будем использовать BGP Anycast, благодаря чему мы можем направлять пользователей к ближайшему к ним узлу. Это позволяет снизить задержки в передаче данных, улучшить общее качество обслуживания и обеспечить быстрый доступ к сервису в любой точке мира. Более того, благодаря распределению трафика между узлами мы снижаем вероятность успешного осуществления DDoS-атаки, так как атакующим будет сложнее сфокусироваться на одном конкретном узле.

---

## 4. Локальная балансировка нагрузки.

### VRRP
Используем VRRP на маршрутизаторах в каждом датацентре. Основное преимущество VRRP заключается в обеспечении непрерывной доступности к сети в случае отказа одного из активных маршрутизаторов. Если один из маршрутизаторов выходит из строя, другой маршрутизатор автоматически берет на себя его функции и продолжает обслуживать трафик.

### Kubernetes
Проблему отказоустойчивости в рамках сервисов, будет решать Kubernetes. Он предоставляет механизмы для автоматического перезапуска контейнеров в случае их сбоя и обеспечивает механизмы для обнаружения и восстановления. Это позволяет быстро восстанавливать работоспособность сервисов и минимизировать простои.

### L7 балансировщик
Для L7 балансировки будем использовать **Envoy**.
Причины:
- Envoy разработан как высокопроизводительный микросервисный прокси-сервер и способен эффективно обрабатывать трафик даже в микросервисных средах с большим количеством запросов.
- Основной принцип работы Envoy - это динамическая маршрутизация. Он может анализировать запросы и решать, куда направить трафик на основе настраиваемых правил и информации о состоянии микросервисов. Он также поддерживает канареечные релизы и схемы обновления микросервисов. Это делает его идеальным выбором для микросервисных архитектур.
- Envoy спроектирован так, чтобы поддерживать множество протоколов и обеспечивать отказоустойчивость в микросервисных средах.
- Envoy предоставляет множество возможностей, таких как балансировка нагрузки, обработка ошибок, трассировка запросов, логирование и многие другие, что делает его полезным для различных задач.
- Envoy легко интегрируется с современными платформами контейнеризации, такими как Docker и Kubernetes, и автоматически обнаруживает сервисы и контейнеры.

---

## 5. Логическая схема БД.
