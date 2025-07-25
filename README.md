# Учебный итоговый проект по курсу "Введение в Data Science" - Анализ сайта «СберАвтоподписка»

## Цели и задачи

1. Проверка следующих гипотез:
- Органический трафик не отличается от платного с точки зрения CR (Conversion Rate) в целевые события.
- Трафик с мобильных устройств не отличается от трафика с десктопных устройств с точки зрения CR (Conversion Rate) в целевые события.
- Трафик из городов присутствия (Москва и область, Санкт-Петербург) не отличается от трафика из иных регионов с точки зрения CR (Conversion Rate) в целевые события.

2. Ответы на вопросы продуктовой команды:
- Из каких источников / кампаний / устройств / локаций к нам идёт самый целевой трафик (и с точки зрения объёма трафика, и с точки зрения CR)?
- Какие авто пользуются наибольшим спросом? У каких авто самый лучший показатель CR (Conversion Rate) в целевые события?
- Стоит ли нам увеличивать своё присутствие в соцсетях и давать там больше рекламы?

## Используемые технологии и инструменты

JupyterLab. Библиотеки: dill, matplotlib, numpy, pandas, scipy, sklearn

## Действия и процесс

### Этап 1: Подготовительная работа

1.1. Чтение данных

- Прочитать данные из предоставленных файлов (ga_sessions.pkl и ga_hits.pkl).
- Использовать оптимизированные методы чтения, например, Dask, или загружать данные частями с помощью chunksize (при необходимости).

1.2. Ознакомление с атрибутами

- Посмотреть структуру данных: типы столбцов, примеры данных, объёмы строк и столбцов. Использовать методы:
 - df.info()
 - df.head()
 - df.describe()

1.3. Оценка полноты данных

- Проверить пропущенные значения с использованием:
 - isna().sum()
 - Написать функцию для анализа пропусков.
- Проанализировать, какие данные можно восстановить, а какие требуют очистки.

1.4. Приведение данных в удобный вид

- Выполнить обработку для:
 - целевых действий,
 - источников трафика,
 - маркировки рекламы в соц сетях.
- Привести данные к нужным типам:
 - Числовые — оптимизировать с помощью astype (например, int32, float32).
 - Текстовые — преобразовать в категориальные (category).
- Удалить ненужные столбцы.

### Этап 2: Разведочный анализ данных (EDA)

2.1. Очистка данных

Удалить дубликаты:

Заполнить или удалить пропущенные значения:
- Для числовых данных — медиана или среднее.
- Для текстовых данных — наиболее частое значение.

2.2. Анализ распределений

- Построить гистограммы для числовых атрибутов.
- Построить бар-чарты для категориальных атрибутов.
- Понять основные паттерны в данных и выявить аномалии.

2.3 Распределение ключевых атрибутов и их связи.

- Построить матрицу корреляций для числовых атрибутов (если они остались после очистки).
- Посмотреть, как ключевые атрибуты (например, utm_source, geo_city, device_category) связаны с целевыми событиями (event_action).
- Возможно, выявить перекосы в данных или аномалии.

### Этап 3: Проверка гипотез

Гипотеза 1: Органический трафик не отличается от платного с точки зрения CR.

Гипотеза 2: Трафик с мобильных устройств не отличается от десктопных устройств с точки зрения CR.

Гипотеза 3: Трафик из городов присутствия (Москва и область, Санкт-Петербург) не отличается от трафика из других регионов с точки зрения CR.

### Этап 4: Ответы на вопросы продуктовой команды

Какие источники/кампании/устройства/локации генерируют самый целевой трафик?

- Анализировать по метрике CR и объёму трафика.
- Использовать группировки и агрегаты:

Какие авто пользуются наибольшим спросом?

- Выделить топ-10 популярных моделей по количеству запросов и CR.

Стоит ли увеличивать своё присутствие в соцсетях?

- Сравнить CR для трафика из соцсетей и других источников.

