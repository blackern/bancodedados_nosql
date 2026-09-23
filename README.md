# 1. Paradigmas e Definições NoSQL

## Paradigmas Principais

* **Modelos:** Existem quatro tipos fundamentais de bancos de dados NoSQL.
* **Propósito:** Cada um resolve um problema específico de organização de dados.

## Os Quatro Modelos e Exemplos

* **Documentos:** Armazenam dados estruturados em formatos flexíveis (Ex: MongoDB).
* **Chave-Valor:** Estrutura simples de dicionário para buscas rápidas (Ex: Redis).
* **Famílias de Colunas:** Armazenamiento otimizado para colunas e grandes volumes (Ex: Cassandra).
* **Grafos:** Focados em mapear relacionamentos e conexões complexas (Ex: Neo4j).

---

# 2. Introdução ao MongoDB

## Significado do Nome

* **Origem:** Vem da palavra inglesa "Humongous" (que significa Gigante).
* **Objetivo:** Projetado para gerenciar grandes volumes de dados.

## Características Principais

* **Licença:** Banco de dados NoSQL de código aberto.
* **Modelo:** Orientado a documentos para armazenamento flexível.
* **Eficiência:** Alta capacidade para processar grandes quantidades de informações.

## Diferença do Modelo Tradicional

* **Relacional:** Usa tabelas rígidas com linhas e colunas (Ex: MySQL, PostgreSQL).
* **MongoDB:** Armazena os dados diretamente em documentos estruturados.

---

# 3. Arquitetura e Funcionamento do MongoDB

## Estrutura de Hospedagem

* **Servidor:** O host principal do sistema de banco de dados.
* **Múltiplos Bancos:** Um único servidor hospeda vários bancos de dados.

## Organização Interna

* **Coleções:** Agrupamentos lógicos equivalentes às tabelas (collections).
* **Documentos:** Registros individuais armazenados nas coleções (documents).

## Hierarquia de Dados

* **Fluxo:** Servidor ➔ Banco de Dados ➔ Coleções ➔ Documentos.

---

# 4. Formato de Dados JSON e BSON

## Natureza dos Registros

* **Documentos:** Todo registro salvo na base de dados é um documento individual.
* **Modelo:** Os objetos contêm uma lista ordenada de todos os elementos armazenados.

## Formato de Armazenamento

* **JSON:** Formato visual e textual de referência para a estrutura dos dados.
* **BSON:** Abreviação para Binary JSON (JSON Binário).
* **Interno:** O formato real usado em disco para otimizar leitura e espaço.

## Anatomia do Elemento

* **Composição:** Par de dados contendo identificação e conteúdo próprio.
* **Chave:** Nome do campo utilizado para o mapeamento (field name).
* **Dado:** Valor associado com a definição estrita do seu tipo.

---

# 5. Relacionamentos no MongoDB

## Abordagem Diferenciada

* **Minimização:** Reduz o uso de relacionamentos complexos entre coleções.
* **Modelo:** Focado na unificação dos dados em um único local.

### Modelo Tradicional (Relacional)

* **Divisão:** Separa informações relacionadas em múltiplas tabelas.
* **Junção:** Utiliza comandos de JOIN para unir os dados na consulta.

### Modelo MongoDB (Não Relacional)

* **Unificação:** Armazena os dados relacionados juntos no mesmo registro.
* **Mecanismo:** Utiliza documentos incorporados conhecidos como embedded documents.

---

# 6. Operações CRUD

## As operações fundamentais de banco de dados dividem-se em quatro ações principais, conhecidas pela sigla CRUD:

### Create

* `insertOne(data, options)`
* `insertMany(data, options)`

### Read

* `find(filter, options)`
* `findOne(filter, options)`

### Update

* `updateOne(filter, data, options)`
* `updateMany(filter, data, options)`
* `replaceOne(filter, data, options)`

### Delete

* `deleteOne(filter, options)`
* `deleteMany(filter, options)`

---

# 7. Comandos Shell

* **`show databases`**
  Exibe os bancos de dados disponíveis.

* **`use database`**
  Usado para trocar para o banco de dados informado.

* **`db.createCollection("nome_collection")`**
  Cria uma nova collection.

* **`show collections`**
  Mostra todas as collections.

* **`db.nome_collection.find()`**
  Retorna todos os documentos da collection.

* **`db.nome_collection.insertOne({objeto})`**
  Insere um documento na collection.

* **`db.nome_collection.insertMany([{objetos}])`**
  Insere vários documentos em uma collection.

* **`db.cliente.find({"nome": "Luis"})`**
  Busca documentos que possuem o campo nome com o valor **"Luis"**.

* **`db.cliente.find({_id: ObjectId("64a7b8c9d0e1f2a3b4c5d6e7")})`**
  Busca um documento pelo seu identificador único (`_id`).

