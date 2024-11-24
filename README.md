# Módulo PyMongo

## Introdução ao MongoDB com Python.

### Execução e CRUD MongoDB

**Passos iniciais**

Com o MongoDB devidamente instalado, precisamos iniciar o cliente da aplicação, com os seguintes comandos:

```
sudo systemctl start mongod
sudo service mongod start
```

Para verificar se o MongoDB está em execução, utilize:

```
sudo systemctl status mongod
sudo service mongod status
```

Obs.: Utilize a tecla q para sair da verificação

Se tudo estiver correto, podemos iniciar o mongodb que estará sendo executado em nosso host local usando a porta padrão 27017:
```
mongo
```
### Criando o primeiro banco de dados com MongoDB

No MongoDB, o banco de dados e a tabela são criados automaticamente quando os dados são inseridos pela primeira vez.

Utilizamos o comando **use** para alternar entre bancos de dados ou para criar um banco de dados caso o banco de dados que deseja-se acessar ainda não tenha sido criado.

No exemplo abaixo, depois de inserir um único registro, o banco de dados “database” e a tabela “table” são criados dinamicamente.

```
use database
```

#### Para inserir um dado na tabela do banco de dados:

```
db.table.insert({
                nome:"Benjamin",
                idade: 10
               })
```

#### Para verificar os dados da tabela:
```
db.table.find()
```
### CRUD no MongoDB, utilizando o banco de dados veiculos e a tabela carros:
```
use veiculos
```
- Inserir dados na base (insert):
```
db.carros.insert({
                  marca:"Acura",
                  modelo: "Integra",
                  ano: 1992
                 })
 
db.carros.insert({
                  marca:"Acura",
                  modelo: "Legend",
                  ano: 1997
                })
 
db.carros.insert([{
                   marca:"Lotus",
                   modelo: "Elan",
                   ano: 1995
                 },
                 { 
                   marca:"Isuzu",
                   modelo: "Hombre",
                   ano: 1995
                }])
```

- Recuperar dados da base (find):
```
db.carros.find()
 
db.carros.find({marca: "Acura"})
 
db.carros.find({ano: 1995}).pretty()
```
- Atualizar dados da base (update):
```
db.carros.update({
                  ano: 1997
                 },
                 {
                  marca: "Bugre",
                  modelo: "Buggy",
                  ano: 1985
                })
 
db.carros.update({
                  modelo: "Integra"
                 },
                 { $set:
                  {
                   ano: 1995
                  }
                })
```

- Excluir dados da base (remove):
```
db.carros.remove({
                  marca: "Acura"
                })
```

## Utilizando MongoDB com Python

**Passos iniciais**

Para utilizarmos MongoDB com Python precisamos de uma biblioteca chamada **PyMongo**.

Para instalar o PyMongo é necessário ter o Python devidamente instalado e utilizar os seguintes comandos:
```
python3 -m pip install pymongo
```

Caso já tenha o PyMongo instalado e queira atualizá-lo:
```
python3 -m pip install --upgrade pymongo
```

Os comandos utilizados pelo PyMongo são bem semelhantes aqueles utilizados na linha de comando.

#### Exemplo script PyMongo

```
from pymongo import MongoClient

client = MongoClient("mongodb://localhost:27017")

database = client["veiculos"]

collection = database["carros"]

new_user = ("name": "Ben", "idade: 18)

collection.insert_one(new_user)

collection.find_one(new_user)

collection.update_one({"name": "Ben"},{"$set":("name": "Joao")})

#collection.delete_one({"name": "Ben"})
```

**Execução do script:**

```
python3 pymongo\ script.py

show dbs

use veiculos

db.carros.find()

```


