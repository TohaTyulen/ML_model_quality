Описание проекта: Обучение с учителем: качество модели
Интернет-магазин «В один клик» продаёт разные товары: для детей, для дома, мелкую бытовую технику, косметику и даже продукты. Отчёт магазина за прошлый период показал, что активность покупателей начала снижаться. Привлекать новых клиентов уже не так эффективно: о магазине и так знает большая часть целевой аудитории. Возможный выход — удерживать активность постоянных клиентов. Сделать это можно с помощью персонализированных предложений.

«В один клик» — современная компания, поэтому её руководство не хочет принимать решения просто так — только на основе анализа данных и бизнес-моделирования. У компании есть небольшой отдел цифровых технологий, и вам предстоит побыть в роли стажёра в этом отделе.


Нужно промаркировать уровень финансовой активности постоянных покупателей. В компании принято выделять два уровня активности: «снизилась», если клиент стал покупать меньше товаров, и «прежний уровень».
Нужно собрать данные по клиентам по следующим группам: Признаки, которые описывают коммуникацию сотрудников компании с клиентом. Признаки, которые описывают продуктовое поведение покупателя. Например, какие товары покупает и как часто. Признаки, которые описывают покупательское поведение клиента. Например, сколько тратил в магазине. Признаки, которые описывают поведение покупателя на сайте. Например, как много страниц просматривает и сколько времени проводит на сайте.

Представим группы признаков (вместе с целевым) в виде диаграммы — такую визуализацию ещё называют диаграммой Исикавы.

