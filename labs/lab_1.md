# Технологии искусственного интеллекта. Семестр 1

© Петров М.В., старший преподаватель кафедры суперкомпьютеров и общей информатики, Самарский университет

## Лабораторная работа №1: Pandas

[Лекция](../lectures/lecture_1/lecture_1.ipynb)

1. Считать в `pandas.DataFrame` любой источник данных: CSV, JSON, Excel-файл, HTML-таблицу и т.п.
Также можно сконвертировать в DataFrame любой из встроенных датасетов `sklearn`: (см. [инструкцию](https://stackoverflow.com/questions/38105539/how-to-convert-a-scikit-learn-dataset-to-a-pandas-dataset)).  
   > Главное условие к датасету, который вы загружаете - там должны быть числовые колонки (численные признаки).

2. Привести описание датасета.  

   Пример.  
   Датасет содержит данные о метеонаблюдениях в Австралии, цель - прогнозирование дождя на следующий день.  
   | Признак | Описание | Единицы измерения |  
   | --- | --- | --- |  
   | Location | The common name of the location of the weather station |  
   | MinTemp | Minimum temperature in the 24 hours to 9am. Sometimes only known to the nearest whole degree. | degrees Celsius  
   | Sunshine | Bright sunshine in the 24 hours to midnight | hours

3. Выполнить над датафреймом следующие операции:  
   - `.head()`.
   - `.describe()`.
   - Считывание значения конкретной ячейки (с конкретным индексом из конкретной колонки).
   - Фильтрация строк по диапазону индекса.
   - Фильтрация набора данных по какому-либо условию.
   - Работа с пропущенными значениями:
      + удаление строк с пропущенными значениями;
      + заполнение пропущенных значений средним значением по колонке.  
     > Если пропущенных значений нет - намеренно их сгенерировать, прибить какие-то куски данных в `np.nan`.
   - Создание нового поля, вычисленного на основе значений других полей:
      + через выражение на базе имеющихся колонок;
      + через `DataFrame.apply`;
      + через `Series.apply`.
   - Сортировка по какому-либо из полей.
   - Вычисление нескольких статистик по колонкам (использовать встроенные агрегатные функции - любые на выбор).
   - Вывод по какому-либо полю / набору полей числа значений с использованием `.value_counts()`.
   - Вывод уникальных значений какой-либо колонки с использованием `.unique()`.
   - Удаление текущего индекса, и создание нового индекса на базе новой колонки, которая для этого лучше всего подходит - см. 
[reset_index](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.reset_index.html) и 
[set_index](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.set_index.html).

4. Продемонстрировать работу `.groupby`, на основе группировок в `groupby` вычислить агрегатные функции по одной или нескольким колонкам.

5. Решейпинг данных $1D\rightarrow2D$ с использованием `.pivot` (можно подать на вход результаты агрегатов, полученных ранее с использованием `.groupby` (сгруппировать по двум полям). 

6. Решейпинг $1D\rightarrow2D$ данных, соединённых с группировкой / агрегацией (одним словом - сводная таблица): `.pivot_table`. Группировать только по категориальным полям или числовым, если значений немного.
   > Если значений много, то необходимо их загрубить. Например, вычислить гистограмму как в задании (8).

7. Вычислить квантили распределения какого-либо вещественного признака (с использованием `numpy.quantile` или `numpy.percentile`).  

8. Вычислить (в виде текста) гистограмму какого-либо вещественного признака (с использованием `numpy.histogram`). Значения гистограммы можно использовать в качестве загрубленного числового признака для заданий (5) или (6).  

9. Проитерировать `DataFrame` построчно `.iterrows()` и выполнить какую-либо операцию внутри цикла.  

10. Получить `DataFrame` с `MultiIndex` любым способом: через конструктор (в документации есть множество видов конструкторов для создания `MultiIndex` с нуля), через `read_sql` / `read_csv` / `read_excel`, `read_*`, через `pivot_table`, через `groupby` или иными способами.  
    - Переставить местами уровни индекса.
    - Транспонировать таблицу (или создать новую другую) с `MultiIndex`.
    - Удалить один из уровней индекса или добавить новый уровень индекса (можно инициализированный константой) - см. документацию.

11. Продемонстировать работу `.merge`.

12. Продемонстрировать работу с `.concat` или `append`.

### Замечания

> Некоторые используют `.pivot` и `.pivot_table` неправильно или в неподходящем контексте, в результате получается бессмыслица.
> - `.pivot` нужен для того, чтобы результаты двухуровневой группировки представить в виде двумерной таблицы, где один из уровней группировки уходит в строчки, другой в столбцы.
> - `.pivot_table` нужен для того же, только умеет сам группировать / агрегировать данные, а не просто растаскивать ячейки по двумерной таблице.

> Для заданий (10) - (12) можно сгенерировать датасет из случайных данных.