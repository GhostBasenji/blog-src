+++
title = "Основы работы с WPF DataGrid. Часть 1. - Введение"
date = "2019-09-07"
tags = [
    "WPF",
    "C#",
    "WPF DataGrid"
]
+++

Этой статьей я начинаю свою серию статей “Осваиваем WPF DataGrid”, в которой мы рассмотрим, как работать с элементом управления WPF DataGrid и его функциональность. В этой серии мы узнаем, как использовать элемент управления WPF DataGrid в реальных приложениях. 
 
WPF DataGrid – один из наиболее широко используемых элементов управления (далее для краткости компонент). Компонент DataGrid отображает данные в формате таблицы, а также позволяет добавлять, обновлять, удалять, фильтровать и сортировать данные, отображаемые в DataGrid. 

<!--more-->

Данная статья является первой статьей (поэтому называется“Введение”), и она описывает простую привязку данных (data binding).
 
### Создание нового приложения WPF 
Создаем приложение WPF с помощью интегрированной среды разработки IDE Visual Studio, и перетаскиваем компонент DataGrid с панели элементов на форму. Ниже показаны панель элементов, форма с DataGrid и просмотр кода XAML.

![Рис. 1](https://i.postimg.cc/3wvdnvM7/gb0001.jpg)
 
Можно использовать маркеры Grid для изменения размеров и перемещения компонента DataGrid. 
 
Конструктор [или дизайнер] IDE Visual Studio не только создает макет компонента, но и создает код XAML. Нижеприведенный листинг демонстрирует типичный XAML-код, созданный конструктором.
```xml
<Window x:Class="WPFDataGridSample.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:WPFDataGridSample"
        mc:Ignorable="d"
        Title="MainWindow" Height="450" Width="800">
    <Grid>
        <DataGrid x:Name="WPFdataGrid" HorizontalAlignment="Left" Height="307" Margin="30,37,0,0" VerticalAlignment="Top" Width="706"/>
    </Grid>
</Window>
```
Листинг 1.

Элемент DataGrid в XAML представляет компонент DataGrid, а свойства Width и Height – ширину и высоту DataGrid. Свойство Margin задает поля размещения DataGrid в окне. Свойство Name представляет имя компонента, являющегося уникальным идентификатором компонента. А теперь изменим имя компонента, отредактировав свойство Name. Измененный код XAML смотрим в листинге 2.
```xml
    <Grid>
        <DataGrid x:Name="WPFdataGrid" HorizontalAlignment="Left" Height="307" Margin="30,37,0,0" VerticalAlignment="Top" Width="706"/>
    </Grid>
```
Листинг 2.

### Привязка данных [Data Binding] 
Следующий шаг после создания компонента DataGrid – отображение в нем некоторых данных. Как известно нам, компонент DataGrid отображает данные в виде таблицы. Таблица представляет собой набор строк и столбцов, поэтому наши данные также быть в одном и том же формате. 

### Коллекция данных [Data Collection] 
Прежде чем мы сможем отобразить данные в DataGrid, у нас должны быть какие-нибудь данные. Данные, которые являются коллекцией объектов. 
Давайте создадим класс, который имеет некоторые общедоступные свойства. Фрагмент кода в листинге 3 определяет класс Author с пятью общедоступными свойствами. Эти свойства таковы: ID, Name, BookTitle и Sci-Fi с соответствующими типами int, string, string и bool.
```cs
public class Author  
{  
   public int ID { get; set; }  
   public string Name { get; set; }  
   public string BookTitle { get; set; }  
   public bool SciFi { get; set; }  
}
```
Листинг 3.

Теперь у нас есть объект. Все, что нам нужно сделать, – это создать коллекцию. Как только у нас будет коллекция объектов, мы сможем отобразить их данные в DataGrid. 
Фрагмент кода в листинге 4 создает список объектов-авторов с помощью метода LoadCollectionData.
```cs
public class AuthorCollection : CollectionBase  
{  
   public List<Author> LoadAuthors()  
   {  
      List<Author> authors = new List<Author>();  
      authors.Add(new Author()  
      {  
         ID = 101,  
         Name = "А.С. Пушкин",  
         BookTitle = "Капитанская дочка",  
         SciFi = false  
      });  
      authors.Add(new Author()  
      {  
         ID = 201,  
         Name = "Роберт Хайнлайн",  
         BookTitle = "Пасынки Вселенной",  
         SciFi = true  
      });  
      authors.Add(new Author()  
      {  
         ID = 244,  
         Name = "Клиффорд Саймак",  
         BookTitle = "Заповедник гоблинов",  
         SciFi = true  
      });  
      return authors;  
   }  
}
```
Листинг 4.

### ItemsSource 
Свойство ItemsSource компонента DataGrid является ключом к привязке данных. Пользователь может связать любой источник данных, который реализует IEnuemerable. Каждая строка в DataGrid привязана к объекту источника данных, и каждый столбец – к свойству объектов источника данных. Чтобы отобразить коллекцию данных в DataGrid, нам просто нужно привязать его свойство ItemsSource к коллекции Author, которую мы создали в классе AuthorCollection. Щелкаем по форме, используем окном свойств и создаем обработчик события Window Loaded. В обработчике событий Window Loaded мы создаем объект AuthorCollection и вызываем его метод LoadAuthors() для привязка к DataGrid, задав свойство ItemsSource в DataGrid.
```cs
private void Window_Loaded(object sender, RoutedEventArgs e)  
  {  
    AuthorCollection authors = new AuthorCollection();
    WPFdataGrid.ItemsSource = authors.LoadAuthors();  
  }
  ```
  Листинг 5.

### Сборка и запуск 
Теперь соберем и запустим наше приложение, нажав F5. Вот что мы увидим – результат наших дел.

![Рис. 2](https://i.postimg.cc/fbxrc8bN/gb0002.jpg)

Как видим на вышеприведенном скрине, имена свойств объекта автоматически генерируются в виде столбцов DataGrid с названием, являющимся именем свойства. 

**Заключение.** В этой первой статье мы рассмотрели, как создается DataGrid с помощью Visual Studio и отображаются в нем некоторые данные. В следующей статье мы рассмотрим некоторые общие свойства компонента WPF DataGrid.