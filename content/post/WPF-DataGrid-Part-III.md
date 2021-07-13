+++
title = "Основы работы с WPF DataGrid. Часть 3. - Заголовок компонента DataGrid"
date = "2019-09-11 16:02:40"
tags = [
    "WPF",
    "XAML",
    "WPF DataGrid"
]
+++

В третьей части «Основы работы с WPF DataGrid» рассматриваются видимость заголовка [**header**] компонента DataGrid и внешний вид заголовка столбцов. 

<!--more-->

### Свойство HeadersVisibility
Заголовок компонента DataGrid можно показать или скрыть с помощью свойства HeadersVisibility. Свойство HeadersVisibility имеет четыре значения: All, Column, None и Row. Если хотим отобразить заголовки строк и столбцов, то задаем значение All свойству HeadersVisibility. Значение None скрывает заголовки строк и столбцов. А значения Column и Row отображают заголовки только столбцов и строк соответственно.

![Рис. 5](https://i.postimg.cc/fbdTZYDj/gb0005.jpg)
Код в листинге 12 прячет заголовки строки и столбца компонента DataGrid.
```xml
<DataGrid x:Name="WPFdataGrid" Margin="0,0,0,0"
                  VerticalAlignment="Top"
                  Height="325" HorizontalAlignment="Stretch"
                  HorizontalContentAlignment="Stretch"
                  ColumnWidth="*"
                  AlternatingRowBackground="Green"
                  BorderBrush="Blue" BorderThickness="5"
                  HeadersVisibility="None"/>
</Grid>
```
Листинг 12.

Ниже представлен результат применения значения None свойства HeadersVisibility.

![Рис. 6](https://i.postimg.cc/ydX13BJD/gb0006.jpg)

### Свойство ColumnHeaderStyle
Часто возникает необходимость изменять внешний вид заголовка DataGrid. Свойство ColumnHeaderStyle используется для применения стиля ко всем заголовкам столбцов DataGrid.

DataGrid также предоставляет возможность изменять внешний вид заголовка отдельных столбцов с помощью свойства **DataGridColumn.HeaderStyle**.

**Style** (стиль) может быть применен ко всем заголовкам столбцов или к отдельному заголовку столбца. Чтобы применить Style к отдельному заголовку, задаем свойство DataGridColumn.HeaderStyle, которое имеет приоритет перед свойством DataGrid.ColumnHeaderStyle.

Style обычно создается как ресурс приложения, страницы (page) или окна (window). Стиль используется для определения и задания свойства с помощью имени и значений свойства.
Код в листинге 13 создает Style как ресурс Windows. Первый Style ориентирован на DataGrid, а второй Style – на DataGridColumnHeader. Стиль DataGridColumnHeader задает свойства Height, Background, Foreground, FontSize и FontFamily.
```xml
<Window.Resources>
    <Style x:Key="DGHeaderStyle" TargetType="{x:Type DataGrid}">
      <Setter Property="ColumnHeaderStyle" Value="{DynamicResource DGCHeaderStyle}"/>
    </Style>
    <Style x:Key="DGCHeaderStyle" TargetType="DataGridColumnHeader">
        <Setter Property="Height" Value="30"/>
        <Setter Property="Background" Value="LightBlue" />
        <Setter Property="Foreground" Value="Black"/>
        <Setter Property="FontSize" Value="14" />
        <Setter Property="FontFamily" Value="Calibri" />
    </Style>
</Window.Resources>
```
Листинг 13.

Код в листинге 14 задает Style компонента DataGrid с помощью свойства Style.
```xml
<DataGrid x:Name="WPFdataGrid" Margin="0"
        AutoGenerateColumns="True"
        SelectionUnit="Cell"
        Style="{DynamicResource DGHeaderStyle}">
</DataGrid>
```
Листинг 14.
Ниже представлен результат применения Style.

![Рис. 7](https://i.postimg.cc/pTtVdydN/gb0007.jpg)