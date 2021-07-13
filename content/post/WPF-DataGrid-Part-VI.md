+++
title = "Основы работы с WPF DataGrid. Часть 5.2. - Столбцы компонента DataGrid"
date = "2019-10-05"
tags = [
    "WPF",
    "XAML",
    "WPF DataGrid"
]
+++

В данной статье серии “Основы работы с WPF DataGrid” рассматриваются некоторые расширенные функции столбцов DataGrid.

<!--more-->

### Столбцы DataGrid
В других статьях серии “Основы работы с WPF DataGrid” мы замечали, что когда свойство **AutoGenerateColumns** имеет значение “true”, DataGrid создает столбцы на основе источника данных, его объектах и общих свойств. Однако в большинстве приложений мы определяем столбцы, их типы и привязываем к свойствам источника данных.

### Свойство DataGrid.Columns

Свойство Columns представляет все столбцы компонента DataGrid. Свойство Columns представляет собой коллекцию и предоставляет методы добавления, обновления и удаления столбцов из коллекции.
Чтобы иметь возможность создавать столбцы вручную, для этого свойству AutoGenerateColumns нужно присвоить значение “false”.

```xml
    <DataGrid x:Name="WPFdataGrid" Margin="10, 10, 0, 0" 
              VerticalAlignment="Top" HorizontalAlignment="Left"
              AutoGenerateColumns="False"
              >
```
Листинг 26

DataGrid имеет 4 типа столбцов:
+ **DataGridHyperlinkColumn.** Используется для отображения гиперссылки в столбце.
+ **DataGridComboBoxColumn.** Используется для отображения выпадающего списка с одним выделенным элементом.
+ **DataGridTextColumn.** Используется для отображения текста.
+ **DataGridCheckBoxColumn.** Используется для отображения булева значения с помощью CheckBox.

Код в листинге 27 создает DataGrid с пятью столбцами. Первый столбец является DataGridHyperlinkColumn. Следующие два столбца – DataGridTextColumn, а последний столбец – DataGridCheckBoxColumn.

```xml
<DataGrid x:Name="WPFdataGrid" Margin="10, 10, 0, 0" 
        HorizontalAlignment="Left" VerticalAlignment="Top"
        Height="270" Width="770"
        AutoGenerateColumns="False"
        AlternatingRowBackground="LightGreen"
        ColumnWidth="*"
        SelectionUnit="Cell" SelectionMode="Extended"
        CanUserResizeColumns="False" CanUserResizeRows="False"
        >
          <DataGrid.Columns>
              <DataGridHyperlinkColumn Binding="{Binding ID}" Header="ID Автора" Width="100"/>
              <DataGridTextColumn Binding="{Binding Name}" Header="Имя автора" IsReadOnly="True" Width="120"/>
              <DataGridTextColumn Binding="{Binding BookTitle}" Header="Произведение" IsReadOnly="True" Width="170"/>
              <DataGridCheckBoxColumn Binding="{Binding SciFi}" Header="Sci-Fi" IsReadOnly="True" Width="50"/>
          </DataGrid.Columns>
```
Листинг 27

