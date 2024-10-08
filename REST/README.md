
## Задание: Проектирование ресурсов

Представьте веб-приложение для работы с проектами и задачами в них. Как могут выглядеть URL ресурсов для API этого веб-приложения?  

Придумайте URL для каждого ендпоинта из списка:  
- для получения списка всех проектов  
- для просмотра/создания/редактирования/удаления проекта  
- для получения списка задач в определённом проекте  
- для просмотра/создания/редактирования/удаления задачи в определённом проекте  
  
**Пример**:
- получение информации о пользователе - /users/{userId}  

- для получения списка всех проектов
``` JSON
/projects
```
- для просмотра/создания/редактирования/удаления проекта
``` JSON
/projects/{projectId} 
(создание проекта POST /projects)
```
- для получения списка задач в определённом проекте
``` JSON
/projects/{projectId}/tasks
```
- для просмотра/создания/редактирования/удаления задачи в определённом проекте
``` JSON
/projects/{projectId}/tasks/{taskId} 
(создание задачи POST /projects/{projectId}/tasks)
```

## Задание: Проектирование методов

Какие методы для ресурсов вы будете использовать в каждом ендпоинте:  

- для получения списка всех проектов  
- для просмотра, создания, редактирования, удаления проекта  
- для получения списка задач в определённом проекте  
- для просмотра, создания, редактирования, удаления задачи в определённом проекте  
  
В итоге должны получится методы и ендпоинты.

- Для получения списка всех проектов
```JSON
GET /projects
```
- Для просмотра, создания, редактирования, удаления проекта
``` JSON
GET /projects/{projectId}
POST /projects
PATCH /projects/{projectId}
DELETE /projects/{projectId}
```
- Для получения списка задач в определённом проекте
``` JSON
GET /projects/{projectId}/tasks
```
- Для просмотра, создания, редактирования, удаления задачи в определённом проекте
```JSON
GET /projects/{projectId}/tasks/{taskId}
POST /projects/{projectId}/tasks
PATCH /projects/{projectId}/tasks/{taskId}
DELETE /projects/{projectId}/tasks/{taskId}
```

## Задание: проектирование endpoint + url + тело (при необходимости) для каждой функции

Допустим, у нас есть ресурсы:  
- projects  
- team-members  
- tasks  

Спроектируйте для каждой функции endpoint: метод + URL, и (при необходимости) тело запроса. 

Например - GET /projects  

1. Создать новый проект с именем и описанием.  
2. Добавить в проект нового члена команды с именем и ролью.  
3. Создать новую задачу в рамках проекта с названием, описанием, назначенным членом команды и статусом.  
4. Обновить название или описание существующего проекта.  
5. Обновить роли члена команды в проекте.  
6. Обновить название, описание, назначенного члена команды или статус задачи в проекте.  
7. Удалить члена команды из проекта.  
8. Удалить задачу в проекте.  
9. Удалить проект.  
10. Получить отдельный проект со всеми его задачами и членами команды по его ID.  
11. Получить список всех проектов, включая их задачи и членов команды.  
  
В итоге должен получится для каждой функции метод + URL и (при необходимости) тело запроса.  

1. Создать новый проект с именем и описанием. 
``` JSON
POST /projects
{
	"Name": "New proj",
	"Description": "Smth new"
}
```
2. Добавить в проект нового члена команды с именем и ролью.
``` JSON
POST /projects/{projectId}/team-members
{
	"fName": "Serj",
	"role": "SA"
}
```
3. Создать новую задачу в рамках проекта с названием, описанием, назначенным членом команды и статусом.  
``` JSON
POST /projects/{projectId}/tasks
{
	"taskName": "New task",
	"desc": "new task for u",
	"memberAssigned": "122",
	"status": "New"
}
```
4. Обновить название или описание существующего проекта.
``` JSON
PUT /projects/{projectId}
{
	"Name": "New proj name",
	"Description": "new description"
}
```
5. Обновить роли члена команды в проекте. 
```JSON
PUT /projects/{projectId}/team-members/{memberId}
{
	"role": "New role"
}
```
6. Обновить название, описание, назначенного члена команды или статус задачи в проекте.  
``` JSON
PUT /projects/{projectId}/tasks/{taskId}
{
	"taskName": "New task name 1",
	"desc": "New desc 1",
	"memberAssigned": "New member id",
	"status": "In process"
}
```
7. Удалить члена команды из проекта.
``` JSON
DELETE /projects/{projectId}/team-members/{memberId}
```
8. Удалить задачу в проекте.
``` JSON
DELETE /projects/{projectId}/tasks/{taskId}
```
9. Удалить проект.
``` JSON
DELETE /projects/{projectId}
```
10. Получить отдельный проект со всеми его задачами и членами команды по его ID
``` JSON
GET /projects/{projectId}
```
11. Получить список всех проектов, включая их задачи и членов команды
``` JSON
GET /projects
```


## Задание: Реализовать пагинацию с использованием подходов limit, offset, count

Реализуйте пагинацию с использованием подходов limit, offset и count для REST API, управляющего библиотекой книг.  

Метод GET /books.  

API должен поддерживать получение книг с постраничной сортировкой, позволяя клиентам запрашивать определенное количество книг  
(лимит), пропускать определенное количество книг (смещение) и возвращать общее количество книг в коллекции.  

Следуйте этим требованиям:  

- Получить список всех книг, позволяя клиентам указывать лимит, смещение и, по желанию, возвращать общее количество книг в библиотеке.  
- По умолчанию limit должно быть 10, а offset по умолчанию должно быть 0.  
- Позволить клиентам сортировать список книг по названию или дате публикации  


Метод: GET  
Эндпоинт: /books  

Параметры запроса:  
limit: целое число (необязательно, по умолчанию 10)  
offset: целое число (необязательно, по умолчанию 0)  
sortBy: string (необязательно, значения: "title", "publicationDate", по умолчанию: "title")  
sortOrder: string (необязательно, значения "asc", "desc", по умолчанию "asc")  

Пример: 
``` JSON
GET /books?limit=20&offset=40&sortBy=publicationDate&sortOrder=desc  
```

