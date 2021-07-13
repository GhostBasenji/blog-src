+++
title = "Основы работы с WPF DataGrid. Часть 5. - Столбцы компонента DataGrid"
date = "2019-10-01"
tags = [
    "WPF",
    "XAML",
    "WPF DataGrid"
]
+++

В пятой статье серии «Основы работы с WPF DataGrid» мы будем рассматривать работу со столбцами DataGrid и со свойствами столбцов. 

<!--more-->

### Свойство AutoGenerateColumns
Свойство **AutoGenerateColumns** определяет, будут ли столбцы DataGrid автоматически создаваться во время выполнения на основе объекта источника данных и его свойствах. Каждое общедоступное свойство коллекции источника данных становится столбцом в компоненте DataGrid. Компонент DataGrid достаточно умен, чтобы знать, какой тип столбца следует создать для различных типов данных. Как мы видели на рис. 2, DataGrid создал 4 столбцов для 4 открытых свойств класса Author, и столбец Checkbox был создан для подтверждения жанра “Sci-Fi” книг.

**Примечание.** Значение AutoGenerateColumns равно true по умолчанию для DataGrid.
Код в листинге 22 задает значение true для AutoGenerateColumns.

```xml
<DataGrid x:Name="WPFdataGrid" Margin="10, 10, 0, 0"
          VerticalAlignment="Top" HorizontalAlignment="Left"
          Height="270"
          ColumnWidth="*" Width="770"
          AutoGenerateColumns="True"
          >
```
Листинг 22.

Если источник данных, привязанный к DataGrid, имеет 50 столбцов, а в свойстве AutoGenerateColumns значение установлено в “true”, то он сгенерирует и покажет все 50 столбцов. Если хотим показать меньше столбцов или определенных столбцов, то задаем значение “false” свойству AutoGenerateColumns и создаем столбцы вручную.

### Свойство ColumnWidth
Компонент DataGrid достаточно умен, чтобы регулировать и управлять шириной столбцов. Свойство ColumnWidth предоставляет параметры ширины столбцов DataGrid.  ColumnWidth – структура DataGridLength, которая имеет следующие ключевые значения, применяемые к столбцам:

+ Auto. Режим автоматического определения размера.
+ DesiredValue. Рассчитанное значение пикселя, необходимое для столбцов.
+ DisplayValue. Значение пикселя, необходимое для столбцов.
+ SizeToCells. Ширина столбца зависит от содержимого ячейки таблицы.
+ SizeToHeader. Ширина зависит от заголовка столбца.
Value. Ширина в пикселях.

Давайте рассмотрим некоторые значения на примере.

![Рис. 13. ColumnWidth=”SizeToHeader”](https://i.postimg.cc/65c5CjJM/gb0018.jpg)

![Рис. 14. ColumnWidth=”SizeToCells”](https://i.postimg.cc/bwvYgxqp/gb0019.jpg)

![Рис. 15. ColumnWidth=”100”.](https://i.postimg.cc/jjwx0RW1/gb0020.jpg)

![Рис. 16. ColumnWidth=”*”](https://i.postimg.cc/P5FXRCqZ/gb0021.jpg)

### Свойства CanUserResizeColumns и CanUserResizeRows
По умолчанию DataGrid разрешает пользователям изменять размеры столбцов и строк. Но мы можем ограничить пользователей в возможности изменять размеры столбцов и строк в DataGrid.
Свойство **CanUserResizeColumns** используется для того, чтобы указать, могут ли пользователи изменять размеры столбца. А свойство **CanUserResizeRows** – разрешать или нет изменять размеры строк.
Нижеприведенный код в листинге 23 ограничивает пользователей в возможности изменять размеры строк и столбцов в компонента DataGrid.

```xml
<DataGrid x:Name="WPFdataGrid" Margin="10, 10, 0, 0" 
        HorizontalAlignment="Left" VerticalAlignment="Top"
        Height="270" Width="770"
        AutoGenerateColumns="True"
        AlternatingRowBackground="LightGreen"
        ColumnWidth="*"
        SelectionUnit="Cell" SelectionMode="Extended"
        CanUserResizeColumns="False"
        CanUserResizeRows="False"
        >
```
Листинг 23.

### Свойства CanUserSortColumns и CanUserReorderColumns
По умолчанию DataGrid разрешает пользователям сортировать и переупорядочивать столбцы. Но мы можем запретить пользователям делать это.
Свойство **CanUserSortColumns** используется для того, чтобы указать, могут ли пользователи сортировать столбцы. А свойство **CanUserReorderColumns** – разрешать или нет переупорядочивать столбцы.
Нижеприведенный код в листинге 24 ограничивает пользователей в возможности сортировать и переупорядочивать столбцы DataGrid.

```xml
<DataGrid x:Name="WPFdataGrid" Margin="10, 10, 0, 0" 
          HorizontalAlignment="Left" VerticalAlignment="Top"
          Height="270" Width="770"
          AutoGenerateColumns="True"
          AlternatingRowBackground="LightGreen"
          ColumnWidth="*"
          SelectionUnit="Cell" SelectionMode="Extended"
          CanUserSortColumns="False" 
          CanUserReorderColumns="False"
          >
```
Листинг 24.

Большинство свойств, описанных выше, можно задавать динамически в исходном коде. Листинг 25 задает значение “False” этим свойствам во время выполнения.

```cs
    WPFdataGrid.CanUserResizeColumns = false;
    WPFdataGrid.CanUserSortColumns = false;
    WPFdataGrid.CanUserReorderColumns = false;
```
Листинг 25