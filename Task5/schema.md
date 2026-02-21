"""
Клиент – основная сущность сервиса client-info.
"""
type Client {
  id: ID!
  name: String
  age: Int
  """
  Список документов клиента. Может быть пустым.
  """
  documents: [Document!]!
  """
  Список родственников клиента. Может быть пустым.
  """
  relatives: [Relative!]!
}

"""
Документ клиента (паспорт, водительское удостоверение и т.п.).
"""
type Document {
  id: ID!
  type: String
  number: String
  issueDate: String
  expiryDate: String
}

"""
Информация о родственнике клиента.
"""
type Relative {
  id: ID!
  relationType: String   # например, "супруг", "ребёнок"
  name: String
  age: Int
}

"""
Корневой тип запросов.
"""
type Query {
  """
  Получить клиента по его идентификатору.
  """
  client(id: ID!): Client
}