# 1. Paradigmas e Definições NoSQL

## Paradigmas Principais

- **Modelos:** Existem quatro tipos fundamentais de bancos de dados NoSQL.
- **Propósito:** Cada um resolve um problema específico de organização de dados.

## Os Quatro Modelos e Exemplos

- **Documentos:** Armazenam dados estruturados em formatos flexíveis (Ex: MongoDB).
- **Chave-Valor:** Estrutura simples de dicionário para buscas rápidas (Ex: Redis).
- **Famílias de Colunas:** Armazenamiento otimizado para colunas e grandes volumes (Ex: Cassandra).
- **Grafos:** Focados em mapear relacionamentos e conexões complexas (Ex: Neo4j).

# 2. Introdução ao MongoDB

## Significado do Nome

- **Origem:** Vem da palavra inglesa "Humongous" (que significa Gigante).
- **Objetivo:** Projetado para gerenciar grandes volumes de dados.

## Características Principais

- **Licença:** Banco de dados NoSQL de código aberto.
- **Modelo Orientado a documentos para armazenamento flexível.**
- **Eficiência:** Alta capacidade para processar grandes quantidades de informações.

## Diferença do Modelo Tradicional
- **Relacional:** Usa tabelas rígidas com linhas e colunas (Ex: MySQL, PostgreSQL).
- **MongoDB:** Armazena os dados diretamente em documentos estruturados.

# 3. Arquitetura e Funcionamento do MongoDB

## Estrutura de Hospedagem

- **Servidor:** O host principal do sistema de banco de dados.
- **Múltiplos Bancos:** Um único servidor hospeda vários bancos de dados.

## Organização Interna

- **Coleções:** Agrupamentos lógicos equivalentes às tabelas (collections).
- **Documentos:** Registros individuais armazenados nas coleções (documents).

## Hierarquia de Dados

- **Fluxo:** Servidor ➔ Banco de Dados ➔ Coleções ➔ Documentos.

# 4. Formato de Dados JSON e BSON

## Natureza dos Registros

- **Documentos:** Todo registro salvo na base de dados é um documento individual.
- **Modelo:** Os objetos contêm uma lista ordenada de todos os elementos armazenados.

## Formato de Armazenamento

- **JSON:** Formato visual e textual de referência para a estrutura dos dados.
- **BSON:** Abreviação para Binary JSON (JSON Binário).
- **Interno:** O formato real usado em disco para otimizar leitura e espaço.

## Anatomia do Elemento

- **Composição:** Par de dados contendo identificação e conteúdo próprio.
- **Chave:** Nome do campo utilizado para o mapeamento (field name).
- **Dado:** Valor associado com a definição estrita do seu tipo.

# 5. Relacionamentos no MongoDB

## Abordagem Diferenciada

- **Minimização:** Reduz o uso de relacionamentos complexos entre coleções.
- **Modelo:** Focado na unificação dos dados em um único local.Modelo Tradicional (Relacional)
- **Divisão:** Separa informações relacionadas em múltiplas tabelas.
- **Junção:** Utiliza comandos de JOIN para unir os dados na consulta.

## Modelo MongoDB (Não Relacional)

- **Unificação:** Armazena os dados relacionados juntos no mesmo registro.
- **Mecanismo:** Utiliza documentos incorporados conhecidos como embedded documents.

# 6. Operações CRUD

## As operações fundamentais de banco de dados dividem-se em quatro ações principais, conhecidas pela sigla CRUD: 

- **Create:** 
  * insertOne(data, options)
  * insertMany(data, options)
- **Read:** 
  * find(filter, options)
  * findOne(filter, options)
- **Update:** 
  * updateOne(filter, data, options)
  * updateMany(filter, data, options)
  * replaceOne(filter, data, options)
- **Delete:** 
  * deleteOne(filter, options)
  * deleteMany(filter, options)

# 7. Comandos Shell

- **show databases:** Exibe os bancos de dados disponíveis. 
- **use database:** Usado para trocar para o banco de dados informado.
- **db.createCollection("nome_collection"):** Cria uma nova collection.
- **show collections:** Mostra todas as collections.
- **db.nome_collection.find():** Retorna todos os documentos da collection.
- **db.nome_collection.insertOne({objeto}):** Insere um documento na collection.
- **db.nome_collection.insertMany([{objetos}]):** Insere vários documentos em uma collection.
- **db.cliente.find({"nome": "Luis"}):** Busca documentos que possuem o campo nome com o valor **"Luis"**.
- **db.cliente.find({_id: ObjectId("64a7b8c9d0e1f2a3b4c5d6e7")}):** Busca um documento pelo seu identificador único (_id).