## Результаты и выводы

1. Источники трафика

- Наиболее целевой трафик приходит из "Other sources" с CR = 2.92%, что значительно выше, чем у рекламы в социальных сетях (CR = 1.47%).
- Количество сессий из "Other sources" составляет 1,585,815, что в 6 раз превышает трафик из социальных сетей (274,227 сессий).

![image](https://github.com/user-attachments/assets/0d1e01a3-466e-4980-a096-380d221b7d89)

![image](https://github.com/user-attachments/assets/0d32c53c-4ba3-4600-9016-7cbc9b3d6e88)


2. Кампании

- Кампании с самым высоким CR (Conversion Rate) — "JkhCpeDGCtTwhwqWLywv" и "MHdHrBKQwbDaRalwnlJq" с CR = 100%. Однако эти кампании имеют лишь по одной сессии и одной конверсии.
- Кампания "lndNIerCYECRQvBTyTye" демонстрирует стабильные показатели: CR = 27.38%, 23 конверсии, 84 сессии. Она показывает наиболее надёжное сочетание объёма и эффективности.

3. Устройства

- Самое эффективное устройство по CR — desktop (3.13%), за ним следуют mobile (2.60%) и tablet (2.30%).
- Несмотря на это, наибольшее количество трафика идёт с mobile устройств: 1,474,871 сессий и 38,379 конверсий. Это может быть связано с большей доступностью мобильных устройств.

![image](https://github.com/user-attachments/assets/1d09e3bf-bece-46c4-92a9-26b6ab7acf5a)


4. Локации

- Города с максимальным CR — Beaver Falls, Brescia, Gravesend и другие — имеют CR = 100%, но только по одной сессии и одной конверсии.
- Такой результат не является статистически значимым. Важно учитывать локации с большим объёмом данных для более точных выводов.

5. Популярные марки и модели автомобилей

- Топ-10 популярных марок:
 - Лидеры: Skoda (744,516 сессий), Mercedes-Benz (472,316 сессий), Volkswagen (417,128 сессий).

![image](https://github.com/user-attachments/assets/25b36e57-334d-4b8b-9409-5b670e257c31)

Эти бренды занимают лидирующие позиции по популярности среди пользователей.

- Топ-10 популярных моделей:
 - Лидеры: Skoda Rapid (442,513 сессий), Lada Vesta (403,910 сессий), Volkswagen Polo (318,075 сессий).

![image](https://github.com/user-attachments/assets/e49065af-fd04-4f48-977e-526dd4e78287)


6. Социальные сети

- Реклама в социальных сетях показала нулевые результаты:
 - Сессий: 0
 - Конверсий: 0
 - CR: 0%
По сравнению с остальными источниками (CR = 2.71%), социальные сети не приносят целевого трафика.

![image](https://github.com/user-attachments/assets/730a0ca2-af02-4f9c-9f5a-28d066c2441c)


7. Рекомендации:

- Увеличить инвестиции в источники с высоким CR:
- Источник "Other sources" показывает высокую конверсию и большой объём трафика.
- Уделить внимание наиболее успешным кампаниям, например, "lndNIerCYECRQvBTyTye".
- Фокус на устройства:
 - Мобильные устройства обеспечивают основной объём трафика. Рекомендуется адаптировать сайт под мобильные устройства, чтобы улучшить CR.
- Оценить целевые города:
 - Провести дополнительный анализ локаций с высоким CR и большим объёмом данных, чтобы определить ключевые регионы.
- Оптимизировать социальные сети:
 - Учитывая нулевые результаты, нужно пересмотреть стратегию рекламы в соцсетях или отказаться от неё в текущем виде.
- Увеличить акцент на продвижение популярных моделей:
 - Skoda Rapid,
 - Lada Vesta,
 - Volkswagen Polo.
- Анализировать спрос на другие модели из топ-10.

# Сложности

Файлы слишком тяжелые для загрузки в GitHub
