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

Согласно информации с [hypestat](https://hypestat.com/info/booking.com) и с [businessofapps](https://www.businessofapps.com/data/booking-statistics/):

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
* В каждый момент времени в сервисе размещается до 100 000 000 объявлений (здесь предположим, что каждый арендодатель, в среднем, за все время разместил не более 10 объявлений, а если аккаунтов в системе 10 000 000, то умножаем на 10)
* В среднем объявление может содержать до 10 картинок
* Количество категорий для объявлений - 20
* Среднее количество запией о попытках бронирования в системе - до 100
* Количество всех отзывов об арендадателей и арендаторах - 500 миллионов.

---

## 2. Расчет нагрузки

### Продуктовые метрики

Согласно [hypestat](https://hypestat.com/info/github.com) количество уникальных пользователей в день составляет около
**13.6M** (DAU).
Месячная аудитория составляет **73M** активных пользователей (MAU).

Исходя из [информации с официального сайта,](https://github.com/about) на платформе создано более 330M
репозиториев. Учитывая, что в 2022 количество новых репозиториев составило 85.7M, то количество репозитореев составляет
примерно **~420M**. Тогда каждый пользователь в среднем имеет `420M /100M = 4.2`, то есть в среднем **4** репозитория на
одного пользователя.
Средний размер репозитория на GitHub может варьироваться в зависимости от типа проекта и содержимого. Однако, в целом,
многие репозитории на GitHub имеют размер от нескольких десятков килобайт до нескольких гигабайт, но большинство
значений попадает в диапазон `1М—30 Мб`.
Поэтому в качетве среднего значения возьмём **15 Мб**.

Пользователь создаёт **~2** Pull Requests в неделю, исходя из большинства открытых репозиториев на github, в среднем в
репозитории 5 Pull Requests, тогда учитывая, что один Pull Request занимает примерно **1 Кб**, в репозитории Pull
Requests занимают **~5 Кб**.

В результате опроса знакомых и анализа открытых репозиториев было выявлено, что в одном репозитории около 15
комментариев, а средняя длина комментария 100 символов ~ **1.47 Кб**.

По личному опыту и опросу знакомых, один пользователь создает около **2** Issues в месяц, а каждый
репозиторий имеет в среднем **5** Issues, предположим, что 1 Issue это 256 байт, тогда в репозитории они будут занимать
около **1.25 Кб**.

Получаем средний размер хранилища пользователя:

```
(15 * 4) Мб + 5 Кб + 1.25 Кб + 1.47 Кб = 60 Мб
```

#### Среднее количество действий пользователя по типам:

| Тип действия                         | Количество/период |
|--------------------------------------|:-----------------:|
| Создание репозитория                 |     1 в месяц     |
| Клонирование репозитория             |     2 в месяц     |
| Загрузка новых данных из репозитория |     3 в день      |
| Редактирование репозитория           |     5 в день      |
| Открытие Pull Request                |    2 в неделю     |
| Просмотр Pull Request                |     2 в день      |
| Добавление комментария               |     2 в день      |
| Просмотр комментариев                |     2 в день      |
| Открытие Issue                       |     1 в месяц     |
| Просмотр Issue                       |     1 в день      |

### Технические метрики

#### Хранилище

- Репозитории: `420М * 15 МБ = 6300 Тб`
- Pull Requests: `420М * 5 Кб = 2.1 Тб`
- Issues: `420М * 1.25 Кб = 525 Гб`
- Комментарии: `420М * 1.47 Кб = 617.4 Гб`

#### Сетевой трафик и rps

Так как количество уникальных пользователей в
день составляет 13.6M, то в качестве дневной аудитории возьмём **40M**, так как часть пользователей посещает сервис
несколько раз в течение дня.

Согласно [hypestat](https://hypestat.com/info/github.com), пользователь в среднем посещает 6.69 страниц в день, округлим
это число до **7** страниц в день.
На стороне клиента в загруженном JS действует механизм кэширования и при повторном переходе на страницу, она не
загружается с сервера или же используются другие механизмы оптимизации. Таким образом, фактических отдач страниц с
сервера может быть не 7, а меньше. Для простоты будем считать, что 7 посещаемых страниц - это фактически полноценная
отдача данных без механизмов кэширования (рассматриваем худший для сервиса
сценарий).

Будем предполагать, что из 7 страниц:

- стартовая страница
- страница со списком репозиториев пользователя
- 2 страницы кода выбранного репозитория
- страница с Pull Requests
- страница Issues
- страница профиля пользователя

Используя. "инструменты разработчика" в браузере мы можем примерно рассчитать размер .html, .js и .css файлов для
отрисовки каждой из страниц и количество запросов для их получения, в качестве данных возьмём средний результат
знакомых:

| Страница                         | Размер в Кб | Кол-во запросов |
|----------------------------------|-------------|-----------------|
| стартовая страница               | 742         | 71              |
| список репозиториев пользователя | 793         | 87              |
| код репозитория                  | 783         | 90              |
| Pull Requests                    | 620         | 71              |
| Issues                           | 611         | 68              |
| профиль пользователя             | 740         | 74              |

Получаем средний размер трафика и запросов для **статики на одного пользователя в день**:

```azure
Трафик: 742 + 793 + 783*2 + 620 + 611 + 740 = 4.9 Мб
Кол-во
запросов: 71 + 87 + 90*2 + 71 + 68 + 74 = 551
```

Тогда учитывая количество пользователей, получаем:

```azure
Трафик: 4.9 Мб * 40М / 86 400 = 2.2 Гб/c
RPS: 551 * 40М / 86 400 = 255 000
```

Для статических ресурсов мы предполагаем использование CDN (Content Delivery Network), чтобы обеспечить масштабируемость
и быструю доставку контента. Поэтому объем трафика и количество запросов в секунду (RPS) для статики будут
обрабатываться и обслуживаться CDN, а мы можем учитывать только получение динамического контента и продуктовые запросы
для нашего сервиса.

Рассмотрим запросы из продуктовых требований для расчёта сетевой нагрузки. Для рассчёта RPS используем формулу:

```azure
 <дневная аудитория> * <средняя частота выполнения данного запроса в сутки одним пользователем> / 86 400(кол-во секунд в сутках)
```

Для рассчёта трафика:

```azure
<средний объём данных переданных по сети для данного типа запроса> * RPS
```

1. Создание репозитория

```
RPS: 40М / 86 400 / 30 = 15.43
Трафик: 3.9 * 15.43 = 60.2 Кб/с 
```

2. Клонирование репозитория

```
RPS: 40М / 86 400 * 2 / 30 = 30.9
Трафик: 15360 * 30.9 = 0,47 Гб/с 
```

3. Загрузка новых данных из репозитория (git pull)

```
RPS: 40М / 86 400 * 3 = 1389
Трафик: 3.6 * 1389 = 5 Мб/с 
```

4. Редактирование репозитория

```
RPS: 40М / 86 400 * 5 = 2315
Трафик: 3.3 * 2315 = 7.6 Мб/с 
```

5. Открытие Pull Request

```
RPS: 40М / 86 400 * 2/7 = 132.3
Трафик: 3.4 * 132.3 = 0.5 Мб/с 
```

6. Просмотр Pull Request

```
RPS: 40М / 86 400 * 2 = 926
Трафик: 50 * 926 = 46.3 Мб/с 
```

7. Добавление комментария

```
RPS: 40М / 86 400 * 2 = 926
Трафик: 19 * 926 = 17.6 Мб/с
```

8. Просмотр комментариев

```
RPS: 40М / 86 400 * 2 = 926
Трафик: 90 * 926 = 83.34 Мб/с 
```

9. Открытие Issues

```
RPS: 40М / 86 400 / 30 = 15.43
Трафик: 3.3 * 15.43 = 51 Кб/с 
```

10. Просмотр Issues

```
RPS: 40М / 86 400 = 463
Трафик: 37 * 463 = 16.72 Мб/с 
```

10. Поиск

```
RPS: 40М / 86 400 = 463
Трафик: 0,11 * 463 = 50 Мб/с 
```

#### В итоге

| Запрос                                          |  RPS  |   Трафик   |   
|-------------------------------------------------|:-----:|:----------:|
| Создание репозитория                            | 15.43 | 60.2  Кб/с |
| Клонирование репозитория                        | 30.9  | 0,47 Гб/с  |
| Загрузка новых данных из репозитория (git pull) | 1389  |   5 Мб/с   |
| Редактирование репозитория                      | 2315  |  7.6 Мб/с  |
| Открытие Pull Request                           | 132.3 |  0.5 Мб/с  |
| Просмотр Pull Request                           |  926  | 46.3  Мб/с |
| Добавление комментария                          |  926  | 17.6 Мб/с  |
| Просмотр комментариев                           |  926  | 83.34 Мб/с |
| Открытие Issues                                 | 15.43 |  51  Кб/с  |
| Просмотр Issues                                 |  463  | 16.72 Мб/с |
| Поиск                                           |  463  |  50 Мб/с   |
| **Общие значения**                              | 7602  | 0.58 Гб/с  |
| **При пиковой нагрузке, х2**                    | 15204 | 1.16 Гб/с  |
