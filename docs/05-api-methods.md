# 5. Методы API
Клиент предоставляет API для работы с сущностями сервиса. Основной интерфейс - `IEmployeeClient`.

##  Методы Person (Сотрудник)
### Создать или обновить сотрудника  
`PUT /person/{PersonId}`  

**Пример запроса:**
```
PUT /person/f47ac10b-58cc-4372-a567-0e02b2c3d479  

{
   "fullName": {
                "lastName": "Иванов",
                "firstName": "Иван", 
                "middleName": "Сергеевич"
               },
    "innFl": "123456789012"
}
```
**Пример ответа:**
```
200 OK  

{
  "guid": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
  "fullName": {
                "lastName": "Иванов",
                "firstName": "Иван", 
                "middleName": "Сергеевич"
              },
  "innFl": "123456789012"
}
```
### Получить сотрудника
`GET /person/{PersonId}`  

**Пример запроса:**
```
GET /person/f47ac10b-58cc-4372-a567-0e02b2c3d479  

{
   
}
```

**Пример ответа:**
```
200 OK  

{
  "guid": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
  "fullName": {
                "lastName": "Иванов",
                "firstName": "Иван", 
                "middleName": "Сергеевич"
              },
  "innFl": "123456789012"
}
```

## Методы Position (Должность)
### Создать или обновить должность
`PUT /position/{PositionId}`  

**Пример запроса:**
```
PUT /position/0d5f4c1a-6b6b-4f11-9f33-b5f63a8d1234

{
  "person": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
  "organization": "c56a4180-65aa-42ec-a945-5fd21dec0538",
  "title": "Главный бухгалтер"
}
```
**Пример ответа:**
```
200 OK  

{
  "positionId": "0d5f4c1a-6b6b-4f11-9f33-b5f63a8d1234",
  "title": "Главный бухгалтер",
  "person": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
  "organization": "c56a4180-65aa-42ec-a945-5fd21dec0538"
}
```
### Удалить должность
`DELETE /position/{PositionId}`   

**Пример запроса:**
``` 
DELETE /position/0d5f4c1a-6b6b-4f11-9f33-b5f63a8d1234   

{
   
}
```
**Пример ответа:**
```
204 No Content
```

## Методы Role (Роль)
### Создать или обновить роль
`PUT /role/{OrganizationId}/{RoleType}`  

**Пример запроса:**
```
PUT /role/b7c3a5ef-44f1-4e25-98b1-2f0c38c7e11f/1

{
  "person": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
  "organization": "b7c3a5ef-44f1-4e25-98b1-2f0c38c7e11f",
  "positionOrganization": "0d5f4c1a-6b6b-4f11-9f33-b5f63a8d1234"
}
```

**Пример ответа:**
```
200 OK  

{
  "type": "Head",
  "organization": "b7c3a5ef-44f1-4e25-98b1-2f0c38c7e11f",
  "person": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
  "positionOrganization": "0d5f4c1a-6b6b-4f11-9f33-b5f63a8d1234"
}
```
### Получить конкретную роль 
`GET /role/{OrganizationId}/{RoleType}`    

**Пример запроса:**
```
GET /role/b7c3a5ef-44f1-4e25-98b1-2f0c38c7e11f/1

{
 
}
```
**Пример ответа:**
```
{
    "person": {
        "guid": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
        "fullName": {
            "lastName": "Иванов",
            "firstName": "Иван",
            "middleName": "Сергеевич"
        },
        "innFl": "123456789012"
    },
    "position": {
        "person": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
        "organization": "b7c3a5ef-44f1-4e25-98b1-2f0c38c7e11f",
        "title": "Генеральный директор"
    }
}
```

### Получить все роли в организации
`GET /role/{OrganizationId}`      

**Пример запроса:**
```
GET /role/b7c3a5ef-44f1-4e25-98b1-2f0c38c7e11f

{
 
}
```  

**Пример ответа:**
```
{
    "Head": {
        "person": {
            "guid": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
            "fullName": {
                "lastName": "Иванов", 
                "firstName": "Иван",
                "middleName": "Сергеевич"
            }
        },
        "position": {
            "person": "f47ac10b-58cc-4372-a567-0e02b2c3d479",
            "organization": "b7c3a5ef-44f1-4e25-98b1-2f0c38c7e11f",
            "title": "Генеральный директор"
        }
    },
    "ChiefAccountant": {
        "person": {
            "guid": "c56a4180-65aa-42ec-a945-5fd21dec0538", 
            "fullName": {
                "lastName": "Петрова",
                "firstName": "Мария",
                "middleName": "Ивановнa"
            }
        },
        "position": {
            "person": "c56a4180-65aa-42ec-a945-5fd21dec0538",
            "organization": "b7c3a5ef-44f1-4e25-98b1-2f0c38c7e11f", 
            "title": "Главный бухгалтер"
        }
    }
}
```
