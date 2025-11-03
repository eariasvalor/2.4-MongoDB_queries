# Tasca S2.04 – MongoDB Queries

## 🧩 Descripció

Aquest projecte inclou una sèrie de **consultes MongoDB** sobre la col·lecció **`restaurants`** de la ciutat de **Nova York**.  
L’objectiu és practicar **filtres, projeccions, ordenacions, operadors lògics i de comparació**, cerques amb **expressions regulars**, **operacions sobre arrays** i **consultes geogràfiques**.

---

## 🗃️ Col·lecció de dades: `restaurants`

La col·lecció `restaurants` conté informació detallada de milers d’establiments de la ciutat de Nova York. Cada document descriu un restaurant amb la seva ubicació, tipus de cuina i resultats d’inspeccions sanitàries.

### 📄 Estructura dels documents

```json
{
  "restaurant_id": "40356018",
  "name": "Riviera Caterer",
  "borough": "Brooklyn",
  "cuisine": "American ",
  "address": {
    "building": "2780",
    "street": "Stillwell Avenue",
    "zipcode": "11224",
    "coord": [-73.98242, 40.579505]
  },
  "grades": [
    { "date": { "$date": 1402358400000 }, "grade": "A", "score": 5 },
    { "date": { "$date": 1370390400000 }, "grade": "A", "score": 7 }
  ]
}
```

### 🧱 Camps principals

| Camp | Tipus | Descripció |
|------|-------|------------|
| **restaurant_id** | String | Identificador únic del restaurant. |
| **name** | String | Nom del restaurant. |
| **borough** | String | Districte de Nova York (*Bronx, Brooklyn, Manhattan, Queens, Staten Island*). |
| **cuisine** | String | Tipus de cuina o categoria gastronòmica. |
| **address.building** | String | Número o identificador de l’edifici. |
| **address.street** | String | Nom del carrer. |
| **address.zipcode** | String | Codi postal. |
| **address.coord** | Array<Number> | Coordenades GPS en format `[longitud, latitud]`. |
| **grades** | Array<Object> | Llista d’inspeccions amb data, lletra de qualificació i puntuació (`score`). |

---

## 📋 Consultes a realitzar

S’han de desenvolupar les consultes següents sobre la col·lecció `restaurants` (una per línia en el fitxer final):

1. Mostra **tots** els documents.  
2. Mostra `restaurant_id`, `name`, `borough`, `cuisine`.  
3. Igual que l’anterior, però **sense `_id`**.  
4. Mostra `restaurant_id`, `name`, `borough` i `zipcode` (sense `_id`).  
5. Restaurants situats al **Bronx**.  
6. **Primers 5** restaurants del Bronx.  
7. Els **5 següents** (saltant els primers 5).  
8. Restaurants amb **score > 90**.  
9. Restaurants amb **80 < score < 100**.  
10. Restaurants amb **latitud < -95.754168**.  
11. Restaurants que **no** preparen *American*, amb **score > 70** i **longitud < -65.754168**.  
12. Igual que (11), **sense `$and`**.  
13. Restaurants que **no** preparen *American*, amb **grade “A”**, fora de **Brooklyn**, ordenats per `cuisine` descendent.  
14. Restaurants amb **nom començant per “Wil”**.  
15. Restaurants amb **nom acabat en “ces”**.  
16. Restaurants amb **“Reg”** en qualsevol posició del nom.  
17. Restaurants del **Bronx** que fan **American** o **Chinese**.  
18. Restaurants de **Staten Island, Queens, Bronx o Brooklyn**.  
19. Restaurants **fora** d’aquests districtes.  
20. Restaurants amb **score ≤ 10**.  
21. Restaurants que fan **peix** excepte *American* i *Chinese*, o amb nom començant per “Wil”.  
22. Restaurants amb **grade “A”** i **score 11** el **2014-08-11**.  
23. Restaurants on el **2n element de `grades`** té **grade “A”**, **score 9** i data **2014-08-11**.  
24. Restaurants on el **segon element de `coord`** és **entre 42 i 52**.  
25. Ordena els restaurants per **nom ascendent**.  
26. Ordena els restaurants per **nom descendent**.  
27. Ordena per **cuisine ascendent** i, dins del mateix **borough**, descendent.  
28. Direccions **sense camp `street`**.  
29. Documents on **`address.coord` és numèric (Double)**.  
30. Restaurants on **`score % 7 == 0`**.  
31. Restaurants amb **“mon”** en algun lloc del nom.  
32. Restaurants amb **nom començant per “Mad”**.

---

## 🧠 Nivells de competència

- **Nivell 1:** 17 consultes correctes.  
- **Nivell 2:** Entre 17 i 25 consultes correctes.  
- **Nivell 3:** Més de 25 consultes correctes.

---

## ⚙️ Requisits tècnics

- **MongoDB 6.0+** i **mongosh**.  
- Dataset: [`restaurants.json`](./data/restaurants.json).  
- Projecte preparat per executar-se amb **Docker Compose**.  

### Exemple de `docker-compose.yml`

```yaml
version: '3.8'

services:
  mongodb:
    image: mongo:latest
    container_name: mongodb
    restart: unless-stopped
    ports:
      - "27017:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: admin123
    volumes:
      - mongodb_data:/data/db

volumes:
  mongodb_data:
```

---

## ▶️ Execució

1. **Arrenca els serveis:**
   ```bash
   docker compose up -d
   ```
2. **Importa el dataset:**
   ```bash
   mongoimport      --uri "mongodb://admin:admin123@localhost:27017/admin"      --db ny      --collection restaurants      --file ./data/restaurants.json      --jsonArray
   ```
3. **Connecta’t amb mongosh:**
   ```bash
   mongosh "mongodb://admin:admin123@localhost:27017/ny?authSource=admin"
   ```
4. **Executa les consultes** sobre la col·lecció `ny.restaurants`.

---

## 🗂️ Estructura del repositori

```
2.4-MongoDB_queries/
├─ restaurants_queries.js
├─ src/
│  └─ restaurants.json
│  └─ docker-compose.yml
└─ README.md
```

---

## 📦 Lliurament

Envia la URL d’un repositori **`mongoDB-queries`** amb:

- ✅ `src/queries.js` → totes les consultes, una per línia.  
- 📁 Dataset `data/restaurants.json` i `docker-compose.yml`.  
