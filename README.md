# ❀ Проект по анализу данных 2024 | Исследование данных о фильмах ❀

**Команда**
* Писчикова Катя
* Стрелец Полина
* Щудро Вика

### Тема и данные

В рамках этого проекта мы выполнили полный цикл анализа данных с использованием данных, в качестве которых выступает спарсенный паблик Вконтакте, посвященный фильмам. Основной целью было получить, обработать и исследовать данные для последующей проверки гипотез и применения методов машинного обучения.

### 1. Сбор данных

> Файл с парсингом: https://drive.google.com/drive/folders/1a4nQloaVLp49sl22Ud_X8bWr6e127oFs?usp=sharing

> Файл с полученными даннными: [project_datacet.csv](https://github.com/KatyaPischikova/academic-butter-knife/blob/main/info/project_dataset.csv)

Первым этапом был парсинг данных из [публичного сообщества ВКонтакте](https://vk.com/obsessed_with_cinema). Мы собрали информацию о постах, включая лайки, репосты, просмотры и комментарии.

### 2. Обработка данных

> Файл с данным шагом: [02_processdata](https://github.com/KatyaPischikova/academic-butter-knife/blob/main/01_processdata.ipynb)

После получения данных мы провели их предварительную обработку:
  * Очистили данные от дубликатов
  * Привели данные к удобному для анализа формату

Мы также обогатили наш спарсенный датасет данными о фильмах - номинантах и победителей Оскара и лауреатов премий Золотая пальмовая ветвь и Золотой глобус.

У нас получились следующие переменные:
  * `post_id` - номер поста
  * `data` - дата публикации поста (не в формате даты, поэтому этот столбец можно убрать)
  * `likes` - количестов лайков
  * `reposts` - количество репостов
  * `views` - количество просмотров
  * `comments` - количество комментариев
  * `attachments` - количество нетекстовых приложений к посту (фотографии)
  * `text` - полный текст поста
  * `movie` - название фильма, который упоминается в посте
  * `director` - имя режиссера
  * `year` - год публикации фильма
  * `additional info` - текст в посте помимо названия фильма, режиссера и года выпуска
  * `oscar_winner` - 0 или 1, где 0 - фильм не выиграл Оскар, 1 - фильм выиграл Оскар
  * `oscar_nominee` - NaN, 0 или 1, где NaN - в посте нет информации о фильме, 0 - фильм не был номинирован на Оскар, 1 - был номинирован
  * `palme_winner` - 0 или 1, где 0 - фильм не выиграл Золотую пальмовую ветвь, 1 - выиграл
  * `globe_winner` - Nan, 0 или 1, где NaN - в посте нет информации о фильме, 0 - фильме не выиграл Золотой глобус, 1 - выиграл 
  * `movie_flg` - 0 или 1, где 0 - пост посвящен не фильму (например, в посте упоминается какой-то актер, набор фотографий или визуальное сравнение нескольких фильмов), 1 - пост посвящен фильму

### 3. Разведочный анализ данных (EDA)

> Файл с данным шагом:  [03_EDA](https://github.com/KatyaPischikova/academic-butter-knife/blob/main/03_EDA.ipynb)

Для того чтобы лучше понять структуру и особенности наших данных, мы провели разведочный анализ данных (EDA):
  * Построили распределения основных переменных (лайки, репосты, просмотры, комментарии)
  * Провели визуализацию данных для выявления скрытых закономерностей и аномалий
  * Очистили данные от выбросов

### 4. Создание новых переменных

> Файл с данным шагом:  [04_newfeatures](https://github.com/KatyaPischikova/academic-butter-knife/blob/main/04_newfeatures.ipynb)

Для дальнейшей проверки гипотез и применения методов машинного обучения мы также создали ряд новых переменных:
  * `ER` - Engagement Rate by Views, соотношение всех целевых активностей аудитории (лайки, репосты, комментарии) к просмотрам
  * `prize` - общее количество присужденных наград фильму
  * `other_award` - присуждение Золотой пальмовой ветви или Золотого глобуса фильму

### 5. Проверка гипотез

> Файл с данным шагом:  [05_hypotheses](https://github.com/KatyaPischikova/academic-butter-knife/blob/main/04_newfeatures.ipynb)

Все гипотезы проверялись на уровне значимости **5%**.

В ходе исследования мы решили выдвинуть следующие гипотезы:

1. Аудитория активнее взаимодействует с более свежими фильмами по сравнению со старыми фильмами
* Проверялась при помощи одностороннего t-теста с правосторонней альтернативой при условии разных дисперсий
* Гипотеза подтвердилась

2. Титулованность фильма не будет влиять на отклик аудитории или будет влиять отрицательно
* Проверялась с помощью наблюдаемого коэффициента корреляции и теста перестановок
* Гипотеза подтвердилась

3. Если фильм выиграл Оскар, то скорее всего у него есть и еще одна награда из двух оставшихся: Золотой глобус или Золотая пальмовая ветвь
* Проверялась с помощью критерия независимости хи-вадрат
* Гипотеза подтвердилась

4. Люди больше взаимодействуют с постами, включающими только картинки, нежели чем с постами, посвященными фильмам
* Проверялась с помощью одностороннего t-теста с правосторонней альтернативой при условии разных дисперсий
* Гипотеза подтвердилась
