# Booking

---

## 1. Тема и целевая аудитория

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

В сети не найдено информации сколько пользователей существует в booking.com и сколько объявлений в среднем хранится в базе данных.

Ясно, что 500 миллионов посещений в месяц - это в большинстве не авторизованные пользователи. Предположим, что в booking.com зарегистрировано 500 миллионов пользователей-арендаторов (примерно 6.25% населения земли) и 10 миллионов пользователей-арендодателей.
Также, учитывая данные исследовния [OneTwoTrip](https://ria.ru/20190913/1558631353.html), возьмем, что в 20% случаев арендаторы оставляют отзывы после каждой брони жилья. Преположим, что в среднем каждый пользователь за все время существования сервиса сделал 5 бронирований. Получим:
```
500.000.000 * 5 * 0.2 = 500.000.000
```
Будем считать, что число всех отзывов об арендадателе и арендаторе равно, т.е. 500 миллионов у арендаторов и арендадателей.

Таким образом, будем считать, что: 
* В системе зарегистрировано до 10 000 000 пользователей-арендодателей
* В системе зарегистрировано до 500 000 000 пользователей-арендаторов
* В каждый момент времени в сервисе размещается до 30 000 000 объявлений
* В среднем объявление может содержать до 10 картинок
* Количество категорий для объявлений - 20
* Среднее количество запией о попытках бронирования в системе - до 100
* Количество всех отзывов об арендадателей и арендаторах - 500 миллионов.

---

## 2. Расчет нагрузки

### Продуктовые метрики

Согласно [hypestat](https://hypestat.com/info/booking.com) количество уникальных пользователей в день составляет около
**18M** (DAU).
Месячная аудитория составляет **550M** активных пользователей (MAU).

При расчете размера хранилища будем учитывать профили пользователей, объявления, данные о совершенных транзакциях за последние 5 лет.
Для хранения изображений будем использовать CDN, следовательно, размер изображений в хранилище учитывать не будем.

Средний размер профиля пользователя включающим в себя персональные данные пользователя, никнейм, ссылку на аватар и контактные данные(номер телефона, email) равным 1.5 КБ.
Средний размер объявления включающего в себя ссылки на изображения, и информацию об объявлении примем равным 50 КБ.
Средний размер данных с информацией об одной транзакции 0.5 КБ.

За последний год было совершено 895 млн. бронирований. Получим размер транзакций за один год = 447.5 ГБ.
За последние 5 лет было совершено 3444 млн. транзакций, следовательно, объем данных о транзакциях за последние 5 лет = 1.7 ТБ.


| Метрика                               | Значение |
|---------------------------------------|----------|
| Месячная аудитория                    | 550 млн  |
| Зарегистрированных пользователей      | 500 млн  |
| Дневная аудитория                     | 18 млн   |
| Средний размер хранилища пользователя | 1.5 КБ   |
| Размещенных объявлений                | 30 млн   |

#### Среднее значение действий пользователя в день:

| Действие                      | Среднее количество в день на пользователя |
|-------------------------------|-------------------------------------------|
| Поиск по параметрам           | 2                                         |
| Получение объявления          | 6                                         |
| Отзывы объявления  ммм        | 1                                         |
| Загрузка/изменение объявления | 0.1                                       |
| Регистрация/Авторизация       | 0.5                                       |
| Бронирование                  | 0.2                                       |

### Технические метрики:

#### Объем хранилища:

Средний размер хранилища на объявление - 50 КБ, количество объявлений - 30 млн. => Размер хранилища на объявления

```30 млн. * 50 КБ = 1.5 ТБ``` 

Средний размер хранилища на профиль - 1.5 КБ, количество пользователей 500 млн => Размер хранилища на пользователей 

```500 млн * 1.5 КБ = 750 ГБ```

Средний размер хранилища на транзакцию - 0.5 КБ, количество транзакций за последние 5 лет в среднем 4475 млн. => Размер хранилища на транзакции

```4475 млн. * 0.5 КБ = 2.3 ТБ```

Средний размер хранилища на отзыв - 1 КБ, количество объявлений - 30 млн. и аурендаторов - 10 млн. Возьмем по 5 отзывов на арендатора и 100 на объявление арендадателя => Размер хранилища на отзывы

```30 млн. * 1 КБ * 100 + 10 млн. * 1 КБ * 5 = 3.1 ТБ```

Общий размер хранилища примерно равен 7.65 ТБ.

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
Трафик: 613 + 1000 + 455*2 + 770 = 3.3 Мб
Кол-во
запросов: 260 + 560 + 40*2 + 190 = 1090
```

Тогда учитывая количество пользователей, получаем:

```azure
Трафик: 3.3 Мб * 500М / 86 400 = 19 Гб/c
RPS: 1090 * 500М / 86 400 = 6.300.000
```

