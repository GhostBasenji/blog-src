+++
title = "Основы работы с WPF DataGrid. Часть 6. - Шаблон данных [Data Template]"
date = "2019-10-10"
tags = [
    "WPF",
    "XAML",
    "WPF DataGrid"
]
+++

В этой статье описывается, как используется шаблон данных [data template] в DataGrid.

<!--more-->

### Шаблон данных

Компонент DataGrid не только отображает данные в формате строки и столбца, но также может использоваться для отображения данных в шаблонном формате. Шаблон используется для отображения данных строки, сгруппированных в шаблон. Шаблон данных можно определить как XAML или как ресурс. Представим себе, что нам нужно отобразить 50 полей в DataGrid, но строка может отображать до 10 столбцов. Итак, как отобразим больше столбцов? Для этого нам поможет **DataTemplate**.
Если посмотрим на рис. 13, то увидим, что строка DataGrid содержит 5 столбцов, но 3 дополнительных столбцов отображаются как часть шаблона данных.

![Рис. 18.](https://i.postimg.cc/pT2TG0mf/gb0023.jpg)

### Свойство RowDetailsTemplate

Свойство **RowDetailsTemplate** представляет DataTemplate, который используется для отображения сведений о строке. События LoadingRowDetails и UnloadingRowDetails используются для загрузки и выгрузки шаблона данных или внесения изменений.
Значение DataTemplate задается как RowDetailsTemplate компонента DataGrid. DataTemplate определяет визуальное представление всех элементов XAML строки.
В листинге 34 показано, как задать свойство RowDetailsTemplate объекта DataGrid.
```xml
<DataGrid x:Name="WPFdataGrid"                  
<DataGrid.RowDetailsTemplate>
                      <DataTemplate>
                      </DataTemplate>
              </DataGrid.RowDetailsTemplate>
</DataGrid>
```
Листинг 34.

Ранее мы определили класс Author. А теперь давайте добавим еще 3 свойства в класс Author – City, Country и Years. Новый класс приведен в листинге 35.
```cs
    public class Author
    {
        public int ID { get; set; }
        public string Name { get; set; }
        public string BookTitle { get; set; }
        public bool SciFi { get; set; }
        public string City { get; set; }
        public string Country { get; set; }
        public DateTime Years { get; set; }
    }
```
Листинг 35.

Листинг 36 отображает новый XAML компонента DataGrid со значением DataTemplate.
```xml
    <Grid x:Name="Window" Loaded="Window_Loaded">
        <DataGrid x:Name="WPFdataGrid" Margin="0" 
        AutoGenerateColumns="False">

            <DataGrid.Columns>
                <DataGridTextColumn Binding="{Binding ID}" Header="ИД Автора" IsReadOnly="True"/>
                <DataGridTextColumn Binding="{Binding Name}" Header="Автор" Width="140">
                    <DataGridTextColumn.ElementStyle>
                        <Style TargetType="TextBlock">
                            <Setter Property="TextWrapping" Value="Wrap"/>
                        </Style>
                    </DataGridTextColumn.ElementStyle>
                    <DataGridTextColumn.EditingElementStyle>
                        <Style TargetType="TextBox">
                            <Setter Property="Foreground" Value="Blue"/>
                        </Style>
                    </DataGridTextColumn.EditingElementStyle>
                </DataGridTextColumn>

                <DataGridTemplateColumn Header="Год" Width="80">
                    <DataGridTemplateColumn.CellTemplate>
                        <DataTemplate>
                            <TextBlock Text="{Binding Years}" Margin="4"/>
                        </DataTemplate>
                    </DataGridTemplateColumn.CellTemplate>
                    <DataGridTemplateColumn.CellEditingTemplate>
                        <DataTemplate>
                            <DatePicker SelectedDate="{Binding Years, Mode=TwoWay}"/>
                        </DataTemplate>
                    </DataGridTemplateColumn.CellEditingTemplate>
                </DataGridTemplateColumn>

                <DataGridTextColumn Header="Произведение" Width="240" Binding="{Binding BookTitle}">
                    <DataGridTextColumn.ElementStyle>
                        <Style TargetType="TextBlock">
                            <Setter Property="TextWrapping" Value="Wrap"/>
                        </Style>
                    </DataGridTextColumn.ElementStyle>
                    <DataGridTextColumn.EditingElementStyle>
                        <Style TargetType="TextBox">
                            <Setter Property="Foreground" Value="Blue"/>
                        </Style>
                    </DataGridTextColumn.EditingElementStyle>
                </DataGridTextColumn>
                <DataGridCheckBoxColumn Header="Sci-Fi" Binding="{Binding SciFi}" IsThreeState="True"/>
            </DataGrid.Columns>

            <DataGrid.RowDetailsTemplate>
                <DataTemplate>
                    <Border BorderThickness="0" Background="Beige" Padding="10">
                        <Grid Margin="5, 0, 0, 0" MinWidth="650" HorizontalAlignment="Left">
                            <Grid.ColumnDefinitions>
                                <ColumnDefinition Width="125"></ColumnDefinition>
                                <ColumnDefinition Width="*"></ColumnDefinition>
                                <ColumnDefinition Width="125"></ColumnDefinition>
                                <ColumnDefinition Width="*"></ColumnDefinition>
                            </Grid.ColumnDefinitions>
                            <Grid.RowDefinitions>
                                <RowDefinition Height="Auto"></RowDefinition>
                                <RowDefinition Height="Auto"></RowDefinition>
                                <RowDefinition Height="Auto"></RowDefinition>
                                <RowDefinition Height="Auto"></RowDefinition>
                            </Grid.RowDefinitions>

                            <TextBlock Text="Город" Margin="10, 0, 0, 0" Grid.Row="0" Grid.Column="0" VerticalAlignment="Center" HorizontalAlignment="Left"/>
                            <TextBlock Margin="3" Grid.Row="0" Grid.Column="1" Text="{Binding Path=City}" MaxHeight="35"/>
                            <TextBlock Text="Страна" Margin="10, 0, 0, 0" Grid.Row="1" Grid.Column="0" VerticalAlignment="Center" HorizontalAlignment="Left"/>
                            <TextBlock Margin="3" Grid.Row="1" Grid.Column="1" Text="{Binding Path=Country}" MaxHeight="35"/>
                        </Grid>
                    </Border>
                </DataTemplate>
            </DataGrid.RowDetailsTemplate>
        </DataGrid>
    </Grid>
</Window>
```
Листинг 36.

В листинге 37 приведена новая коллекция AuthorCollection с обновленными объектами Author.
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
                SciFi = false,
                Years = new DateTime(1836, 01, 03),
                City = "Москва",
                Country = "Россия"
            });
            authors.Add(new Author()
            {
                ID = 201,
                Name = "Роберт Хайнлайн",
                BookTitle = "Пасынки Вселенной",
                SciFi = true,
                Years = new DateTime(1941, 5, 13),
                City = "Батлер, штат Миссури",
                Country = "США"
            });
            authors.Add(new Author()
            {
                ID = 244,
                Name = "Клиффорд Саймак",
                BookTitle = "Заповедник гоблинов",
                SciFi = true,
                Years = new DateTime(1968, 9, 21),
                City = "Милвилл, штат Висконсин",
                Country = "США"
            });
            return authors;
        }
    }
```
Листинг 37.

Теперь запустим проект. Щелкнуть по строке, то увидим, что дополнительные свойства Author отобразятся под строкой.

![Рис. 18.](https://i.postimg.cc/pT2TG0mf/gb0023.jpg)

### Получение выделенных элементов
Свойство SelectedItems возвращает все выделенные элементы в DataGrid. Каждый выделенный элемент представляет собой объект, привязанный к строке. Например, в нашем случае объект Author и его свойства привязаны к строкам DataGrid.
В листинге 38 код использует свойство DataGrid.SelectedItems и отображает ряд выделенных элементов, а затем отображает значения столбца Name выделенных элементов.
```cs
            AuthorCollection authors = new AuthorCollection();
            WPFdataGrid.ItemsSource = authors.LoadAuthors();

            var AuthorInfo = new System.Text.StringBuilder();
            MessageBox.Show(WPFdataGrid.SelectedItems.Count.ToString() + "Элементы выделены.");
            foreach (Author author in WPFdataGrid.SelectedItems)
            {
                AuthorInfo.AppendLine(author.Name);
            }
            MessageBox.Show(AuthorInfo.ToString());
```
Листинг 38.