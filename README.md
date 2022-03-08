# Исследование объявлений о продаже квартир

## Описание проекта
В распоряжении данные сервиса Яндекс.Недвижимость — архив объявлений о продаже квартир в Санкт-Петербурге и соседних населённых пунктах за несколько лет. Нужно научиться определять рыночную стоимость объектов недвижимости. Моя задача — установить параметры. Это позволит построить автоматизированную систему: она отследит аномалии и мошенническую деятельность.
По каждой квартире на продажу доступны два вида данных. Первые вписаны пользователем, вторые — получены автоматически на основе картографических данных. Например, расстояние до центра, аэропорта, ближайшего парка и водоёма.

## Описание данных

- `airports_nearest` — расстояние до ближайшего аэропорта в метрах (м)
- `balcony` — число балконов
- `ceiling_height` — высота потолков (м)
- `cityCenters_nearest` — расстояние до центра города (м)
- `days_exposition` — сколько дней было размещено объявление (от публикации до снятия)
- `first_day_exposition` — дата публикации
- `floor` — этаж
- `floors_total` — всего этажей в доме
- `is_apartment` — апартаменты (булев тип)
- `kitchen_area` — площадь кухни в квадратных метрах (м²)
- `last_price` — цена на момент снятия с публикации
- `living_area` — жилая площадь в квадратных метрах(м²)
- `locality_name` — название населённого пункта
- `open_plan` — свободная планировка (булев тип)
- `parks_around3000` — число парков в радиусе 3 км
- `parks_nearest` — расстояние до ближайшего парка (м)
- `ponds_around3000` — число водоёмов в радиусе 3 км
- `ponds_nearest` — расстояние до ближайшего водоёма (м)
- `rooms` — число комнат
- `studio` — квартира-студия (булев тип)
- `total_area` — площадь квартиры в квадратных метрах (м²)
- `total_images` — число фотографий квартиры в объявлении

## Общий вывод
1. Были определены и изучены пропущенные значения. В большинстве случае с пропусками оставили пустые значения, т.к. нет данных на которые можно было бы осуществить привязку. Необходимо уточнить информацию у операторов по сбору данных по поводу этих пропусков.
2. Для более эффективного анализа были добавлены данные с ценой квадратного метра, с днем недели, месяцем и годом публикации, с категоризацией этажей, с отношением жилой площади к общей площади и соотвешение площади кухни к общей площади.
3. Средняя площадь квартир в публикуемых объявлениях - `60` м`, средняя стоимость проданных квартир - `6541548.77` руб, а средняя высота потолков в публикуемых объявлениях - `2.77` м.
4. Согласно правилам размещения объявлений на Яндекс.Недвижимость, обявления снимаются автоматически по истечении 30, 60, 90, 120 дней, именно этот фактор и мог повлиять на пиковые значения в данных. Но также выявились значения - `7` и `45` дней, здесь необходимо уточненить информацию у операторов по внесению данных;
5. Все что является меньше среднего значения - `195,8` дней, является быстрой продажей, а все что больше - необычно долгой продажей.
6. Площадь, число комнат, удаленность от центра и на каком этаже расположена квартира (согласоно данным по всем населенным пуктам) оказывают влияние на стоимость. Очевидные - площадь, этаж, удаленность от центра. Неочевидные - число комнат - 3-х комнатные оказались самые дешевые, но для более правильного вывода стоит также учитывать площадь данных комнат.
7. Влияние периодов по дате размещения:
- день недели не оказывает какого-либо характерного и систематического влияния на стоимость;
- впериод с мая по июнь цены очень резко падают и также резко поднимаются - лучшее наиболее выгодным для продажи и наиболее невыгодное время для покупки, является период с июня по сентябрь.;
- экономический кризис 2014 года существуенно повлиял на цены, но после этой отметки стоимость недвижимости только растет.
8. Лидирует по количеству объявлений Санкт-Петербург со средней ценой за квадратный метр - `114849.01`, замыкает топ-10 населенных пуктов по количеству объявлений Выборг со средней ценой за квадратный метр - `58141.91`, максимальная стоимость по всем населенным пуктам в поселке Лисий Нос - `121616.2`, минимальная стоимость по всем населенным пуктам в деревне Старополье - `11206.2`;
9. Анализируя данные Санкт-Петербурга в радиусе в `10` км от цетра города были сделаны сл. выводы:
- больше всего продают квартиры до `100` м²;
- больше всего квартир с ценой до `200000` руб/м²;
- больше всего квартир с числом комнат - `3` шт.;
- больше всего квартир с высотой потолков до `10` м.
10. В отличии от всех населенных пунктов на центр Санкт-Петербурга выделяется зависимость цен от числа комнат - 6-ти комнатные квартиры стоят меньше всего в отличии от всей выборки, где это были 3-х комнтаные квартиры. И в том, и в другом случае стоит учитывать площадь данных комнат. Так, 6-ти комнатная квартира в центра Санкт-Петербурга может оказаться старой комммунальной квартирой с очень малой площадью данных комнат. Зависимсоть этажа не имеет каких-либо отличий от всех населенных пунктов, а удаленность от центра не имеет смысла, т.к. разница в стоимости не существенна. 
11. Влияние периодов по дате размещения в центре Санкт-Петербурга характерно отличаются от всех населенных пунктов только в зависимости от месяца. Наиболее выгодным для продажи и наиболее невыгодным для покупки периодом остается неизменно - это период с июня по сентябрь.
12. Не хватает данных с годом постройки дома/объекта недвижимости. Следует предложить вести регистрацию этих данных.