Нужно построить модель, которая предскажет вероятность снижения покупательской активности клиента в следующие три месяца.
В исследование нужно включить дополнительные данные финансового департамента о прибыльности клиента: какой доход каждый покупатель приносил компании за последние три месяца.
Используя данные модели и данные о прибыльности клиентов, нужно выделить сегменты покупателей и разработать для них персонализированные предложения.
Руководство одобрило описание решения, и вам, как специалисту по DS, нужно его реализовать.
Описание данных
Данные для работы находятся в нескольких таблицах. 
market_file.csv
Таблица, которая содержит данные о поведении покупателя на сайте, о коммуникациях с покупателем и его продуктовом поведении.
id — номер покупателя в корпоративной базе данных.
Покупательская активность — рассчитанный класс покупательской активности (целевой признак): «снизилась» или «прежний уровень».
Тип сервиса — уровень сервиса, например «премиум» и «стандарт».
Разрешить сообщать — информация о том, можно ли присылать покупателю дополнительные предложения о товаре. Согласие на это даёт покупатель.
Маркет_актив_6_мес — среднемесячное значение маркетинговых коммуникаций компании, которое приходилось на покупателя за последние 6 месяцев. Это значение показывает, какое число рассылок, звонков, показов рекламы и прочего приходилось на клиента.
Маркет_актив_тек_мес — количество маркетинговых коммуникаций в текущем месяце.
Длительность — значение, которое показывает, сколько дней прошло с момента регистрации покупателя на сайте.
Акционные_покупки — среднемесячная доля покупок по акции от общего числа покупок за последние 6 месяцев.
Популярная_категория — самая популярная категория товаров у покупателя за последние 6 месяцев.
Средний_просмотр_категорий_за_визит — показывает, сколько в среднем категорий покупатель просмотрел за визит в течение последнего месяца.
Неоплаченные_продукты_штук_квартал — общее число неоплаченных товаров в корзине за последние 3 месяца.
Ошибка_сервиса — число сбоев, которые коснулись покупателя во время посещения сайта.
Страниц_за_визит — среднее количество страниц, которые просмотрел покупатель за один визит на сайт за последние 3 месяца. market_money.csv
Таблица с данными о выручке, которую получает магазин с покупателя, то есть сколько покупатель всего потратил за период взаимодействия с сайтом.
id — номер покупателя в корпоративной базе данных.
Период — название периода, во время которого зафиксирована выручка. Например, 'текущий_месяц' или 'предыдущий_месяц'.
Выручка — сумма выручки за период.
market_time.csv
Таблица с данными о времени (в минутах), которое покупатель провёл на сайте в течение периода.
id — номер покупателя в корпоративной базе данных.
Период — название периода, во время которого зафиксировано общее время.
минут — значение времени, проведённого на сайте, в минутах.
money.csv
Таблица с данными о среднемесячной прибыли покупателя за последние 3 месяца: какую прибыль получает магазин от продаж каждому покупателю.
id — номер покупателя в корпоративной базе данных.
Прибыль — значение прибыли.
Задачей данных исследований стояло проработать решение, которое позволит персонализировать предложения постоянным клиентам, чтобы увеличить их покупательскую активность.
Данные были практически чистыми с полным обьемом за исключением 4 строк, удаление которых не повлияло на качество данного решения. Предобработка потребовалась в минимальном обьеме, данные были обьеденены в один общий датасет с помощью сводных таблиц.
В результате исследовательского анализа было обнаружено влияние нескольких признаков на покупательскую активность - покупательская активность зависит от 6 месячной маркетинговой активности, Зависимость есть между акционными покупками и покупательской активностью, с ростом доли акционных покупок, покупательская активность снижается, Чем выше среднее количество просмотров категорий за визит, тем выше покупательская активность, видна обратная зависимость - Чем больше неоплаченных продуктов в корзине, тем ниже покупательская активность клиентов. Видна зависимость, чем больше страниц за визит, тем выше покупательская активность.Есть зависимость, Чем больше времени, проведенного на сайте в предыдущем месяце, и/или текущем месяце тем выше покупательская активность. Видна зависимость - чем выше выручка за предпредыдущий месяц , тем выше покупательская активность.
По матрице корреляции видна явная зависимость покупательской активности от количества просмотренных страниц за визит, от количества проведенных минут в текущем и предыдущем месяце на сайте, от выручки в предпредыдущий месяц, от акционных покупок, от 6 месячной маркетинговой активности, от среднего просмотра категорий за визит, от неоплаченных продуктов в корзине. Также наблюдаем сильную зависимость выручки между собой в текущем и предыдущем месяце, что может вызвать мультиколлениарность при построении модели. В связи с низкой корреляцией между покупательской активностью и типом сервиса - 0.13, между покупательской активностью и разрешением сообщать - 0, между покупательской активностью и Маркет_актив_тек_мес - 0, между покупательской активностью и длительностью - 0.1, между покупательской активностью и ошибкой сервиса 0.22, между покупательской активностью и предыдущий месяц выручка - 0.22, между покупательской активностью и текущий месяц выручка - 0.2, между покупательской активностью и прибылью - 0, данные столбцы не будут учитываться при построении модели.
Для мелкой бытовой техники и электроники, кухонной посуды, косметики и аксессуаров, домашнего текстиля видим явную линейную зависимость выручки за текущий и за предыдущий месяц. Для товаров для детей и техники для красоты и здоровья видна некоторая нелинейность зависимости выручки за текущий и за предыдущий месяц.
Выбрали основную метрику ROC AUC, так как она лучше подходит для несбалансированных данных ( количество 'Осталось прежним' выше чем 'Снизилось'), но также наблюдали за остальными метриками при тестировании модели. Использовали полиномизацию 2-й степени в пайплайне.
Выбрали модель LogisticRegression(). Получили ROC AUC на кросс-валидационной выборке 0.9. Обрезали мешающие признаки, метрика ROC AUC на тестовой выборке составила 0.923, f1 = 0.905, accuracy = 0.87
По анализу признаков основные негативные факторы, которые влияют на покупательскую активность, это Акционные покупки и неоплаченные покупки штук, квартал и их производные. Можно повлиять на данный признак через уменьшение акционных покупок. Из предыдущего анализа данных было видно, что покупательская активность снижается при выше чем 30% акционных покупок. Положтельные факторы, которые влияют на покупательскую активность - это 1. количество минут в предыдущий месяц потраченных на покупку, 2. количество минут в текущий месяц потраченных на покупк 3. Страниц за визит, 4. Средний просмотр категорий за визит, 5. Маркетинговая активность за 6 месяцев и их производные.
Выбраны следующие критерии, пороги, KPI - акционные покупки > 30%, предыдущий_месяц_минут < 14, текущий_месяц_минут < 14, Страниц_за_визит < 8, Средний_просмотр_категорий_за_визит < 3, Маркет_актив_6_мес < 4.1, как видно из распределения прибыли, данные критерии, пороги, KPI не влияют на прибыль и могут использоваться для увеличения покупательской активности. Требуется корректировать поведение покупателей в расчете данных KPI, для увеличения покупательской активности. При тестовой корректировки удалось улучшить покупательскую активность со значения 38% "снизилась", 62% "осталась прежней", до 100% "осталась прежней".
