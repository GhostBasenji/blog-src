+++
title = "Основы работы с WPF DataGrid. Часть 2. - Layout и Border"
date = "2019-09-10 16:02:40"
tags = [
    "WPF",
    "XAML",
    "WPF DataGrid"
]
+++

Во второй части данной серии мы рассмотрим разметку и границы компонента DataGrid. Свойства, рассматриваемые в этой статье, -- margin, width, height и border. 

<!--more-->

Свойства являются одним из наиболее важных аспектов компонента (элемента управления). Каждый компонент в WPF имеет 2 подхода использования и задания значения свойств. Первый подход [design-time] заключается в задании во время разработки значений в XAML, а второй [run-time] – во время выполнения задавая значения свойства в коде C#.
 
### Свойство Margin
Свойство **Margin** задает поля размещения компонента DataGrid в окне. Поле – это пространство между DataGrid и другими компонентами, которые будут смежными во время разметки пользовательского интерфейса.

**Thickness** описывает толщину рамки вокруг прямоугольника. Он имеет 4 двойных значений, описывающие левую, верхнюю, правую и нижнюю стороны прямоугольника соответственно.
Если перетащим DataGrid в окно и изменим его размеры, то увидим прямоугольник с синей рамкой и четырьмя маркерами с двойными значениями. Эти значения являются значениями полей DataGrid (см. рис. 3).

![Рис. 3](https://i.postimg.cc/W14fvmfr/gb0003.jpg)
 
Код XAML для компонента DataGrid приведен в листинге 6. В этом листинге задается свойство Margin для DataGrid во время разработки.
```xml
<Grid x:Name="Window" Loaded="Window_Loaded">
  <DataGrid x:Name="WPFdataGrid" HorizontalAlignment="Left"
     Height="325" Margin="30,37,0,0" VerticalAlignment="Top" 
     Width="711"/>
</Grid>
```
Листинг 6.

Фрагмент кода в листинге 7 создает объект Thickness и задает свойство Margin компонента DataGrid.
```cs
  Thickness gridMargin = new Thickness();
  gridMargin.Bottom = 20;
  gridMargin.Left = 20;
  gridMargin.Right = 24;
  gridMargin.Top = 10;
  WPFdataGrid.Margin = gridMargin;
```
Листинг 7.

### Свойство Height и Width
Свойства Height и Width представляют высоту и ширину DataGrid соответственно. Нижеприведенный код в листинге 8 задает высоту и ширину DataGrid.
```xml
<DataGrid x:Name="WPFdataGrid" HorizontalAlignment="Left" 
          Margin="30,37,0,0" VerticalAlignment="Top" Height="325" Width="711"/>
```
Листинг 8.

В листинге 9 код задает свойства Height и Width компонента DataGrid в режиме выполнения.
```cs
WPFdataGrid.Width = 800;
WPFdataGrid.Height = 200;
```
Листинг 9.

**Примечание**. Если в программировании применяются оба подхода, то значения run-time будут применены в последнюю очередь. Мы можем использовать подход run-time в том случае, если не уверены в настройках свойства. Но если мы уже знаем все значения свойств при проектировании интерфейса, то рекомендуется использовать подход design-time.

### Fill Width
Часто нам требуется, чтобы DataGrid заполнил все окно по горизонтали. Мы можем сделать это, установив значения свойств HorizontalAlignment, HorizontalContentAlignment и ColumnWidth в Stretch, Stretch и * соответственно (см. листинг 10).
```xml
<DataGrid x:Name="WPFdataGrid" Margin="0,0,0,0"
    VerticalAlignment="Top"
    Height="325" HorizontalAlignment="Stretch"
    HorizontalContentAlignment="Stretch"
    ColumnWidth="*"/>
</Grid>
```
Листинг 10.

### Border [Граница]

Свойства BorderBrush и BorderThickness используются для задания цвета и ширины границы. Нижеприведенный фрагмент кода присваивает цвет границы – синий и задает толщину границы в 5.
```xml
<Grid x:Name="Window" Loaded="Window_Loaded">
  <DataGrid x:Name="WPFdataGrid" Margin="0,0,0,0"
  VerticalAlignment="Top"
  Height="325" HorizontalAlignment="Stretch"
  HorizontalContentAlignment="Stretch"
  ColumnWidth="*"
  BorderBrush="Blue" BorderThickness="5"/>
</Grid>
```
Листинг 11.

На нижеприведенном рисунке видим DataGrid с измененной границей.

![Рис. 4](https://i.postimg.cc/T3HNYyZs/gb0004.jpg)