## 7.1. Relacionamento One-to-One (Um para Um)

### Abordagem por Referência

**Quando usar:** Utilizada quando os documentos possuem ciclos de vida independentes, são muito grandes ou quando separar os dados evita duplicações desnecessárias e estouros no limite de tamanho do documento (16 MB).

```javascript
// Documento principal (Pessoa)
db.persons.insertOne({
  name: "Jefté",
  age: 35,
  salary: 3000
})

// Documento referenciado (Carro)
db.cars.insertOne({
  model: "BMW",
  price: 40000,
  owner: ObjectId("6aa9e2cee9c288ce1241317e")
})
```

Neste caso, a pessoa e o carro são entidades distintas do sistema. O carro aponta para a pessoa através do campo `owner`, contendo o `ObjectId`. Isso permite que o carro seja vendido ou trocado de dono sem alterar a estrutura do documento da pessoa.

---

## 7.2. Relacionamento One-to-Many (Um para Muitos)

Ocorre quando um documento principal possui múltiplos subelementos associados a ele. Por exemplo, uma postagem que possui vários comentários ou uma cidade que possui muitos cidadãos.

### Abordagem Embarcada (Embedded)

**Quando usar:** Indicada para cenários em que a quantidade de itens relacionados é limitada e conhecida, e os subdocumentos não precisam ser consultados ou alterados de forma totalmente independente do documento principal.

```javascript
db.questionThreads.insertOne({
  creator: "Jefté",
  question: "How does that work?",
  answers: [
    { text: "Like that." },
    { text: "Thanks!" }
  ]
})
```

Neste exemplo, as respostas de uma thread ficam armazenadas dentro de um array no mesmo documento, facilitando a consulta e a renderização completa da discussão em uma única operação.

### Abordagem por Referência

**Quando usar:** Indicada quando o lado "muitos" pode crescer indefinidamente, como milhares de transações financeiras de um cliente ou milhões de registros de sensores IoT. Nesses casos, manter todos os dados em um único documento poderia torná-lo excessivamente grande.

```javascript
// Documento pai (Cidade)
db.cities.insertOne({
  name: "New York City",
  coordinates: {
    lat: 21,
    lng: 55
  }
})

// Documentos filhos apontando para o pai
db.citizens.insertMany([
  {
    name: "Jefté Goes",
    cityId: ObjectId("5b98d6b44d01c52e1637a99f")
  },
  {
    name: "Brenno Salvador",
    cityId: ObjectId("5b98d6b44d01c52e1637a99f")
  }
])
```

Neste exemplo, a cidade armazena apenas suas próprias informações. Os cidadãos ficam armazenados separadamente na coleção `citizens`, e cada documento possui uma referência para a cidade através do campo `cityId`.

---

## 7.3. Relacionamento Many-to-Many (Muitos para Muitos)

Representa um cenário em que múltiplos documentos de uma coleção podem se relacionar com múltiplos documentos de outra coleção. Um exemplo é o relacionamento entre autores e livros, em que um autor pode escrever vários livros e um livro pode possuir vários autores.

### Abordagem Embarcada (Embedded)

**Quando usar:** Aplicada quando o relacionamento é restrito e os dados aninhados funcionam como um histórico ou snapshot que não precisa ser atualizado simultaneamente em múltiplos lugares.

```javascript
// Criando o documento base
db.customers.insertOne({
  name: "Jefté",
  age: 35
})

// Atualizando para embarcar os pedidos
db.customers.updateOne(
  {},
  {
    $set: {
      orders: [
        {
          title: "A Book",
          price: 12.99,
          quantity: 2
        }
      ]
    }
  }
)
```

Neste caso, os detalhes dos pedidos são armazenados diretamente no documento do cliente, permitindo consultar o histórico de compras junto com os demais dados do cliente.

### Abordagem por Referência

**Quando usar:** Indicada para relacionamentos muitos-para-muitos em que as entidades possuem existência independente. Utiliza arrays de `ObjectId` para relacionar os documentos entre diferentes coleções.

```javascript
// Inserindo os autores
db.authors.insertMany([
  {
    name: "Jorge Amado",
    age: 78,
    address: {
      street: "Bahia"
    }
  },
  {
    name: "Graciliano Ramos",
    age: 55,
    address: {
      street: "Rio de Janeiro"
    }
  }
])

// Atualizando o livro para referenciar os autores criados
db.books.updateOne(
  {},
  {
    $set: {
      authors: [
        ObjectId("5b98d9e44d01c52e1637a9a6"),
        ObjectId("5b98d9e44d01c52e1637a9a7")
      ]
    }
  }
)
```

Neste modelo, o livro armazena um array de referências contendo os `ObjectId` dos autores. Dessa forma, os autores e os livros permanecem em documentos separados e podem ser relacionados entre si por meio dessas referências.
