## XDTO-пакеты

Все типы данных XDTO подразделяются на типы-значения и типы-объекты. Типы-значения позволяют определять простые типы, например: строки, числа, даты, булевы значения и т. д. Типы-объекты позволяют определять сложные типы, такие как структуры и массивы.

**Структуры моделируются типами-объектами.** Тип-объект может содержать свойства, которые соответствуют элементам структуры. Каждое свойство характеризуется уникальным именем и типом. Тип свойства может быть как типом-значением, так и типом-объектом.
 
![XDTO-пакет](https://raw.githubusercontent.com/grydni4ok/1C/main/%D0%A2%D0%B5%D1%85%D0%BD%D0%BE%D0%BB%D0%BE%D0%B3%D0%B8%D0%B8%20%D0%B8%D0%BD%D1%82%D0%B5%D0%B3%D1%80%D0%B0%D1%86%D0%B8%D0%B8/XDTO-%D0%BF%D0%B0%D0%BA%D0%B5%D1%82.png)

**Сформируем свой XDTO-пакет для Web-сервиса.**


**Товар** – для передачи данных элемента справочника Товары. Этот тип объектов XDTO будет содержать свойство:<br>
 - Наименование – тип string из пространства имен http://www.w3.org/2001/XMLSchema.

**Клиент** – для передачи данных элемента справочника Клиенты. Этот тип объектов XDTO будет содержать свойство:<br>
 - Наименование – тип string из пространства имен http://www.w3.org/2001/XMLSchema.

**СтрокаЗаказа** – для передачи данных одной строки состава заказа товаров. Этот тип объектов XDTO будет содержать следующие свойства:
 - Товар – тип Товар из пространства имен http://localhost/REST. Представляет собой ссылку на объект XDTO, определенный нами ранее, в предыдущем примере;
 - Количество – тип int из пространства имен http://www.w3.org/2001/XMLSchema;
 - Цена – тип int из пространства имен http://www.w3.org/2001/XMLSchema;
 - Сумма – тип int из пространства имен http://www.w3.org/2001/XMLSchema.


**Заказ** – для передачи всех данных одного заказа. Этот тип объектов XDTO будет содержать следующие свойства:
 - Дата – тип date из пространства имен http://www.w3.org/2001/XMLSchema;
 - Клиент – тип Клиент из пространства имен http://localhost/REST. Представляет собой ссылку на объект XDTO, определенный нами выше;
 - Состав – тип СтрокаЗаказа из пространства имен http://localhost/REST. Представляет собой ссылку на объект XDTO, определенный нами выше. Для того чтобы это свойство могло содержать неограниченное множество значений, установим его свойство Максимальное количество в значение -1 ;
 - Представление – тип string из пространства имен http://www.w3.org/2001/XMLSchema.

**Заказы** – для передачи данных всех заказов. Этот тип объектов XDTO будет содержать единственное свойство:
 - Список – тип Заказ из пространства имен http://localhost/REST. Представляет собой ссылку на объект XDTO, определенный нами выше. Для того чтобы это свойство могло содержать неограниченное множество значений, установим его свойство Максимальное количество в значение -1.

Подробное описание создание и использование Web-сервисов https://its.1c.ru/db/intgr83#content:78:hdoc

Дальнейшее использование возможно с помощью слдующего кода:
```
Процедура WSссылкаНажатие(Элемент) 
	//при необходимости, нужно передать имя пользователя и пароль 2 и 3им параметром
	Определения = Новый WSОпределения("http://localhost/TEST/ws/wsOrdersTest.1cws?wsdl");
	
	//получаем доступ и используем созданный нами Web-сервис 
	Прокси = Новый WSПрокси(Определения, "http://localhost/TEST", "ЗаказыТест", "ЗаказыТестSoap");
	НеЗакрытыеЗаказы = Прокси.НеЗакрытыеЗаказы();
КонецПроцедуры
```
