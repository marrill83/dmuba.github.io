# Guía LABORATORIO III: Introducción a Bases de Datos NOSQL

## Crear una db. 
Con botón derecho sobre la conexión, __Create Database__


![crear db](./img/creardb.png)


## Crear una colección
Botón derecho sobre *collections* __Create Collection__

![crear col](./img/crearcol.png)


## OPERACIONES CRUD

Ejemplo: cómo armar un documento JSON para importar a la base.

```javascript
    { 
        "_id": 1,
        "titulo": "Se estrelló un avión en Cuba",
        "cuerpo": "La aeronave cayó a poco de despegar del aeropuerto de La Habana. Era un Boeing 737 de una compañía aérea subsidiaria de Cubana de Aviación. El presidente cubano Miguel Díaz-Canel se dirigió de inmediato al lugar del accidente.",
        "fecha-hora": "2018-05-18 16:00:00"
    }
```

a) Incorporar un documento desde el shell

```javascript
    db.documentos.insertOne({ 
        "_id": 1,
        "titulo": "Se estrelló un avión en Cuba",
        "cuerpo": "La aeronave cayó a poco de despegar del aeropuerto de La Habana. Era un Boeing 737 de una compañía aérea subsidiaria de Cubana de Aviación. El presidente cubano Miguel Díaz-Canel se dirigió de inmediato al lugar del accidente.",
        "fecha-hora": "2018-05-18 16:00:00"
    })
```    

b) Buscar todos los documentos cargados en la colección.
```javascript
    db.documentos.find({})
```

c) Actualizar un atributo con __update__

```javascript
    db.documentos.update(
        {"_id": 1},
        {$set: {"titulo": "NOTICIA MODIFICADA EN DMUBA"}}
    )
```

d) Eliminar un documento de la colección

```javascript
    db.documentos.deleteOne({"_id": 3})
```
    
e) Incorporar varios documentos a través del shell

Con la instrucción db.<mi colección>.insert([{doc1}, {doc2}, ...,])

Ejemplo:

```javascript
    db.documentos.insert(
    [
        
    {
        "_id" : ObjectId("5af98a285987f909b4005ff3"),
        "status_id" : "996013967498776577",
        "created_at" : ISODate("2018-05-14T13:06:49.000Z"),
        "user_id" : "213888080",
        "screen_name" : "Florsube",
        "text" : "@perroscalle  piel de gallina imaginando la situación de Alejandro!cada uno con sus montruos, jajaja, y nosotros preocupados por el dólar y la inflación! tiburón, qué buscas en la orilla?",
        "source" : "Twitter Web Client",
        "reply_to_user_id" : "76727519",
        "reply_to_screen_name" : "perroscalle",
        "is_quote" : false,
        "is_retweet" : false,
```

El dataset de Tweets está disponible [acá](https://raw.githubusercontent.com/dmuba/dmuba.github.io/master/Practicos/guias/tweets-dolar.json).

d) Utilizar operadores de comparación

¿Cuantos tweets tienen más de un retweet?

```javascript

db.getCollection('tweets').find({retweet_count: {$gt: 1} })

```
Ver otros operadores [aquí](https://docs.mongodb.com/manual/reference/operator/query-comparison/)

e) Utilizar búsquedas por cadenas

¿Cuáles usuarios comienzan con P?

    db.getCollection('tweets').find({screen_name: {$regex: "^P.*"} })


## Algunas consultas más de ejemplo 

Tutorial con ejemplos de mongolite [[Ir]](https://jeroen.github.io/mongolite/query-data.html).

```R
# Queries con mongolite

# Recuperar los tweets que tienen más de 10 favoritos

q1 = tweets$find(query = '{"favorite_count":{"$gte": 10}}', 
                 limit = 10, 
                 fields='{"screen_name": "TRUE", "text": "TRUE", "favorite_count": "TRUE"}')

# Recuperar los tweets donde el código de pais es AR
q2 = tweets$find(query = '{"country_code": "AR"}', limit = 100)

# Recuperar los tweets que dicen inflaci.n 
q3 = tweets$find(query = '{"text": {"$regex": "inflaci.n", "$options" : "i"}}', limit = 100)

# Agregaciones con $aggregate y $project
# Contamos para cada usuario la cantidad de tweets N y el promedio de favoritos de sus publicaciones 

q4 = tweets$aggregate(
  '[{"$group":{"_id": "$screen_name", 
               "N": {"$sum":1}, 
                "PROM": {"$avg": "$favorite_count"}}}, 
    {"$project": {"screen_name": 1, "N": 1, "PROM":1}}]',
  options = '{"allowDiskUse":true}'
)




```

