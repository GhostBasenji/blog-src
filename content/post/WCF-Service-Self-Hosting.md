+++
title = "Создание и размещение WCF-службы – Self-Hosting"
date = "2019-10-15"
tags = [
    "C#", 
    "WCF", 
    "Self-hosting", 
    "Visual Studio 2019", 
    ".NET 4.5", 
    "dotnet"]
+++

В данной статье рассматривается вариант использования службы WCF методом авто-размещения (Self-Hosting).

<!--more-->

## Основная часть

Наше простейшее приложение будет производить арифметические операции над простейшими числами.
План действий:
1.	Создание WCF-службы.
2.	Создание консольного приложения для произведения арифметических операций.

### Часть 1. Создание WCF-службы
1. Запускаем Visual Studio 2019. Потом выбираем **Create a new project**.
2. В появившемся окне выбираем WCF Service Application и даем название проекту “SelfHosting”.
   
![Рис. 1](https://i.postimg.cc/kgZF6rBT/gb0024.jpg)

![Рис. 2](https://i.postimg.cc/85LHgykt/gb0025.jpg)

3. Открываем файл IService1.cs и удаляем существующие детали **DataContract**, потом добавляем новый класс *ExceptionMessage* в DataContract для показа сведения об исключении.

```cs
[DataContract]
public class ExceptionMessage
{
    private string infoExceptionMessage;
    public ExceptionMessage(string Message)
    {
        this.infoExceptionMessage = Message;
    }
    [DataMember]
    public string errorMessageOfAction
    {
        get { return this.infoExceptionMessage; }
        set { this.infoExceptionMessage = value; }
    }
}
```
4. Удаляем все перечисленное *OperationContract* в интерфейсе IService1, потом добавляем новый *OperationContracts* с **FaultContract** для выполнения арифметических операций.

```cs
[ServiceContract]
public interface IService1
{
    [OperationContract]
    [FaultContract(typeof(ExceptionMessage))]
    int Addition(int number1, int number2);

    [OperationContract]
    [FaultContract(typeof(ExceptionMessage))]
    int Subtraction(int number1, int number2);

    [OperationContract]
    [FaultContract(typeof(ExceptionMessage))]
    int Multiplication(int number1, int number2);
        
    [OperationContract]
    [FaultContract(typeof(ExceptionMessage))]
    int Division(int number1, int number2);
}
```
5. Разворачиваем файл Service1.svc и открываем файл Service1.svc.cs. Удаляем все функции, находящиеся в классе Service1. Там же будем реализовать нижеперечисленные методы интерфейса.
* Метод **Addition()**:
```cs
public int Addition(int number1, int number2)
{
    try
    {
        return number1 + number2;
    }
    catch (Exception exception)
    {
        throw new FaultException<ExceptionMessage>(new ExceptionMessage(exception.Message));
    }
}
```

* Метод **Subtraction()**:
```cs
public int Subtraction(int number1, int number2)
{
    try
    {
        if (number1 > number2)
        {
            return number1 - number2;
        }
        else
        {
            return 0;
        }
    }
    catch (Exception exception)
    {
        throw new FaultException<ExceptionMessage>(new ExceptionMessage(exception.Message));
    }
}
```

* Метод **Multiplication()**:
```cs
public int Multiplication(int number1, int number2)
{
    try
    {
        return number1 * number2;
    }
    catch (Exception exception)
    {
        throw new FaultException<ExceptionMessage>(new ExceptionMessage(exception.Message));
    }
}
```

* Метод **Division()**:
```cs
public int Division(int number1, int number2)
{
    try
    {
        if (number2 != 0)
        {
            return number1 / number2;
        }
        else
        {
            return 1;
        }
    }
    catch (Exception exception)
    {
        throw new FaultException<ExceptionMessage>(new ExceptionMessage(exception.Message));
    }
}
```
6. Итак, мы создали службу WCF для Self-Hosting. А теперь построим ее с помощью команды Build Solution.

### Часть 2. Создание консольного приложения
1. Правой кнопкой мыши щелкаем по Solution и из меню выбираем Add > New Project…
2. Выбираем консольное приложение и создаем его.
3. Добавляем ссылку на “SelfHostingTest” и на сборку “System.ServiceModel”.
4. Правой кнопкой мыши щелкаем на файле **“App.config”** консольного приложения, после чего выбираем **“Edit WCF Configuration”**.
5. Перед нами появится окно конфигурации служб.
   
![Рис. 3](https://i.postimg.cc/nrkGCCDm/gb0026.jpg)

6. Выбираем папку **“Services”**, потом щелкаем в правой стороне на ссылку **“Create a New Service…”**. Щелкаем по кнопке “Browse…”, после чего заходим в папку bin проекта SelfHostingTest. Выбираем **SelfHosting.dll** и щелкаем по кнопке Open.

![Рис. 4](https://i.postimg.cc/MpXmpZKc/gb0027.jpg)

В следующем окне выбираем нашу службу. Снова щелкаем по кнопке Open

![Рис. 5](https://i.postimg.cc/FFgZPnBK/gb0028.jpg)

Вот и все, мы определили тип службы.

![Рис. 6](https://i.postimg.cc/fyZvzxJZ/gb0029.jpg)

7. Щелкаем по кнопке Next, следующее окно попросит предоставить контракт службы. Оставляем все по умолчанию.
   
![Рис. 7](https://i.postimg.cc/SNgG4YqF/gb0030.jpg)

8. Снова щелкаем по кнопке Next. Следующее окно попросит выбрать тип связи. В нашем примере мы выберем “TCP”.
   
![Рис. 8](https://i.postimg.cc/vmV75Pnb/gb0031.jpg)

9. Щелкаем по кнопке Next. Следующее окно спросит про адрес конечной точки (endpoint address). Напишем относительный адрес службы SelfHosting.

![Рис. 9](https://i.postimg.cc/MK6YgbCm/gb0032.jpg)

10.  Снова щелкаем по кнопке Next. Следующее окно покажет список выбранных настроек.

![Рис. 10](https://i.postimg.cc/rm21jSGW/gb0033.jpg)

11.  Щелкаем по кнопке Finish. В результате чего появится наша служба.

![Рис. 11](https://i.postimg.cc/Jn3b2GKF/gb0034.jpg)

12.  Теперь нам нужно развернуть нашу службу и выбрать **“Host”**.

![Рис. 12](https://i.postimg.cc/FzD0h8Mg/gb0035.jpg)

13.  Здесь добавляем два базовых адреса: один для оконечной точки службы, а другой – для обмена метаданными. Добавляем базовый адрес, нажимая на кнопку New…

![Рис. 13](https://i.postimg.cc/rs8SXMPw/gb0036.jpg)

14.  Чтобы включить обмен метаданными, для этого нужно включить службу поведения. С помощью которой клиенты могут создавать прокси-классы. Разворачиваем “Advanced”, потом выбираем папку “Service Behavior”. В правой части окна щелкаем по ссылке **“New Service Behavior Configuration”**.

![Рис. 14](https://i.postimg.cc/9XpdPwDR/gb0037.jpg)

15.  Меняем имя поведения службы на **“SelfHostingBehavior”**.

![Рис. 15](https://i.postimg.cc/65pdM6ZH/gb0038.jpg)

16.  Нам нужно добавить новое поведение службы для обмена метаданными. Для этого выбираем **“SelfHostingBehavior”**, потом щелкаем по кнопке “Add…”, и выбираем из списка **“ServiceMetadata”**.

![Рис. 16](https://i.postimg.cc/QM15FFLM/gb0039.jpg)

17.  Потом щелкаем по **“serviceMetadata”**, чтобы установить свойство **“HttpGetEnable”** с False на True.

![Рис. 17](https://i.postimg.cc/3xPmrgc6/gb0040.jpg)

18.  А теперь нам нужно настроить это новое поведение для нашей службы. Для этого щелкаем по нашей службе “SelfHostingTest”, и устанавливаем свойство “Behavior Configuration” в “SelfHostingBehavior”.

![Рис. 18](https://i.postimg.cc/Jn8XZRm5/gb0041.jpg)

19.  Щелкаем на File в главном меню, и сохраняем все это. Потом закрываем это окно. После чего появится окно сообщения с вопросом, хотим ли сохранить все изменения. На что мы отвечаем утвердительно.

20. После чего проверим файл App.config на наличие внесенных изменений.

![Рис. 19](https://i.postimg.cc/Y9xWxTCK/gb0042.jpg)

21.  Открываем файл Program.cs консольного приложения и добавляем нижеприведенные коды.

* Подключаем следующие операторы using.
```cs
using SelfHosting;
using System.ServiceModel;
```

* Добавляем новую функцию **WCFServiceConsume()**
```cs
public static void WCFServiceConsume()
{
    try
        {
            Console.WriteLine("Self-Hosting a WCF Service in Console Application\n");
            Console.WriteLine("-------------------------------------------------\n");
            Console.WriteLine("Enter first integer number : ");
            int number1 = Convert.ToInt32(Console.ReadLine());
            Console.WriteLine("Enter second integer number : ");
            int number2 = Convert.ToInt32(Console.ReadLine());
            SelfHostingTest.Service1 wcfService = new SelfHostingTest.Service1();

            try
            {
                int addition = wcfService.Addition(number1, number2);
                Console.WriteLine("Addition Result : " + addition);
            }
            catch (FaultException<ExceptionMessage> exceptionFromService)
            {
                Console.WriteLine("Addition Service Error : " + exceptionFromService.Detail.errorMessageOfAction);
            }

            try
            {
                int subtraction = wcfService.Subtraction(number1, number2);
                Console.WriteLine("Subtraction Result : " + subtraction);
            }
            catch (FaultException<ExceptionMessage> exceptionFromService)
            {
                Console.WriteLine("Subtraction Service Error : " + exceptionFromService.Detail.errorMessageOfAction);
            }

            try
               {
                int multiplication = wcfService.Multiplication(number1, number2);
                Console.WriteLine("Multiplication Result : " + multiplication);
            }
            catch (FaultException<ExceptionMessage> exceptionFromService)
            {
                Console.WriteLine("Multiplication Service Error : " + exceptionFromService.Detail.errorMessageOfAction);
            }

            try
            {
                int division = wcfService.Division(number1, number2);
                Console.WriteLine("Division Result : " + division);
            }
            catch (FaultException<ExceptionMessage> exceptionFromService)
            {
                Console.WriteLine("Division Service Error : " + exceptionFromService.Detail.errorMessageOfAction);
            }
            Console.WriteLine("*********************************\n");
        }
    catch (Exception exception)
    {
        Console.WriteLine(exception.Message);
    }
    finally
    {
        ConsoleClose();
    }
}
```

* Добавляем новую функцию **ConsoleClose()**
```cs
public static void ConsoleClose()
{
    Console.WriteLine("Are you sure to close the application? (1/0)\n");
    string close = Console.ReadLine();
    if (close == "1")
    {
        Console.Clear();
        WCFServiceConsume();
    }
}
```

* Вызываем функцию WCFServiceConsume() в методе **Main**
```cs
static void Main(string[] args)
{
    WCFServiceConsume();
}
```

22. Назначаем Консольное приложение в качестве первого запускаемого проекта. Для этого щелкаем правой кнопкой мыши на проект **SelfHostingConsole**, потом выбираем из контекстного меню Set as StartUp Project.

23. Запускаем приложение.

### Тестируем приложение
* Успешное выполнение

![Рис. 20](https://i.postimg.cc/kXYWzrF7/gb0043.jpg)

* Обработка ошибок

![Рис. 21](https://i.postimg.cc/L8qjMyNL/gb0044.jpg)

[**Скачать пример приложения**](https://github.com/GhostBasenji/SampleSelfHosting/archive/master.zip)