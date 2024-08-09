## Задание: Создание SOAP-сервиса для управления задачами (Task Management)  

Цель: Разработать SOAP веб-сервис, который позволит управлять задачами. Сервис должен поддерживать следующие операции:  
1. `CreateTask` : Создание новой задачи.  
2. `GetTask` : Получение информации о задаче по её идентификатору.  
3. `UpdateTask` : Обновление информации о задаче.  
4. `DeleteTask` : Удаление задачи.  
Требования к задаче (Task):  
- `TaskID` : Уникальный идентификатор задачи (строка).  
- `Title` : Заголовок задачи (строка).  
- `Description` : Описание задачи (строка).  
- `Status` : Статус задачи ("New", "In Progress", "Completed").  

Дополнительные требования:  
1. Сервис должен возвращать соответствующие ошибки в случае, если задача с заданным TaskID не найдена.  
2. Используйте WSDL для описания сервиса.  
  
Ваша задача — создать WSDL-файл, который полностью описывает данный сервис.

```WSDL
<?xml version="1.0" encoding="UTF-8"?>
<wsdl:definitions xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap"
    xmlns:tns="http://www.example.com/taskmanagement"
	xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/"
	xmlns:xsd="http://www.w3.org/2001/XMLSchema"
	targetNamespace="http://www.example.com/taskmanagement">

<!-- Type Definitions -->
<wsdl:types>
  <xsd:schema targetNamespace="http://www.example.com/taskmanagement">
   <xsd:element name="Task">
   <xsd:complexType>
    <xsd:sequence>
     <xsd:element name="TaskID" type="xsd:string"/>
     <xsd:element name="Title" type="xsd:string"/>
     <xsd:element name="Description" type="xsd:string"/>
     <xsd:element name="Status" type="xsd:string"/>
    </xsd:sequence>
   </xsd:complexType>
  </xsd:element>
 </xsd:schema>
</wsdl:types>

<!-- Mesage Definitions -->
<wsdl:message name="CreateTaskRequest>
 <wsdl:part name="task" element="tns:Task"/>
</wsdl:message>
<wsdl:message name="TaskResponse">
 <wsdl:part name="task" element="tns:Task"/>
</wsdl:message>
<wsdl:message name="GetTaskRequest">
 <wsdl:part name="TaskID" type="xsd:string"/>
</wsdl:message>
<wsdl:message name="UpdateTaskRequest">
 <wsdl:part name="task" element="tns:Task"/>
</wsdl:message>
<wsdl:message name="DeleteTaskRequest">
 <wsdl:part name="TaskID" type="xsd:string"/>
</wsdl:message>

<!-- Port Type Definitions -->
<wsdl:portType name="TaskManagementPortType">
 <wsdl:operation name="CreateTask">
  <wsdl:input mesage="tns:CreateTaskRequest"/>
  <wsdl:output message="TaskResponse"/>
 </wsdl:operation>
 <wsdl:operation name="GetTask>
  <wsdl:input name="tns:GetTaskRequest"/>
  <wsdl:output name="tns:TaskResponse"/>
  <wsdl:fault name="NotFoundError" message="tns:NotFoundError"/>
 </wsdl:operation>
 <wsdl:operation name="UpdateTask">
  <wsdl:input name="tns:UpdateTaskRequest"/>
  <wsdl:output name="tns:TaskResponse">
 </wsdl:operation>
 <wsdl:operation name="DeleteTask">
  <wsdl:input name="tns:DeleteTaskRequest"/>
  <wsdl:output name="tns:TaskResponse"/>
 </wsdl:operation>
</wsdl:portType>

<!-- Binding Definitions -->
<wsdl:binding name="TaskManagementBinding" type="tns:TaskManagementPortType">
 <soap:binding style="document" transport="http://schemas.xmlsoap.org/soap/http"/>
 <wsdl:operation name="CreateTask">
  <soap:operation soapAction="http://www.example.com/taskmanagement/CreateTask"/>
  <wsdl:input>
   <soap:body use="literal"/>
  </wsdl:input>
  <wsdl:output>
   <soap:body use="literal"/>
  </wsdl:output>
 </wsdl:operation>
 <wsdl:operation name="GetTask">
  <soap:operation soapAction="http://www.example.com/taskmanagement"/>
  <wsdl:input>
   <soap:body use="literal"/>
  </wsdl:input>
  <wsdl:output>
   <soap:body use="literal"/>
  </wsdl:output>
  <wsdl:fault name="NotFoundError">
   <soap:fault name="NotFoundError" use="literal"/>
  </wsdl:fault>
 </wsdl:operation>
 <wsdl:operation name="UpdateTask">
  <soap:operation soapAction="http://www.example.com/taskmanagement/UpdateTask"/>
  <wsdl:input>
   <soap:body use="literal"/>
  </wsdl:input>
  <wsdl:output>
   <soap:body use="literal"/>
  </wsdl:output>
</wsdl:operation>
 <wsdl:operation name="DeleteTask">
  <soap:operation soapAction="http://www.example.com/taskmanagement"/>
   <wsdl:input>
   <soap:body use="literal">
   </wsdl:input>
  <wsdl:output>
	  <soap:body use="literal">
	</wsdl:output>
	</wsdl:operation>
</wsdl:binding>

<!-- Service Definitions -->
<wsdl:service name="TaskManagementService"> 
<wsdl:port name="TaskManagementPort" binding="tns:TaskManagementBinding">  
<soap:address location="http://www.example.com/taskmanagement"/>  
</wsdl:port>  
</wsdl:service>  
</wsdl:definitions>
```

