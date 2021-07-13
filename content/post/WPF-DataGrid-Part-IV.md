+++
title = "Основы работы с WPF DataGrid. Часть 4. - Строки компонента DataGrid"
date = "2019-09-15"
tags = [
    "WPF",
    "XAML",
    "WPF DataGrid"
]
+++

В четвертой статье описывается работа с заголовком и видимостью строк, а также рассматриваются внешний вид и некоторые другие свойства. 

<!--more-->

### Свойство RowHeaderWidth
DataGrid – это набор строк и столбцов, каждая строка и каждый столбец могут иметь заголовок. Этот заголовок можно использовать для отображения текста, например, заголовков строк и столбцов.
Свойство **RowHeaderWidth** используется для задания ширины заголовка строк.

Код в листинге 15 задает значение 50 в свойстве RowHeaderWidth.
```xml
<DataGrid x:Name="WPFdataGrid" Margin="0"
        AutoGenerateColumns="True"
        SelectionUnit="Cell"
        RowHeaderWidth="50"
        >
</DataGrid>
```
Листинг 15.

Ниже видим результат написания одной строки:

![Рис. 8](https://i.postimg.cc/pTY5rYyZ/gb0008.jpg)

### Свойство GridLinesVisibility
Мы можем показать или скрыть линии таблицы DataGrid, используя свойство **GridLinesVisibility**. Данное свойство имеет 4 значения: All, Horizontal, None и Vertical. Если хотим отобразить и горизонтальные, и вертикальные линии, задаем значение All свойству GridLinesVisibility. Значение None скрывает горизонтальные и вертикальные линии, а значения Horizontal и Vertical отображают только горизонтальные и вертикальные линии соответственно.

![Рис. 9. Листинг 16](https://i.postimg.cc/Y0rGWGWw/gb0009.jpg)

Код в листинге 17 скрывает линии столбцов компонента DataGrid.
```xml
<DataGrid x:Name="WPFdataGrid" Margin="0"
          AutoGenerateColumns="True"
          SelectionUnit="Cell"
          RowHeaderWidth="50"
          AlternatingRowBackground="LightGreen"
          GridLinesVisibility="Horizontal">
</DataGrid>
```
Листинг 17.

Результат данного кода:

![Рис. 10](https://i.postimg.cc/qRdCpZBq/gb0010.jpg)

### Свойство AlternatingRowBackground
Свойство **AlternatingRowBackground** используется для задания и получения цвета фона каждой альтернативной строки в DataGrid.
Код в листинге 18 задает значение цвета LightGreen свойству AlternatingRowBackground.
```xml
<DataGrid x:Name="WPFdataGrid" Margin="0"
          AutoGenerateColumns="True"
          SelectionUnit="Cell"
          RowHeaderWidth="50"
          AlternatingRowBackground="LightGreen"
          GridLinesVisibility="Horizontal">
</DataGrid>
```
Листинг 18.


![Рис. 11](https://i.postimg.cc/pL4F6LgD/gb0011.jpg)

### Свойства SelectionMode и SelectionUnit
Свойства **SelectionMode** и **SelectionUnit** используются для определения поведения выделения для компонента DataGrid. Свойство SelectionMode указывает, как выделяются строки и ячейки в DataGrid. У SelectionMode есть 2 значения:
* **Extended**. Несколько элементов могут быть выделены одновременно.
* **Single**. Только один элемент может быть выделен за один раз.

Свойство SelectionUnit указывает, могут ли выделены строки, ячейки или оба в DataGrid. Это свойство имеет три значения:
* **Cell**. Выделяются только ячейки. Щелчок по заголовку строки или столбца ничего не производит.
* **CellOrRowHeader**. Ячейки или строки выделяются. При нажатии на ячейку выделяется только ячейка. При нажатии на заголовок строки выделяется строка полностью.
* **FullRow**. Щелчок по ячейку или заголовок строки выделяет всю строку.

Код в листинге 19 задает значения Cell и Extended свойствам SelectionUnit и SelectionMode соответственно.
```xml
<DataGrid x:Name="WPFdataGrid" Margin="0"
          AutoGenerateColumns="True"
          RowHeaderWidth="50"
          AlternatingRowBackground="LightGreen"
          GridLinesVisibility="All"
          ColumnWidth="*"
          SelectionUnit="Cell"
          SelectionMode="Extended">
</DataGrid>
```
Листинг 19.

Ниже видим результат нашего кода. Если нажать на несколько ячеек, удерживая клавишу Ctrl, то увидим, что будет выделено несколько ячеек.

![Рис. 12](https://i.postimg.cc/PqDwskj0/gb0012.jpg)

### Свойства CanUserResizeRow и CanUserResizeColumns
По умолчанию DataGrid разрешает пользователям изменять размеры столбцов и строк. Но мы можем ограничить пользователей в возможностях изменять размеры строк и столбцов в DataGrid.
Свойство **CanUserResizeRows** используется для указания того, могут ли пользователи изменять размер строки. Свойство **CanUserResizeColumns** – могут ли пользователи изменять размер столбцов.

Код в листинге 20 ограничивает пользователей в возможностях изменять размеры строк и столбцов в DataGrid.
```xml
<DataGrid x:Name="WPFdataGrid" Margin="0" 
          AutoGenerateColumns="True"
          RowHeaderWidth="50"
          AlternatingRowBackground="LightGreen"
          GridLinesVisibility="All"
          ColumnWidth="*"
          SelectionUnit="Cell"
          SelectionMode="Extended"
          CanUserResizeColumns="False"
          CanUserResizeRows="False">
</DataGrid>
```
Листинг 20.

### Свойство RowStyle
Свойство **RowStyle** используется для стилизации всех строк DataGrid. 
Код в листинге 21 создает стиль и задает свойство DataGrid.RowStyle.
```xml
<DataGrid x:Name="WPFdataGrid" Margin="0, 0, 0, 0" 
          VerticalAlignment="Top" HorizontalAlignment="Stretch"
          HorizontalContentAlignment="Stretch"
          Height="270"
          AutoGenerateColumns="True"
          ColumnWidth="*"
          >
  <DataGrid.RowStyle>
      <Style TargetType="DataGridRow">
        <Setter Property="Background" Value="LightGreen" />
          <Style.Triggers>
            <Trigger Property="IsMouseOver" Value="True">
            <Setter Property="Background" Value="Green"/>
            <Setter Property="Foreground" Value="White"/>
          </Trigger>
        </Style.Triggers>
      </Style>
  </DataGrid.RowStyle>
</DataGrid>
```
Листинг 21.