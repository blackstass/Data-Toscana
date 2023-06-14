# Data-Toscana
Добро пожаловать на страницу нашего проекта!!!

В результате бесчисленных споров нашей командой было принято решение проанализировать данные о вине с прекрасного сайта SimpleWine.ru. В рамках этого проекта мы произвели парсинг данных, провели глубокий анализ и визуализацию, проверили интересующие нас гипотезы, а также построили модель машинного обучения, которая предсказывает справедливую рыночную стоимость бутылки вина по её характеристикам.

__Проект включает несколько ключевых этапов:__
* Сбор данных (парсинг).
* Анализ данных и визуализация.
* Проверка гипотез.
* Построение модели предсказания.

__Цель проекта__

Целью этого проекта является предоставление инструмента, который поможет людям, в частности виноделам, дистрибьюторам, а также любителям вина, получить более глубокое понимание того, как формируется цена вина и что она может быть на рынке исходя из его характеристик.

Мы надеемся, что этот проект принесет вам пользу и будет интересен!

## Часть 1. Парсинг
Первым этапом мы приступили к сбору информации со страниц каталога. Как только основные сведения были получены, мы начали собирать 
дополнительную информацию по каждой бутылке отдельно, переходя по ссылкам, полученным в начале. 

[Наш скрипт для парсинга](Алкопарсинг.ipynb) разработан так, чтобы автоматически пройти через каталог вина на сайте и собрать следующую информацию для каждого представленного вина:

 Признак | Описание | Признак | Описание | Признак | Описание | Признак | Описание |
|:---------------:|:---------------:|:---------------:|:---------------:|:---------------:|:----------:|:----------:|:----------:|
| name | полное название вина | color | цвет вина | region | региона производства вина | taste | вкус вина |
| w_id | ID конретного вина на сайте SimpleWine | sweetness | вкус вина | year | год производства | dishes | к каким блюдам подается вино |
| href | ссылка на вино на сайте | volume | объём бутылки | strength | крепкость вина (содержание алкоголя) | sugar | содержание сахара (по 5-бальной шкале) |
| base_price | начальная цена бутылки вина (руб) | SW_rating, VIVINO_rating | клиентский рейтинг вин | storage_potential | срок годности | acidity | кислотность (по 5-бальной шкале) |
| discount_size | предоставляемая скидка (%) | WS, RVF, JS_rating, RP, AM, GR, AIS, PENIN, ST, JR rating | рейтинги различных критиков | appelltion | гос стандарт для выращивания вина | aromaticity | ароматические свойства вина (по 5-бальной шкале) |
| discount_price | скидочная цена бутылки вина | grape | сорт винограда | category | категория вина | tannins | таннины (по 5-бальной шкале) |
| simple_collection | состоит ли бутылка вина в коллекции магазина SimpleWine | manufacturerz | производитель вина | decantation | рекомендуется ли декантация вина | body | тело вина (по 5-бальной шкале) |
| country | страна производства | features | дополнительные характеристиики вина | aging_in_container | где вино настаивалось | description | описание вина на сайте |

Полученные данные сохраняются в формате [CSV](Алкопарсингновый.csv) для дальнейшего анализа и обработки.

## Часть 2. Анализ и визуализация
После того как мы успешно собрали датасет, было время погрузиться в [анализ данных](). Этот этап оказался испытанием, в котором мы столкнулись с некоторыми сложностями.
Прежде всего, мы занялись очисткой данных от дубликатов, при этом уделив особое внимание удалению неинформативных признаков. Внимательно просмотрев данные, мы обнаружили и заполнили пробелы, исключив при этом те экземпляры вин, которые были неадекватно представлены из-за большого количества пропусков в их описаниях - к счастью, таких случаев оказалось не много.
Также, мы реализовали стратегию объединения всех клиентских оценок и рейтингов критиков в два обособленных рейтинга. Наконец, мы разделили списочные признаки на отдельные строки, чтобы облегчить дальнейший анализ.
В итоге, этап подготовки данных стал основой для следующих шагов в нашем исследовании. [CSV после обработки]()

С помощью инструмента Plotly мы создали интерактивную географическую визуализацию - [карту мира вин](). Эта карта подчеркивает разнообразие винной индустрии, предоставляя ценную информацию о каждой стране.
На карте мы отобразили ценовой диапазон вин для каждой страны, показывая стоимость самого доступного и самого дорогого вина, а также среднюю стоимость вин этой страны.
Для каждой страны мы выявили наиболее популярные вина по цвету, что дает представление о характерных предпочтениях в разных регионах. Мы определили самый распространенный сорт винограда и самого популярного производителя вина, отражая специфику и особенности виноделия каждой страны.
Таким образом, наша карта мира вин представляет собой источник уникальных и детализрованных знаний о винной индустрии мира.

## Часть 3. Проверка гипотез
На [данном этапе]() нашей задачей было сформулировать и подвергнуть проверке статистические гипотезы, что помогло нам проникнуть глубже в механизмы формирования цен на вина.

__Ниже представлен перечень гипотез, которые мы разработали и исследовали:__
* В среднем, красное вино обладает более высокой стоимостью, по сравнению с белым
* Белое вино, в свою очередь, в среднем обходится дороже, нежели розовое
* Рейтинг клиентов и оценки критиков не влияют друг на друга
* Критики выставляют более строгие оценки винам, в сравнении с обычными потребителями
* Сухое вино стоит дороже, чем полусухое в среднем
* Сладкое вино в среднем обходится дороже, чем полусладкое
* Сладость вина и рейтинг покупателей не коррелируют между собой

Для каждой из этих гипотез, мы тщательно выбирали наиболее подходящий критерий для проверки, учитывая предпосылки его применения. Кроме того, мы визуализировали признаки и гипотезы, чтобы более наглядно представить и анализировать обнаруженные тенденции.

## Часть 4. Построение модели
После подробного анализа и обработки собранных данных, мы перешли к следующему важному этапу нашего проекта - [созданию и обучению модели машинного обучения](). Цель этой модели - предсказывать ожидаемую рыночную стоимость бутылки вина, исходя из ее характеристик.

Подготовка данных для обучения модели требовала некоторой дополнительной работы. Особенно это касалось категориальных признаков, которые нужно было закодировать, чтобы модель могла эффективно их обрабатывать. Для этого мы использовали технику "one-hot" кодирования.

Однако мы столкнулись с трудностью при обработке признаков, представленных в виде списков. Эти признаки требовали индивидуального подхода и были закодированы вручную.

После подготовки данных, мы перешли к настройке и обучению модели. Для создания оптимальной модели, мы провели тщательный подбор гиперпараметров для алгоритмов случайного леса (Random Forest) и градиентного бустинга.

Таким образом, на основе собранных и тщательно обработанных данных, мы смогли создать и обучить модель машинного обучения, способную предсказывать ожидаемую рыночную стоимость бутылки вина, исходя из ее характеристик, что является значимым достижением в рамках нашего проекта.