![Рис. 17.](https://i.postimg.cc/CK4sq5kB/gb0022.jpg)

### Свойства столбца DataGrid
Каждый столбец DataGrid имеет свои собственные свойства и может управляться иначе, чем другие столбцы. Ниже перечислены общие свойства столбцов DataGrid:
+ **Binding.** Привязка связывает столбец со свойством в источнике данных.
+ **CanUserReorder.** Определяет, может ли пользователь изменять положение отображаемого столбца, перетаскивая заголовок столбца.
+ **CanUserResize.** Определяет, может ли пользователь изменять ширину столбца с помощью мыши.
+ **CanUserSort**. Определяет, может ли пользователь сортировать столбец, щелкая по заголовку столбца.
+ **FontFamily**. Семейство шрифтов для содержимого ячеек в столбце.
+ **FontSize**. Размер шрифта для содержимого ячеек в столбце.
+ **FontStyle**. Стиль шрифта для содержимого ячеек в столбце.
+ **FontWeight**. Вес шрифта для содержимого ячеек в столбце.
+ **Foreground**. Кисть, которая используется для раскраски текстового содержимого ячеек в столбце.
+ **Header**. Содержимое заголовка столбца.
+ **IsAutoGenerate**. Определяется, может ли автоматически создаваться столбец.
+ **IsFrozen**. Определяет, не допускается ли прокрутка по горизонтали столбца.
+ **IsReadOnly**. Проверяет, можно ли редактировать или нет ячейки в столбце.
+ **SortDirection**. Сортировать по направлению (по возрастанию или убыванию) столбца.
+ **Visibility**. Показывать или скрывать столбец.
+ **Width**. Ширина столбца или режим автоматического определения размера.

Код в листинге 28 создает столбец и задает ему различные свойства.
```xml
<DataGridTextColumn 
        Binding="{Binding Name}" Header="Имя автора" IsReadOnly="True" Width="120"
        CanUserReorder="False" CanUserResize="False" CanUserSort="False"
        FontFamily="Georgia" FontSize="14" FontStyle="Normal" FontWeight="Bold"
        SortDirection="Ascending" Foreground="Blue" Visibility="Collapsed"/>
```
Листинг 28

## Свойство Binding
Свойство Binding привязывает свойство объекта к столбцу. В листинге 29 код связывает DataGridTextColumn со свойством Name объектов источника данных.
```xml
<DataGridTextColumn Binding="{Binding Name}" Header="Имя автора" Width="120"/>
```
Листинг 29

## Динамические столбцы DataGrid
Как уже ранее говорилось, DataGrid.Columns представляет собой коллекцию столбцов в DataGrid. DataGrid.Columns наследует от ObservaleCollection<T> и предоставляет все функции, связанные с коллекциями, такие как добавление, удаление и поиск элементов в коллекции.
Метод Add используется для добавления динамического столбца в коллекцию. Код, показанный в листинге 30, создает столбец DataGridTextColumn, задает его свойства Binding и Header, а также добавляет столбец в ряды столбцов DataGrid.
```cs
DataGridTextColumn col = new DataGridTextColumn();
col.Binding = new Binding("Name");
col.Header = "Имя автора";
WPFdataGrid.Columns.Add(col);
```
Листинг 30.

Методы **Remove** и **RemoveAt** используются для удаления столбцов из коллекции столбцов DataGrid.
```cs
DataGridTextColumn col = new DataGridTextColumn();
col.Binding = new Binding("Name");
col.Header = "Имя автора";
WPFdataGrid.Columns.RemoveAt(col);
```
Листинг 31.

## Замороженные столбцы [Frozen Columns]
Замороженные столбцы – это столбцы, которые всегда видимы и не могут быть прокручены вне видимости. Замороженные столбцы всегда являются самыми левыми столбцами в порядке отображения. Например, у нас есть DataGrid, который имеет слишком много столбцов, что не помещаются в коне DataGrid, и этому компоненту нужно горизонтальная прокрутка. А мы хотим, чтобы первые два столбца всегда видны, так что мы можем заморозить те столбцы.
Свойство FrozenColumnCount задает количество столбцов, которые должны быть заморожены в DataGrid. По умолчанию в DataGrid отсутствуют замороженные столбцы. Но если установим значение FrozenColumnCount равным 2, то самые левые 2 столбца будут заморожены.
```xml
<DataGrid x:Name="WPFdataGrid" Margin="10, 10, 0, 0" 
          AutoGenerateColumns="True"
          FrozenColumnCount="2"
          >
```
Листинг 32

## Развернуть и свернуть строки DataGrid
DataGrid предоставляет свернутые и развернутые виды строк, в которых пользователи могут не только просматривать данные строки, но также можно использовать строку для редактирования и обновления данных строки.

## Свойство RowDetailsVisibilityMode
Свойство RowDetailsVisibilityMode компонента DataGrid отвечает за отображение и скрытие данных строки. Это свойство имеет одно из трех: Visible, Collapsed и VisibleWhenSelected. Значение Visible хранит данные строки видимыми все время. Значение Collapsed держать данные строки свернутыми все время. А значение VisibleWhenSelected показывает данные строки тогда, когда строка выделена.
Ниже показан пример кода, в котором этому свойству присваивается значение VisibleWhenSelected в XAML.
```xml
RowDetailsVisibilityMode ="VisibleWhenSelected"
```
Листинг 33

Следующий код в листинге 34 задает свойству RowDetailsVisibilityMode значение VisibleWhenSelected в C#.
```cs
WPFdataGrid.RowDetailsVisibilityMode = DataGridRowDetailsVisibilityMode.VisibleWhenSelected;
```
Листинг 34