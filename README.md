# Banco de Dados Não Relacional - MongoDB (mongosh)

## Tecnologias utilizadas

* Docker
* MongoDB
* mongosh

---

# 1. Iniciando o MongoDB (Docker)

## 1.1 Criar o container

```bash
docker run -d --name mongo-escola -p 27017:27017 mongo
```
## 1.2 Verificar container em execução

```bash
docker ps
```

<img width="1288" height="151" alt="Image" src="https://github.com/user-attachments/assets/f00c3a72-3776-49d4-917e-a550238463c2" />

---

# 2. Conectando ao MongoDB

## 2.1 Acessar o mongosh

```bash
docker exec -it mongo-escola mongosh
```

<img width="1570" height="481" alt="Image" src="https://github.com/user-attachments/assets/f2a8614f-0cfe-4549-8ca3-cef486a276a3" />

---

# 3. Criando banco e collection

## 3.1 Selecionar/criar banco

```javascript
use escola
```
## 3.2 Criar collection alunos

```javascript
db.createCollection("alunos")
```

<img width="682" height="155" alt="Image" src="https://github.com/user-attachments/assets/733f3c00-b8b6-4fb7-a938-83823c39157f" />

---

# 4. Inserindo dados

## 4.1 Inserir múltiplos alunos

```javascript
db.alunos.insertMany([
{
  nome: "Rodrigo Pereira",
  idade: 27,
  curso: "SI",
  notas: [10, 2, 6],
  endereco: { cidade: "Maricá", estado: "RJ" }
},
{
  nome: "Ramona Santos",
  idade: 19,
  curso: "ADS",
  notas: [5, 4, 7],
  endereco: { cidade: "Niterói", estado: "RJ" }
},
{
  nome: "Tiffany Ferreira",
  idade: 22,
  curso: "SI",
  notas: [3, 6, 9],
  endereco: { cidade: "Rio de Janeiro", estado: "RJ" }
},
{
  nome: "Suellen Souza",
  idade: 25,
  curso: "ADS",
  notas: [8, 10, 7],
  endereco: { cidade: "São Gonçalo", estado: "RJ" }
},
{
  nome: "Lineu Fernandes",
  idade: 32,
  curso: "ADS",
  notas: [3, 1, 5],
  endereco: { cidade: "Maricá", estado: "RJ" }
}
])
```

<img width="1903" height="336" alt="Image" src="https://github.com/user-attachments/assets/cd49dbcd-226e-4467-bcbb-095fec3338a4" />

---

# 5. Consultas

## 5.1 Buscar todos os alunos

```javascript
db.alunos.find()
```

<img width="502" height="867" alt="Image" src="https://github.com/user-attachments/assets/2a38e526-2912-49d9-85f4-47eba49c4d0c" />

## 5.2 Buscar alunos do curso "ADS"

```javascript
db.alunos.find({ curso: "ADS" })
```

<img width="674" height="595" alt="Image" src="https://github.com/user-attachments/assets/ade4e7bd-4eaf-45b6-8930-0039953ebb87" />

---

## 5.3 Buscar alunos com idade maior que 21

```javascript
db.alunos.find({ idade: { $gt: 21 } })
```

<img width="669" height="753" alt="Image" src="https://github.com/user-attachments/assets/224b43d1-29d5-43bb-a7c0-ea5181e7c188" />

---

# 6. Atualizações

## 6.1 Atualizar idade de um aluno

```javascript
db.alunos.updateOne(
  { nome: "Rodrigo Pereira" },
  { $set: { idade: 24 } }
)
```

<img width="672" height="715" alt="Image" src="https://github.com/user-attachments/assets/1c9366b7-05df-4c65-ab28-c1d6f420e67a" />

---

## 6.2 Adicionar nova nota a um aluno

```javascript
db.alunos.updateOne(
  { nome: "Suellen Souza" },
  { $push: { notas: 10 } }
)
```

<img width="671" height="735" alt="Image" src="https://github.com/user-attachments/assets/e1e53cf2-2b72-4404-9d67-5519be7a25df" />

---

# 7. Remoção

## 7.1 Remover um aluno

```javascript
db.alunos.deleteOne({ nome: "Ramona Santos" })
```

<img width="671" height="354" alt="Image" src="https://github.com/user-attachments/assets/fa972c41-1a19-41f1-acec-385e4a836ae1" />

---

# 8. Aggregations

## 8.1 Média de notas por aluno

```javascript
db.alunos.aggregate([
  {
    $project: {
      nome: 1,
      media: { $avg: "$notas" }
    }
  }
])
```

<img width="770" height="514" alt="Image" src="https://github.com/user-attachments/assets/d9a3268a-5dea-4375-96af-da808d86b96a" />

---

## 8.2 Quantidade de alunos por curso

```javascript
db.alunos.aggregate([
  {
    $group: {
      _id: "$curso",
      quantidade: { $sum: 1 }
    }
  }
])
```

<img width="786" height="109" alt="Image" src="https://github.com/user-attachments/assets/41c24dd1-d268-4dbc-93b7-11330eb4e7c6" />

---