-------------------------------------

## Описание файла

### Объявление пространства имен и общие атрибуты

1. `?xml version="1.0" encoding="UTF-8"?>`: Версия XML и кодировка документа
2. `<wsdl:definitions>`: Корневой элемент WSDL. Объявляет пространство имен и атрибуты, которые будут использоваться в WSDL документе.
	-	`xmlns:soap`: Пространство имен для SOAP. URL `http://schemas.xmlsoap.org/wsdl/soap/` - версия SOAP 1.1
	-	`xmlns:tns`: Пространство имен для конкретной службы. tns - `Target Name Space`
	-	`xmlns:wsdl`: Стандартное пространство имен WSDL
	-	`xmlns:xsd`: Стандартное пространство имен XML Schema
	-	`targetNameSpace`: URL, уникально идентифицирующий веб-сервис

### Определения типов

1. `<wsdl:types>`: Элемент, содержащий определения всех типов данных, используемых в веб-сервисе.
2. `<xsd:schema targetNamespace="http://www.example.com/taskmanagement">`: Определение схемы и использует то же пространство имен, что и весь веб-сервис.
3. `<xsd:element name="Task">...</xsd:element>`: Определяет структуру "Task", которая будет использована в сообщениях

### Определения сообщений

1. `<wsdl:message name="CreateTaskRequest">...</wsdl:message>`: Определяет структуру входящего сообщения для операции `CreateTask`

### Определения порта

1. `<wsdl:portType name="TaskManagementPortType">...</wsdl:portType>: `portType` определяет набор операций, которые можно выполнить с веб-сервисом

## Определения привязки
1.  `<wsdl:binding name="TaskManagementBinding" type="tns:TaskManagementPortType"> ... </wsdl:binding>`: binding  описывает конкретные протоколы и форматы данных для операций и сообщений, определенных в  portType.
2.  `<soap:binding style="document" transport="http://schemas.xmlsoap.org/soap/http"/>`: элемент уточняет, что используется стиль "document" и протокол "HTTP".

## Определения службы
1.  `<wsdl:service name="TaskManagementService"> ... </wsdl:service>` : элемент определяет сервис и указывает порт (или порты), который будет использоваться.
2.  `<soap:address location="http://www.example.com/taskmanagement"/>` : элемент определяет URL, по которому доступен веб-сервис.
