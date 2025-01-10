#### Сущности
1. **`Client`**  
   Представляет клиента.  
   ```graphql
   type Client {
     id: ID!
     name: String
     age: Int
     documents: [Document] # Связь с документами клиента
     relatives: [Relative] # Связь с родственниками клиента
   }
   ```

2. **`Document`**  
   Представляет документ клиента.  
   ```graphql
   type Document {
     id: ID!
     type: String
     number: String
     issueDate: String
     expiryDate: String
   }
   ```

3. **`Relative`**  
   Представляет родственника клиента.  
   ```graphql
   type Relative {
     id: ID!
     relationType: String
     name: String
     age: Int
   }
   ```

---

#### Запросы (Queries)
1. **Получение информации о клиенте (аналог `/clients/{id}`):**  
   ```graphql
   type Query {
     client(id: ID!): Client
   }
   ```

2. **Получение списка документов клиента (аналог `/clients/{id}/documents`):**  
   Это покрывается связью `Client.documents`.  

3. **Получение списка родственников клиента (аналог `/clients/{id}/relatives`):**  
   Это покрывается связью `Client.relatives`.  

---

### Пример использования GraphQL API

#### Запрос полной информации о клиенте, включая документы и родственников:  
```graphql
query GetClientData($id: ID!) {
  client(id: $id) {
    id
    name
    age
    documents {
      id
      type
      number
      issueDate
      expiryDate
    }
    relatives {
      id
      relationType
      name
      age
    }
  }
}
```

#### Запрос только документов клиента:  
```graphql
query GetClientDocuments($id: ID!) {
  client(id: $id) {
    documents {
      id
      type
      number
    }
  }
}
```

#### Запрос только родственников клиента:  
```graphql
query GetClientRelatives($id: ID!) {
  client(id: $id) {
    relatives {
      id
      relationType
      name
    }
  }
}
```
